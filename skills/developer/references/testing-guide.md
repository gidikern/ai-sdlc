# Testing Guide

## Test Pyramid

```
        /\
       /  \      E2E Tests (Few)
      /────\     Integration Tests (Some)
     /──────\    Unit Tests (Many)
    /────────\
```

| Level | What | Tools | Speed |
|-------|------|-------|-------|
| Unit | Functions, classes | Jest, Vitest | Fast |
| Integration | API endpoints, DB | Supertest, Testcontainers | Medium |
| E2E | User flows | Playwright, Cypress | Slow |

## Unit Testing

### Structure: AAA Pattern

```typescript
describe('calculateTotal', () => {
  it('should calculate total with tax', () => {
    // Arrange
    const items = [{ price: 100 }, { price: 50 }];
    const taxRate = 0.1;

    // Act
    const result = calculateTotal(items, taxRate);

    // Assert
    expect(result).toBe(165);
  });
});
```

### Naming Convention

```typescript
// describe: Component/Function name
// it: should [expected behavior] when [condition]

describe('UserService', () => {
  describe('createUser', () => {
    it('should create a user with valid data', () => {});
    it('should throw ValidationError when email is invalid', () => {});
    it('should hash password before saving', () => {});
  });
});
```

### What to Test

```typescript
// ✓ Test
- Business logic
- Edge cases (null, empty, boundary values)
- Error handling
- State transitions

// ✗ Don't Test
- External libraries
- Simple getters/setters
- Framework code
- Implementation details
```

### Mocking

```typescript
// Mock external dependencies
jest.mock('@/services/email', () => ({
  sendEmail: jest.fn().mockResolvedValue(true),
}));

// Use dependency injection for easier testing
class UserService {
  constructor(private emailService: EmailService) {}
  
  async createUser(data: UserData) {
    const user = await this.saveUser(data);
    await this.emailService.sendWelcome(user.email);
    return user;
  }
}

// In tests
const mockEmailService = { sendWelcome: jest.fn() };
const service = new UserService(mockEmailService);
```

## Integration Testing

### API Testing

```typescript
import request from 'supertest';
import { app } from '@/app';

describe('POST /api/users', () => {
  it('should create a user and return 201', async () => {
    const response = await request(app)
      .post('/api/users')
      .send({ email: 'test@example.com', name: 'Test' })
      .expect(201);

    expect(response.body).toMatchObject({
      id: expect.any(String),
      email: 'test@example.com',
    });
  });

  it('should return 400 for invalid email', async () => {
    await request(app)
      .post('/api/users')
      .send({ email: 'invalid', name: 'Test' })
      .expect(400);
  });
});
```

### Database Testing

```typescript
// Use test database or containers
beforeAll(async () => {
  await db.connect(process.env.TEST_DATABASE_URL);
});

beforeEach(async () => {
  await db.truncateAll(); // Clean slate
});

afterAll(async () => {
  await db.disconnect();
});
```

## E2E Testing

### Page Object Pattern

```typescript
// pages/LoginPage.ts
class LoginPage {
  constructor(private page: Page) {}

  async login(email: string, password: string) {
    await this.page.fill('[data-testid="email"]', email);
    await this.page.fill('[data-testid="password"]', password);
    await this.page.click('[data-testid="submit"]');
  }

  async expectError(message: string) {
    await expect(this.page.locator('.error')).toHaveText(message);
  }
}

// tests/login.spec.ts
test('successful login', async ({ page }) => {
  const loginPage = new LoginPage(page);
  await page.goto('/login');
  await loginPage.login('user@example.com', 'password');
  await expect(page).toHaveURL('/dashboard');
});
```

## Test Data

### Factories

```typescript
// factories/user.ts
export const createUser = (overrides = {}): User => ({
  id: faker.string.uuid(),
  email: faker.internet.email(),
  name: faker.person.fullName(),
  createdAt: new Date(),
  ...overrides,
});

// Usage
const user = createUser({ email: 'specific@email.com' });
```

### Fixtures

```typescript
// fixtures/users.json
{
  "adminUser": {
    "id": "admin-1",
    "role": "admin",
    "email": "admin@example.com"
  }
}
```

## Coverage

Target meaningful coverage, not 100%:

| Type | Target |
|------|--------|
| Critical paths | 90%+ |
| Business logic | 80%+ |
| Utilities | 70%+ |
| UI components | 60%+ |

```bash
# Run with coverage
npm test -- --coverage

# Coverage report
---------------------------|---------|
File                       | % Stmts |
---------------------------|---------|
All files                  | 78.5    |
 src/services/user.ts      | 92.3    |
 src/utils/format.ts       | 85.0    |
---------------------------|---------|
```
