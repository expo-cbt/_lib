# Entity Relationship Diagram (ERD)

An Entity-Relationship Diagram (ERD) is a visual representation of the data in a database.

It shows entities (tables), their attributes (columns), and the relationships between them.

## Concepts of ERD

| Component                 | Symbol                   | Description                     | Example                                                  |
| ------------------------- | ------------------------ | ------------------------------- | -------------------------------------------------------- |
| Entity (Table)            | Rectangle                | A real-world object or class    | Exam, Question, Candidate                                |
| Attribute (Column, Field) | Oval                     | Properties of an entity         | Exam Duration, Question Prompt, Candidate Full Name      |
| Relationship              | Diamond                  | Link between entities           | Candidate `registers` Exam, Candidate `answers` Question |
| Primary Key (PK)          | Underlined attribute     | Uniquely identifies each record | `exam_id`, `question_id`, `candidate_id`                 |
| Foreign Key (FK)          | Attribute with FK marker | Reference to a primary key      | `question_id`                                            |
| Unique Key (UK)           | Attribute with UK marker | Reference to a unique key       | `candidate.email`                                        |

## Benefits of ERD

- Helps design databases before implementation (the Figma of database design).
- Serves as documentation for developers and database administrators.

## [Mermaid ERD](https://mermaid.ai/open-source/syntax/entityRelationshipDiagram.html)

Mermaid ERD is a way to create Entity-Relationship Diagrams using text/code with the Mermaid diagramming syntax.

#### Mermaid Relationship Notation

| Component          | Character     | Description                                                                         |
| ------------------ | ------------- | ----------------------------------------------------------------------------------- |
| One-to-One (1:1)   | `pipe`        | Each exam has exam de. Known as `extension` tables                                  |
| One-to-Many (1:M)  | `curly brace` | Each **Exam** contains several **Questions** . Known as `parent–child` tables       |
| Many-to-Many (M:N) | `lowercase o` | Several **Candidates** write several **Exams**. Known as `pivot or junction` tables |

#### Mermaid Data Types

> PROMPT: list of erd mermaid data types

- `string`
- `int`
- `float`
- `double`
- `decimal`
- `boolean`
- `date`
- `datetime`
- `timestamp`
- `time`
- `uuid`
- `binary`
- `text`
- `json`
- `enum`

## [Data Model](./3b_DATA_MODEL.md)

## [Data Flow](./3c_DATA_FLOW.md)
