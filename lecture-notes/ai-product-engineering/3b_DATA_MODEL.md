# Data Model

**Domain model** — the conceptual representation of real-world concepts and their relationships in a business domain (e.g., "a Realtor has many Leads, a Lead belongs to a Property"). Focuses on _meaning_ and _rules_, not implementation.

**Entities** — the key objects/nouns within a domain model that hold identity and state (e.g., `User`, `Lead`, `Realtor`, `Property`). These are the "things" the system is built around.

**Modules** — the code/system-level groupings that organize functionality (e.g., `auth`, `lead-routing`, `notifications`). Modules often map loosely to domains but focus on _how the system is structured_, not business meaning.

**Relationship**

- Domain model → defines the concepts and rules
- Core entities → the concrete nouns extracted from that domain model
- Modules → the technical boundaries built to implement and manage those entities/behaviors

**Analogy**: Domain model = the blueprint of a house (rooms and their purpose), core entities = the actual rooms (kitchen, bedroom), modules = the construction crews responsible for building/wiring each part (plumbing team, electrical team).

## Core Modules

- Exams
- Questions
- Candidates

## Models

> PROMPT: generate list of models for basic cbt web app

#### Generic Models

| Entity            | Description                                       |
| ----------------- | ------------------------------------------------- |
| User              | User auth and account info                        |
| Role              | User types: `admin`, `examiner`, `candidate`      |
| Permission        | Permitted resource, actions, and scope (optional) |
| RolePermission    | Permissions assigned to roles                     |
| UserRole / Policy | Users assigned to roles                           |
| Setting ⏳        | App configuration                                 |
| UserSetting ⏳    | User configuration                                |
| Notification ⏳   | Notification messages                             |
| AuditLog          | Captures in-app activities                        |

#### Domain Models

| Entity                  | Description                     |
| ----------------------- | ------------------------------- |
| Exam                    | Exam details                    |
| ExamQuestion / Question | Questions assigned to exams     |
| ExamCandidate           | Candidates assigned to exams    |
| Answer                  | Answers submitted by candidates |
| Result                  | Candidates scores               |

## Mermaid ERD

> PROMPT: generate erd mermaid markdown file for basic cbt web app

```mermaid
erDiagram
    BASE {
        int id PK
        datetime created_at
        datetime updated_at
        datetime deleted_at
        uuid created_by
        uuid updated_by
        uuid deleted_by
    }

    USER {
        string photo_url
        string surname
        string other_names
        string sex
        string tel
        string email UK
        datetime email_verified_at
        string password
        datetime password_changed_at
        Address address
        Device device
        %% active | suspended
        UserStatus status
        uuid uuid
    }

    EXAM {
        uuid user_uuid FK
        string avatar_url
        string code UK
        string title
        text description
        text instructions
        int duration
        int questions
        float pass_mark
        boolean randomize
        boolean use_camera
        boolean use_microphone
        boolean use_location
        datetime exam_date
        datetime exam_time
        %% draft | published
        ExamStatus status
        uuid uuid
    }

    EXAM_QUESTION {
        uuid exam_uuid FK
        text title
        text description
        blob diagram_url
        string answer
        string option_a
        string option_b
        string option_c
        string option_d
        string option_e
        string option_f
        uuid uuid
    }

    ANSWER {
        uuid user_uuid FK
        uuid question_uuid FK
        string answer
        uuid uuid
    }

    RESULT {
        uuid user_uuid FK
        uuid exam_uuid FK
        int score
        json snapshot_url
        uuid uuid
    }

    USER ||--o{ EXAM : creates
    USER ||--o{ ANSWER : submits
    USER ||--o{ RESULT : receives
    EXAM ||--o{ EXAM_QUESTION : contains
    EXAM ||--o{ RESULT : produces
    EXAM_QUESTION ||--o{ ANSWER : has
```

#### Constraints

- ANSWER user_uuid + question_uuid should be a `Composite Unique Key (CUK)`
- RESULT record should be immutable ✅
