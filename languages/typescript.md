# TypeScript

## Overview
TypeScript is a strongly typed programming language that builds on JavaScript, adding static type definitions and advanced features for large-scale application development.

## Core Concepts

### Basic Types
```typescript
// Primitive Types
let name: string = "John";
let age: number = 30;
let isActive: boolean = true;
let nothing: null = null;
let notDefined: undefined = undefined;

// Arrays
let numbers: number[] = [1, 2, 3];
let strings: Array<string> = ["a", "b", "c"];

// Tuples
let tuple: [string, number] = ["hello", 42];

// Enums
enum Direction {
  Up = "UP",
  Down = "DOWN",
  Left = "LEFT",
  Right = "RIGHT"
}

// Any and Unknown
let flexible: any = "anything";
let safe: unknown = "must check type first";
```

### Interfaces
```typescript
interface User {
  id: number;
  name: string;
  email: string;
  age?: number;  // Optional property
  readonly createdAt: Date;  // Read-only
}

// Extending interfaces
interface Admin extends User {
  permissions: string[];
}

// Function interface
interface SearchFunc {
  (query: string, limit?: number): Promise<User[]>;
}
```

### Types
```typescript
// Type Alias
type ID = string | number;

// Union Types
type Status = "pending" | "success" | "error";

// Intersection Types
type Employee = User & {
  department: string;
  salary: number;
};

// Utility Types
type PartialUser = Partial<User>;      // All properties optional
type RequiredUser = Required<User>;     // All properties required
type ReadonlyUser = Readonly<User>;     // All properties readonly
type UserName = Pick<User, "name">;     // Pick specific properties
type WithoutEmail = Omit<User, "email">; // Omit specific properties
```

### Generics
```typescript
// Generic Function
function identity<T>(arg: T): T {
  return arg;
}

// Generic Interface
interface Container<T> {
  value: T;
  getValue(): T;
}

// Generic Class
class Box<T> {
  private content: T;
  
  constructor(value: T) {
    this.content = value;
  }
  
  get(): T {
    return this.content;
  }
}

// Generic Constraints
interface Lengthwise {
  length: number;
}

function logLength<T extends Lengthwise>(arg: T): number {
  return arg.length;
}
```

### Classes
```typescript
class Animal {
  private name: string;
  protected species: string;
  public readonly id: number;
  
  constructor(name: string, species: string) {
    this.name = name;
    this.species = species;
    this.id = Math.random();
  }
  
  public speak(): void {
    console.log(`${this.name} makes a sound`);
  }
}

// Abstract Classes
abstract class Shape {
  abstract getArea(): number;
  
  describe(): string {
    return `Area: ${this.getArea()}`;
  }
}

class Circle extends Shape {
  constructor(private radius: number) {
    super();
  }
  
  getArea(): number {
    return Math.PI * this.radius ** 2;
  }
}
```

### Type Guards
```typescript
// typeof guard
function processValue(value: string | number) {
  if (typeof value === "string") {
    return value.toUpperCase();
  }
  return value * 2;
}

// instanceof guard
function logError(error: Error | string) {
  if (error instanceof Error) {
    console.log(error.message);
  } else {
    console.log(error);
  }
}

// Custom type guard
function isUser(obj: any): obj is User {
  return obj && typeof obj.name === "string" && typeof obj.id === "number";
}
```

### Decorators
```typescript
// Class Decorator
function sealed(constructor: Function) {
  Object.seal(constructor);
  Object.seal(constructor.prototype);
}

// Method Decorator
function log(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
  const original = descriptor.value;
  descriptor.value = function(...args: any[]) {
    console.log(`Calling ${propertyKey} with:`, args);
    return original.apply(this, args);
  };
}

@sealed
class Example {
  @log
  greet(name: string) {
    return `Hello, ${name}!`;
  }
}
```

### Module System
```typescript
// Named exports
export interface Config {
  apiUrl: string;
}

export function fetchData(): Promise<void> {
  // ...
}

// Default export
export default class ApiClient {
  // ...
}

// Import
import ApiClient, { Config, fetchData } from './api';
import type { User } from './types';  // Type-only import
```

## Best Practices

1. **Enable strict mode** in tsconfig.json
2. **Prefer interfaces** over type aliases for object types
3. **Use unknown instead of any** when type is truly unknown
4. **Leverage type inference** - don't over-annotate
5. **Use readonly** for immutable properties
6. **Prefer const assertions** for literal types
7. **Use discriminated unions** for complex state

## tsconfig.json
```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "ESNext",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "outDir": "./dist",
    "rootDir": "./src",
    "declaration": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"]
}
```

## Resources
- TypeScript Handbook
- TypeScript Deep Dive
- DefinitelyTyped (@types packages)
