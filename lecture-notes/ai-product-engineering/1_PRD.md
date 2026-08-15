# Product Requirements Document (PRD)

A Product Requirements Document (PRD) describes what the product should do and why.

It is written mainly by the **Product Manager**, and focuses on business goals, user needs, and features.

#### Outline

- Product overview
- Objectives
- Features
- User stories
- Success metrics

#### Discussion

- CBT in the AI era?
- CBT for stakeholder and student demographic?
- Go back to previous question, and why?
- Offline support, and why?
- UX constraints from past CBT experiences?
- - Practice test ✨
- - Detailed instructions
- - Timer indicator when less than 5mins left
- - Feedback after test*

# Documentation
# Documentation

> PROMPT: generate prd markdown file for basic cbt web app

## 1. Product Overview

A web-based Computer-Based Testing (CBT) application that allows administrators to create and manage exams, and students to take timed multiple-choice tests and receive results.

## 2. Goals

- Provide a simple, reliable online examination experience.
- Allow admins to manage users, questions, exams, and results.
- Automatically score objective questions.
- Enforce exam timing and submission rules.

## 3. Users

#### Admin

- Log in securely.
- Create, edit, publish, and archive exams.
- Create and manage questions and options.
- Assign exams to students.
- View student results.

#### Student

- Register/log in.
- View assigned and available exams.
- Start an exam.
- Navigate between questions.
- Select answers and submit.
- View permitted results.

## 4. Core Features

#### Authentication

- Email/username and password login.
- Role-based access: Admin or Student.
- Logout and basic password reset.

#### Exam Management

- Exam title, description, duration, instructions, status.
- Question count and pass mark.
- Draft/published/archived states.
- Exam assignment to students.

#### Question Management

- Multiple-choice questions.
- One correct answer per question.
- Question ordering.
- Optional question explanation.

#### Exam Taking

- Countdown timer.
- One question per screen or question navigation panel.
- Answer selection.
- Previous/next navigation.
- Automatic saving of answers.
- Submit confirmation.
- Automatic submission when time expires.

#### Results

- Score and percentage.
- Pass/fail status.
- Completion date/time.
- Admin result listing.
- Student result history.

## 5. Non-Goals

- Essay/manual grading.
- Live proctoring.
- Payments.
- Advanced analytics.
- Question types other than single-answer MCQ.

## 6. Key User Flow

1. Student logs in.
2. Student selects an assigned/published exam.
3. System creates an exam attempt and starts the timer.
4. Student answers questions.
5. Answers are saved during the attempt.
6. Student submits or the system auto-submits at timeout.
7. System calculates the score.
8. Result is stored and displayed according to exam settings.

## 7. Functional Requirements

- The system shall authenticate users.
- The system shall enforce role-based permissions.
- Admins shall CRUD exams and questions.
- Admins shall assign exams to students.
- Students shall only access exams available to them.
- The system shall create one attempt per permitted exam session.
- The system shall save selected answers.
- The system shall prevent submissions after an attempt expires.
- The system shall calculate objective scores automatically.
- The system shall persist results.

## 8. Success Criteria

- Students can complete an exam without losing saved answers.
- Scores are calculated correctly.
- Expired exams are automatically submitted.
- Admins can manage the complete exam lifecycle.
- Unauthorized users cannot access protected admin/student resources.

## 9. MVP Metrics

- Exam completion rate.
- Submission success rate.
- Average exam duration.
- Error/crash rate.
- Result calculation accuracy.

## 10. Assumptions

- Internet connection is required.
- Exams use single-answer multiple choice questions.
- Results are calculated immediately after submission.
