# Coding Standards

## General Principles

1. **Readability over cleverness** - Code is read more than written
2. **Consistency** - Follow established project patterns
3. **Simplicity** - Prefer simple solutions
4. **DRY** - Don't repeat yourself (but don't over-abstract)
5. **YAGNI** - You aren't gonna need it (avoid premature optimization)

## Naming Conventions

### Variables and Functions

```typescript
// Use descriptive, meaningful names
const userAge = 25;                    // ✓ Clear
const a = 25;                          // ✗ Unclear

// Boolean names should be questions
const isActive = true;                 // ✓
const hasPermission = false;           // ✓
const active = true;                   // ✗ Ambiguous

// Functions should be verbs
function calculateTotal() {}           // ✓
function fetchUserData() {}            // ✓
function userData() {}                 // ✗ Not a verb
```

### Classes and Types

```typescript
// PascalCase for classes and types
class UserAccount {}
interface PaymentMethod {}
type OrderStatus = 'pending' | 'complete';

// Prefix interfaces with 'I' only if project convention
interface IUserRepository {}           // Some projects
interface UserRepository {}            // Others
```

### Files and Directories

```
// kebab-case for files
user-service.ts
payment-controller.ts

// Match export name
UserService.ts → export class UserService
```

## Code Structure

### Function Length

- Functions should do one thing
- Aim for < 20 lines (guideline, not rule)
- If you need comments to explain sections, consider extracting

### File Length

- < 300 lines is a good target
- Split when file has multiple responsibilities

### Nesting

```typescript
// Avoid deep nesting
// ✗ Bad
if (user) {
  if (user.isActive) {
    if (user.hasPermission) {
      // do something
    }
  }
}

// ✓ Good - early returns
if (!user) return;
if (!user.isActive) return;
if (!user.hasPermission) return;
// do something
```

## Error Handling

```typescript
// Be specific with errors
// ✗ Bad
throw new Error('Something went wrong');

// ✓ Good
throw new NotFoundError(`User ${userId} not found`);

// Always handle async errors
// ✗ Bad
async function fetchUser() {
  const user = await db.getUser(id);
  return user;
}

// ✓ Good
async function fetchUser() {
  try {
    const user = await db.getUser(id);
    if (!user) throw new NotFoundError(`User ${id} not found`);
    return user;
  } catch (error) {
    logger.error('Failed to fetch user', { id, error });
    throw error;
  }
}
```

## Comments

```typescript
// ✗ Bad - obvious comments
// increment i by 1
i++;

// ✓ Good - explain WHY, not WHAT
// Using binary search because the list is sorted and can be very large
const index = binarySearch(sortedList, target);

// ✓ Good - document complex business logic
// Tax calculation follows IRS Publication 15-T (2024)
// See: https://www.irs.gov/pub/irs-pdf/p15t.pdf
function calculateWithholding(income: number) {}
```

## TypeScript Specific

```typescript
// Use strict mode
// Avoid 'any' - use 'unknown' if type is truly unknown

// ✗ Bad
function process(data: any) {}

// ✓ Good
function process(data: unknown) {
  if (isValidData(data)) {
    // now TypeScript knows the type
  }
}

// Use type guards
function isUser(obj: unknown): obj is User {
  return typeof obj === 'object' && obj !== null && 'id' in obj;
}

// Prefer interfaces for objects, types for unions/primitives
interface User {
  id: string;
  name: string;
}

type Status = 'active' | 'inactive';
type ID = string | number;
```

## React Specific

```tsx
// Use functional components with hooks
const UserProfile: React.FC<Props> = ({ user }) => {
  const [isEditing, setIsEditing] = useState(false);
  
  // Hooks at the top, handlers next, render last
  const handleSave = useCallback(() => {
    // save logic
  }, [dependencies]);

  return <div>...</div>;
};

// Avoid inline functions in JSX for performance
// ✗ Bad
<Button onClick={() => handleClick(id)} />

// ✓ Good
const handleButtonClick = useCallback(() => handleClick(id), [id]);
<Button onClick={handleButtonClick} />
```

## Import Order

```typescript
// 1. External libraries
import React from 'react';
import { useQuery } from '@tanstack/react-query';

// 2. Internal modules (absolute paths)
import { UserService } from '@/services/user';
import { Button } from '@/components/ui';

// 3. Relative imports
import { UserCard } from './UserCard';
import { formatDate } from './utils';

// 4. Types (if separate)
import type { User } from '@/types';

// 5. Styles
import styles from './styles.module.css';
```
