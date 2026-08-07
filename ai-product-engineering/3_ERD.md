# Entity Relationship Diagram (ERD)

> https://mermaid.ai/open-source/syntax/entityRelationshipDiagram.html

An Entity-Relationship Diagram (ERD) is a visual representation of the data in a database.

It shows entities (tables), their attributes (columns), and the relationships between them.

#### Basic ERD Symbols

- Rectangle → Entity (Table)
- Oval → Attribute (Column)
- Diamond → Relationship
- Lines → Connect entities and relationships

#### Components of an ERD

Component; Description; Example

- Entity; A real-world object or table; Student, Employee
- Attribute; Properties of an entity; Name, Age, Salary
- Primary Key (PK); Uniquely identifies each record; Student_ID
- Foreign Key (FK); Links two tables; Course_ID
- Relationship; Association between entities; Student enrolls in Course

#### Relationship Types

```sh
|| = one (mandatory)
o| = zero or one
|{ = one or many
o{ = zero or many
```

- One-to-One (1:1 ||--||); One person has one passport.
- One-to-Many (1:M ||--o{); One department has many employees.
- Many-to-Many (M:N }o--o{); Many students enroll in many courses.
- - This is usually implemented using a `pivote table` such as Enrollment.

#### Benefits of ERD

Helps design databases before implementation.
Reduces data redundancy.
Improves data integrity.
Makes database structure easier to understand.
Serves as documentation for developers and database administrators.

#### Data Types; Example

- Integer; int, bigint, smallint
- Decimal; decimal, float, double
- Text; char, varchar, text
- Date/time; date, datetime, timestamp
- Boolean; boolean, bool
- Binary; blob, binary
- JSON; json
- UUID; uuid

## Modules

- Candidates
- Exams
- Questions

## Models

For a **bootcamp CBT exam-only system**, the models can be reduced to:

- **User** — Accounts for admins, exam creators, and exam takers.
- **Role** — Defines user permissions (owner, examiner, candidate, seeder).
- **Permission** — Defines specific actions a user can perform.
- **RolePermission (Policy)** — Defines specific actions a user can perform.
- **UserRole** — A junction model connecting users and roles.
- **Notification** — Sends exam alerts and result updates.
- **AuditLog** — Tracks system activities and changes.
- **Settings** — Stores CBT configuration settings.

---

- **Examiner** — Stores exam information such as title, duration, instructions, and status.
- **Exam** — Stores exam information such as title, duration, instructions, and status.
- **ExamQuestion (Question)** — Links questions to specific exams.
- **Candidate** — Stores exam information such as title, duration, instructions, and status.
- **CandidateAnswer (Answer)** — Stores answers submitted by candidates.
- **Result** — Stores exam outcome and final status.

This is closer to a **CBT platform** rather than a school/bootcamp management system.

## Pages

- Batch upload Seed portal - Upload excel + settings + instructions + randomize + hardware, form multipler (google forms) + image + reorder, preview, submit, manage,

- Users, rbac\*, exams settings.json, candidates, exam_questions, exam_transaction + score + json.answers like payments
