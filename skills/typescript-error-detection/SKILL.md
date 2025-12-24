---
name: TypeScript Error Detection and Debugging
description: This skill activates when you're debugging TypeScript/JavaScript build errors, compilation failures, or type mismatches. Provides patterns for common errors, root cause analysis techniques, and fixes for type-related issues across frameworks.
version: 1.0.0
---

# TypeScript Error Detection and Debugging

When builds fail with TypeScript errors or type checking issues, this skill provides structured debugging approaches and common patterns you'll encounter.

## Common TypeScript Error Categories

### Category 1: Type Mismatches

**Pattern: "Property X does not exist on type Y"**

**Root causes:**
- Interface/type doesn't match actual implementation
- Missing optional property marker (`?`)
- Wrong property name (typo)
- Property added after type definition

**Debugging approach:**
1. Check the type definition file (interface, type alias)
2. Compare against actual implementation
3. Verify property names match exactly (case-sensitive)
4. Check if property should be optional

**Common fix:**
```typescript
// ❌ BEFORE: Property missing from interface
interface User {
  name: string
  email: string
}

const user = {
  name: "John",
  email: "john@example.com",
  avatar: "/avatar.png"  // ❌ Not in interface!
}

// ✅ AFTER: Add optional property
interface User {
  name: string
  email: string
  avatar?: string  // ✅ Now it matches
}
```

**Prevention:** Always update type definitions when adding properties.

---

### Category 2: Missing Type Annotations

**Pattern: "Implicit 'any' type"**

**Root causes:**
- Function parameter missing type annotation
- Variable assigned without type hint
- Function return type not specified
- Component props not properly typed

**Debugging approach:**
1. Find the line with the error
2. Identify if it's a function parameter, variable, or return
3. Add explicit type annotation
4. Or use type inference if it's clear

**Common fix:**
```typescript
// ❌ BEFORE: Implicit any
function processData(data) {
  return data.toUpperCase()
}

// ✅ AFTER: Explicit type
function processData(data: string): string {
  return data.toUpperCase()
}
```

**Prevention:** Enable `noImplicitAny` in `tsconfig.json`.

---

### Category 3: Component Props Type Issues

**Pattern: "Type error in JSX/React component"**

**Root causes:**
- Props interface missing required properties
- Passing props that don't exist in component definition
- Children type not properly defined
- Event handlers have wrong signature

**Debugging approach:**
1. Find component definition
2. Check its props interface
3. Verify all passed props exist in interface
4. Verify prop types match usage

**Common fix:**
```typescript
// ❌ BEFORE: Props interface incomplete
interface ButtonProps {
  text: string
}

function Button({ text, onClick }: ButtonProps) {
  return <button onClick={onClick}>{text}</button>
}

// ✅ AFTER: Add missing prop
interface ButtonProps {
  text: string
  onClick: () => void
}

function Button({ text, onClick }: ButtonProps) {
  return <button onClick={onClick}>{text}</button>
}
```

**Prevention:** Keep component props interfaces in sync with actual usage.

---

### Category 4: Union Type Errors

**Pattern: "This value of type A cannot be assigned to type B | C"**

**Root causes:**
- Type narrowing not done correctly
- Missing type guard
- Assumption about type without checking

**Debugging approach:**
1. Identify what the union type expects
2. Check if value could be one of the union types
3. Add type guard or conditional

**Common fix:**
```typescript
// ❌ BEFORE: No type guard
function getValue(value: string | number): string {
  return value.toUpperCase()  // ❌ number doesn't have toUpperCase
}

// ✅ AFTER: Type guard
function getValue(value: string | number): string {
  if (typeof value === 'string') {
    return value.toUpperCase()
  }
  return String(value)
}
```

**Prevention:** Always guard union types before using type-specific methods.

---

### Category 5: Array Type Issues

**Pattern: "Type 'string | null' is not assignable to type 'string[]'"**

**Root causes:**
- Array element type mismatch
- Null/undefined not handled
- Mixed types in array

**Debugging approach:**
1. Check array element type definition
2. Verify all elements match that type
3. Handle null/undefined if present
4. Use type assertion if intentional

**Common fix:**
```typescript
// ❌ BEFORE: Type mismatch
const items: string[] = [
  "apple",
  "banana",
  null  // ❌ null not in type
]

// ✅ AFTER: Include null in type
const items: (string | null)[] = [
  "apple",
  "banana",
  null
]
```

**Prevention:** Be explicit about optional/nullable array elements.

---

## Build Error Debugging Workflow

### Step 1: Read the Error Message Completely

The error message tells you:
- **File and line number** where error occurred
- **Exact error code** (e.g., TS2339)
- **What went wrong** (description)
- **What type was expected** vs **what you provided**

### Step 2: Locate the Problematic Code

Find the exact line mentioned in the error. Look at:
- The variable/property in question
- The type it's being assigned to
- Any type annotations

### Step 3: Check Type Definitions

Find where the type is defined:
- Interface definition
- Type alias
- Class declaration
- Function signature

### Step 4: Compare Implementation vs Definition

Ask:
- Does the implementation match the type definition?
- Are all required properties present?
- Do property names match exactly?
- Are types compatible?

### Step 5: Apply the Fix

Common fixes:
- Update interface to match implementation
- Add missing type annotations
- Add type guards for union types
- Use type assertions (carefully!)

### Step 6: Verify with Build

```bash
npm run build
# or
npx tsc --noEmit
```

---

## TypeScript Configuration Best Practices

**Strict mode catches more errors:**
```json
{
  "compilerOptions": {
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    "strictFunctionTypes": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noImplicitReturns": true
  }
}
```

**Benefits:**
- Catches type errors during development
- Forces explicit typing
- Prevents subtle bugs
- Makes code more maintainable

---

## Quick Reference: Common Error Codes

| Error Code | Meaning | Fix |
|-----------|---------|-----|
| TS2322 | Type not assignable | Check type compatibility |
| TS2339 | Property doesn't exist | Add to interface or check name |
| TS2345 | Argument of wrong type | Match function parameter type |
| TS2339 | Implicit 'any' | Add type annotation |
| TS2532 | Object is possibly null | Add null check |
| TS2740 | Missing properties | Add required properties |

---

## When to Use Type Assertions (Carefully!)

Type assertions (`as Type`) should be rare. Only use when:
1. You know more about the type than TypeScript does
2. You've verified it's safe
3. You've documented why

```typescript
// ✅ OK: You control the JSON structure
const data = JSON.parse(json) as UserData

// ❌ Bad: Hiding type error
const value = someUnknownValue as string  // Could be null!
```

---

## Integration with CI/CD

**Before deployment, verify:**
```bash
# Full type check
npm run build

# Or just type check (no emit)
npx tsc --noEmit

# With strict settings
npx tsc --strict --noEmit
```

**Catch type errors BEFORE Vercel/CI sees them.**
