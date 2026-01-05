# TypeScript Project CLAUDE.md Template

Add these sections to your TypeScript project's CLAUDE.md alongside the general rules.

---

## Commands

```bash
# Development
npm install                      # Install dependencies
npm run dev                      # Start dev server
npm run build                    # Production build

# Testing
npm test                         # Run all tests
npm run test:watch               # Watch mode
npm run test:coverage            # With coverage

# Linting & Formatting
npm run lint                     # ESLint
npm run lint:fix                 # Auto-fix issues
npm run format                   # Prettier

# Type Checking
npm run typecheck                # tsc --noEmit
```

## Standards

- TypeScript strict mode enabled
- ESLint + Prettier for linting and formatting
- Vitest or Jest for testing
- Functional components with hooks (React projects)

## Directory Structure

```
project/
├── src/
│   ├── components/              # React components (if applicable)
│   ├── hooks/                   # Custom hooks
│   ├── services/                # API and business logic
│   ├── utils/                   # Shared utilities
│   ├── types/                   # TypeScript type definitions
│   └── index.ts
├── tests/
│   ├── unit/
│   └── integration/
├── package.json
├── tsconfig.json
└── CLAUDE.md
```

## Testing Requirements

- Co-locate unit tests with source (`*.test.ts`) or in `tests/unit/`
- Use Testing Library for React component tests
- Avoid mocking unless necessary for external services
- Target 80%+ coverage on new code

## Code Patterns

### Type Definitions
```typescript
// Prefer interfaces for objects, types for unions/intersections
interface User {
  id: string;
  name: string;
  email: string;
}

type Status = 'pending' | 'active' | 'completed';

// Use generics for reusable patterns
function fetchData<T>(url: string): Promise<T> {
  return fetch(url).then(res => res.json());
}
```

### Error Handling
```typescript
// Use Result pattern or explicit error types
type Result<T, E = Error> =
  | { success: true; data: T }
  | { success: false; error: E };

async function fetchUser(id: string): Promise<Result<User>> {
  try {
    const user = await api.getUser(id);
    return { success: true, data: user };
  } catch (error) {
    return { success: false, error: error as Error };
  }
}
```

### React Patterns (if applicable)
```typescript
// Functional components with explicit return types
interface ButtonProps {
  label: string;
  onClick: () => void;
  disabled?: boolean;
}

export function Button({ label, onClick, disabled = false }: ButtonProps): JSX.Element {
  return (
    <button onClick={onClick} disabled={disabled}>
      {label}
    </button>
  );
}

// Custom hooks with descriptive names
function useUserData(userId: string) {
  const [user, setUser] = useState<User | null>(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetchUser(userId).then(result => {
      if (result.success) setUser(result.data);
      setLoading(false);
    });
  }, [userId]);

  return { user, loading };
}
```

### Async Patterns
```typescript
// Prefer async/await over .then chains
async function processItems(items: Item[]): Promise<ProcessedItem[]> {
  const results = await Promise.all(
    items.map(item => processItem(item))
  );
  return results.filter(Boolean);
}
```

## tsconfig.json Essentials

```json
{
  "compilerOptions": {
    "strict": true,
    "noUncheckedIndexedAccess": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true,
    "esModuleInterop": true,
    "skipLibCheck": true
  }
}
```

## Notes

- Prefer `const` over `let`; avoid `var`
- Use optional chaining (`?.`) and nullish coalescing (`??`)
- Export types alongside implementations
- Keep components small and focused
