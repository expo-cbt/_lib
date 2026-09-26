# Frontend Developer Trivia

## Feature-based Directory Structure

A feature-based directory structure groups files by feature/domain (e.g. `features/auth/`, `features/dashboard/`) instead of by file type (`components/`, `hooks/`, `services/`), keeping each feature's components, hooks, styles, and tests together.

- **Structure**: each feature gets its own folder under `src/features/`, e.g. `src/features/auth/`, `src/features/cart/`, `src/features/profile/`
- **Contents per feature**: components, hooks, types, API calls, and tests specific to that feature live together instead of being scattered across global `components/`, `hooks/`, `services/` folders
- **Shared code**: truly reusable pieces (generic UI components, utility functions, shared hooks) go into a top-level `shared/` or `common/` folder
- **Barrel exports**: each feature folder usually has an `index.ts` that exports only what other parts of the app need, hiding internal implementation details
- **Scalability**: as the app grows, you add/remove feature folders instead of hunting through type-based folders that balloon in size
- **Coupling**: encourages low coupling between features and high cohesion within a feature, since everything related lives in one place
- **Testing**: colocating tests with the feature they test makes it easier to find and maintain them
- **Common pitfall**: overlapping features can cause duplication if boundaries aren't well defined, so some teams add a `core/` or `lib/` layer for cross-cutting concerns (auth context, routing, config)

Typical layout:

```sh
src/
  features/
    auth/
      components/
      hooks/
      api.ts
      types.ts
      index.ts
    cart/
      components/
      hooks/
      api.ts
      types.ts
      index.ts
  shared/
    components/
    hooks/
    utils/
  app/
    App.tsx
    routes.tsx
```

## Atomic Design Pattern

**Atomic Design** — a component organization pattern (Brad Frost), structuring UI into 5 levels of increasing complexity:

- **Atoms** — smallest building blocks: `Button`, `Text`, `Input`, `Icon`
- **Molecules** — collection of atoms: `FormField` (label + input), `DataTable`
- **Organisms** — shared UI sections: `Header`, `Nav`, `Aside`, `Footer`
- **Templates** — page layout skeletons, arranging organisms without real data
- **Pages** — templates filled with real/actual data — the final screen

#### Classic folder structure:

```sh
components/
  atoms/
    Button.tsx
    Text.tsx
  molecules/
    SearchBar.tsx
  organisms/
    TransactionListItem.tsx
    Header.tsx
  templates/
    DashboardTemplate.tsx
```

#### Adapted folder structure:

- **Templates ❌** — deprecated by Next.js and Expo file-based route layouts (i.e. layout.tsx, \_layout.tsx)
- **Pages ❌** — deprecated by Next.js and Expo file-based routing (i.e. app directory)
- **Species** — feature-based directory, organizes code by domain (components, hooks, types, utils) `products`, `customers`, `orders`
- **Widgets** — standalone, smart components with internal api calls (HoC, impure functions) `NotificationsWidget`

## SOLID Principles

Five design principles for writing maintainable, extensible object-oriented code coined by Robert C. Martin (known as "Uncle Bob") in the early 2000s, building on principles he and others had written about through the 1990s.

- **Single Responsibility Principle (SRP)**: a class/module should have only one reason to change — it should do one job. E.g. a `UserService` should handle user logic, not also handle logging or email sending.
- **Open/Closed Principle (OCP)**: software entities should be open for extension but closed for modification — you should be able to add new behavior without changing existing code, typically via interfaces/abstraction or inheritance.
- **Liskov Substitution Principle (LSP)**: subtypes must be substitutable for their base types without breaking the program — if `Bird` has a `fly()` method, a `Penguin` subclass shouldn't inherit it and throw an error, since that violates expected behavior.
- **Interface Segregation Principle (ISP)**: clients shouldn't be forced to depend on interfaces they don't use — prefer several small, specific interfaces over one large general-purpose one.
- **Dependency Inversion Principle (DIP)**: high-level modules shouldn't depend on low-level modules; both should depend on abstractions (interfaces) — this decouples code and makes it easier to swap implementations (e.g. injecting a `Repository` interface instead of a concrete database class).

**Single Responsibility Principle**
```typescript
// Bad: handles both user data and email sending
class UserService {
  saveUser(user: User) { /* save to db */ }
  sendWelcomeEmail(user: User) { /* send email */ }
}

// Good: separated responsibilities
class UserService {
  saveUser(user: User) { /* save to db */ }
}

class EmailService {
  sendWelcomeEmail(user: User) { /* send email */ }
}
```

**Open/Closed Principle**
```typescript
interface Discount {
  apply(price: number): number;
}

class NoDiscount implements Discount {
  apply(price: number) { return price; }
}

class PercentageDiscount implements Discount {
  constructor(private percent: number) {}
  apply(price: number) { return price - (price * this.percent) / 100; }
}

// New discount types can be added without modifying existing code
function checkout(price: number, discount: Discount) {
  return discount.apply(price);
}
```

**Liskov Substitution Principle**
```typescript
// Bad: Penguin breaks the contract of Bird
class Bird {
  fly() { console.log("flying"); }
}
class Penguin extends Bird {
  fly() { throw new Error("can't fly"); }
}

// Good: separate capability
interface Bird {
  eat(): void;
}
interface FlyingBird extends Bird {
  fly(): void;
}
class Sparrow implements FlyingBird {
  eat() { console.log("eating"); }
  fly() { console.log("flying"); }
}
class Penguin implements Bird {
  eat() { console.log("eating"); }
}
```

**Interface Segregation Principle**
```typescript
// Bad: forces Robot to implement eat()
interface Worker {
  work(): void;
  eat(): void;
}

// Good: split into smaller interfaces
interface Workable {
  work(): void;
}
interface Eatable {
  eat(): void;
}
class Human implements Workable, Eatable {
  work() { console.log("working"); }
  eat() { console.log("eating"); }
}
class Robot implements Workable {
  work() { console.log("working"); }
}
```

**Dependency Inversion Principle**
```typescript
// Bad: high-level module depends on concrete implementation
class MySQLDatabase {
  save(data: string) { /* save to mysql */ }
}
class UserService {
  private db = new MySQLDatabase();
  saveUser(data: string) { this.db.save(data); }
}

// Good: depend on abstraction
interface Database {
  save(data: string): void;
}
class MySQLDatabase implements Database {
  save(data: string) { /* save to mysql */ }
}
class UserService {
  constructor(private db: Database) {}
  saveUser(data: string) { this.db.save(data); }
}
```