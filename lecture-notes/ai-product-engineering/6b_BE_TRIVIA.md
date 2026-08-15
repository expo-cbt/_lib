# Backend Developer Trivia

## Lifecycle

Cracking ASP.NET MVC Interviews\_ 25+ Essential Questions ANSWERED (2025 Developer Guide).mp4

- Singleton
- Scoped
- Transient

## Design Patterns

Common categories:

**Creational**

- Singleton
- Factory
- Builder

**Structural**

- Adapter
- Decorator
- Facade

**Behavioral**

- Observer
- Strategy
- Command

## CLEAN Architecture

## SOLID Principles

## Layered Architecture (N-tier) — Controller → Service → Repository → Database

## MVC (Model-View-Controller)

## CQRS (Command Query Responsibility Segregation)

**Software design patterns/principles** — reusable solutions and best practices for structuring code:

- **SOLID** — 5 principles for maintainable OOP code
- **MVC** (Model-View-Controller) — separates data, UI, and logic
- **DRY** (Don't Repeat Yourself)
- **KISS** (Keep It Simple, Stupid)
- **Singleton** — ensures only one instance of a class exists
- **Factory** — creates objects without specifying exact class
- **Observer** — objects notify others of state changes (e.g. pub/sub)
- **Dependency Injection** — supplies dependencies externally rather than hardcoding them

Common **layered architecture** pattern:

- **Controller** — handles HTTP requests/responses, routes input to services
- **Service** — contains business logic, orchestrates operations
- **Repository** — handles data access/persistence (DB queries)
- **Model/Entity** — represents data structure/schema
- **DTO** (Data Transfer Object) — shapes data passed between layers (e.g. API request/response)
- **Middleware** — cross-cutting concerns (auth, logging, validation)

**Flow**: Controller → Service → Repository → Database

Example folder structure:

```
src/
├── controllers/
├── services/
├── repositories/
├── models/
├── dtos/
└── middleware/
```

Additional layers/patterns beyond the basics:

- **Interfaces/Contracts** — define method signatures for services/repositories (enables mocking/testing)
- **Validators** — request/input validation logic (often separate from DTOs)
- **Mappers** — convert between entities and DTOs
- **Events/Listeners** — for event-driven side effects (e.g. send email on user created)
- **Jobs/Queues** — background/async task processing
- **Exceptions/Errors** — custom error classes for consistent error handling
- **Config** — environment/app configuration
- **Utils/Helpers** — shared utility functions
- **Guards/Policies** — authorization logic (who can do what)
- **Providers/Factories** — dependency instantiation and injection setup
