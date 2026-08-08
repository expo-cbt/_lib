# Software Requirements Specification (SRS)

A Software Requirements Specification (SRS) describes how the software should meet the requirements.

It is written mainly by the **System Analysts**, and focuses on technical and functional requirements.

#### Outline

- Functional requirements
- Non-functional requirements (performance, security, reliability)
- System constraints
- Interfaces
- Acceptance criteria

# Documentation

> PROMPT : generate srs markdown file for basic cbt web app

## 1. Introduction

#### 1.1 Purpose

This document defines the software requirements for a basic Computer-Based Testing web application.

#### 1.2 Scope

The system consists of authentication, exam administration, question management, exam attempts, answer recording, automatic scoring, and result reporting.

## 2. System Roles

- **Examiner:** manages exams, questions, assignments, and results.
- **Seeder:** manages exams questions only.
- **Candidate:** takes assigned exams and views permitted results.

## 3. Functional Requirements

#### FR-01 Authentication

- Users shall log in with valid credentials.
- Invalid credentials shall be rejected.
- Authenticated sessions shall be protected.
- Users shall only access resources permitted by their role.

#### FR-02 User Management

- Admins shall create, update, activate, and deactivate users.
- User roles shall be stored and enforced.

#### FR-03 Exam Management

- Admins shall create, edit, publish, archive, and delete exams where permitted.
- Each exam shall have a title, description, duration, pass mark, and status.
- Published exams shall be available only to assigned/eligible students.

#### FR-04 Question Management

- Admins shall create, edit, delete, and order questions.
- Each question shall contain a prompt and multiple options.
- Exactly one option shall be marked correct for MVP.

#### FR-05 Exam Assignment

- Admins shall assign an exam to one or more students.
- The system shall prevent unauthorized students from starting assigned exams.

#### FR-06 Exam Attempt

- The system shall create an attempt when a student starts an exam.
- The attempt shall record start time and calculated expiry time.
- The system shall save selected answers.
- The system shall allow navigation between questions.
- The system shall allow manual submission.
- The system shall automatically submit expired attempts.

#### FR-07 Scoring

- The system shall compare submitted answers with correct options.
- Score shall equal the number of correct answers.
- Percentage shall be calculated from score and total questions.
- Pass/fail shall be determined using the exam pass mark.

#### FR-08 Results

- The system shall store completed attempt results.
- Students shall be able to view results allowed by the exam configuration.
- Admins shall be able to view results for managed exams.

## 4. Non-Functional Requirements

#### NFR-01 Performance

- Normal API requests should respond within 2 seconds under expected MVP load.
- Exam answer saves should be lightweight and reliable.

#### NFR-02 Availability

- The application should recover gracefully from transient failures.
- Submitted answers must not be silently lost.

#### NFR-03 Security

- Passwords shall be securely hashed.
- Authentication shall use secure sessions/tokens.
- Authorization shall be enforced server-side.
- Inputs shall be validated and sanitized.
- Database queries shall use parameterized mechanisms/ORM protections.
- HTTPS shall be used in production.

#### NFR-04 Data Integrity

- Attempts, answers, and results shall use database transactions where appropriate.
- An attempt shall not be scored more than once.

#### NFR-05 Usability

- The interface shall be responsive on desktop and mobile browsers.
- Exam controls shall clearly show current question, answered state, and remaining time.

## 5. Validation Rules

- Exam duration must be greater than zero.
- Pass mark must be between 0 and 100.
- Published exams must contain at least one question.
- Questions must contain at least two options.
- Exactly one option must be correct.
- Students cannot modify questions or scoring data.
- Completed attempts cannot be edited.

## 6. Acceptance Criteria

- Admin can create and publish an exam with MCQ questions.
- Admin can assign the exam to a student.
- Student can start, answer, and submit the exam.
- Answers persist during the attempt.
- Timeout triggers automatic submission.
- Correct score and pass/fail status are produced.
- Admin can view completed results.

## [7. Tech Stack & Infrastructure](./2b_TECH_STACK.md)
