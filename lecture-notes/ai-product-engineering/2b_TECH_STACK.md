# Tech Stack, Infrastructure & Architecture

- **Technology Stack :** The programming languages, frameworks, libraries, and tools used to `build the software`.
- **Software Infrastructure :** The cloud services, servers, databases, storage, networking, monitoring, and other resources required to `run and operate the software`.
- **System Architecture :** The overall `structure of the software` and how its components communicate and interact with each other.

#### Discussion

- Tech stack, and why?
- Infrastructure, and why?
- Time estimates and budget (Ask, Offer, Deal)?

# Documentation

> PROMPT : generate tech stack, infras and architecture markdown file for basic cbt web app using react, asp.net and azure

## Technology Stack

| Component | Technology                            | Purpose                                                              |
| --------- | ------------------------------------- | -------------------------------------------------------------------- |
| Frontend  | TypeScript, React/Next.js (Hybrid\*)  | Responsive web application and UI                                    |
| Styling   | Tailwind CSS, shadcn/ui               | Rapid development of responsive and consistent interfaces            |
| Backend   | C#, ASP.NET Core Web API              | REST API, business logic, authentication, authorization, and scoring |
| Testing   | RTL + Vitest, xUnit + Moq, Playwright | Frontend, backend, integration, and end-to-end testing               |

## Software Infrastructure

| Component       | Technology                                       | Purpose                                                                          |
| --------------- | ------------------------------------------------ | -------------------------------------------------------------------------------- |
| Database        | Azure SQL Database / Azure PostgreSQL / Supabase | Relational storage for users, exams, questions, attempts, answers, and results   |
| File Storage    | Azure Blob Storage / Supabase                    | Storage for optional files/assets                                                |
| Hosting         | Azure App Service / Vercel                       | Hosting the frontend and backend where supported by the available free allowance |
| Backups         | **Azure SQL automated backups**                  | Database recovery and protection against data loss                               |
| Monitoring      | Azure Monitor, Azure App Insights                | Application logs, errors, performance, and availability monitoring               |
| Version Control | GitHub                                           | Source code management and CI/CD                                                 |

## System Architecture

```sh
 TypeScript + React/Next.js
            │
            ▼
     C# .NET Core Web API
            │
      ┌─────┴─────┐
      ▼           ▼
 PostgreSQL  Azure Blob Storage
      │
      ▼
 Azure SQL Backups

Azure Monitor + App Insights
            │
            ▼
       Monitoring
```

```sh
                    ┌─────────────────────┐
                    │      Examiner       │
                    │      Candidates     │
                    └──────────┬──────────┘
                               │
                               ▼
                 ┌────────────────────────────┐
                 │ TypeScript + React/Next.js │
                 └────────────┬───────────────┘
                              │ HTTPS / REST
                              ▼
                 ┌─────────────────────────┐
                 │   C# .NET Core Web API  │
                 ├─────────────────────────┤
                 │ Authentication          │
                 │ Authorization           │
                 │ Exam Management         │
                 │ Question Management     │
                 │ Result Processing       │
                 └───────┬─────────┬───────┘
                         │         │
               ┌─────────▼───┐   ┌─▼────────────┐
               │ PostgreSQL  │   │ Azure Blob   │
               │  Database   │   │ Storage      │
               └─────────────┘   └──────────────┘

                 ┌──────────────────┐
                 │ Azure Monitor +  │
                 │ App Insights     │
                 └──────────────────┘
```
