Monitor the front end and server with Vercel Analytics or Sentry, and the database with Supabase's built-in reports and query tools:

- **Next.js front end**: Vercel Analytics and Speed Insights track Core Web Vitals (CWV) like page load speed and responsiveness.
- **Next.js server and errors**: Sentry provides Application Performance Monitoring (APM), error tracking, and slow API route tracing.
- **Supabase dashboard**: the Reports section shows API requests, database load, and response times.
- **Slow queries**: Supabase's Query Performance report (built on `pg_stat_statements`) shows your slowest SQL (Structured Query Language) queries.
- **Query plans**: run `EXPLAIN ANALYZE` on slow queries to find missing indexes.
- **Supabase advisors**: the Performance Advisor flags missing indexes and inefficient Row Level Security (RLS) policies.
- **End-to-end tracing**: OpenTelemetry (OTel) with Next.js's `instrumentation.ts` sends traces to tools like Datadog or Grafana.

Add "show me" to your prompt if you want the TypeScript setup code.

Use OpenTelemetry (OTel) when you need to trace requests across multiple services, or want to avoid locking into a single monitoring vendor:

- **Multiple services**: a request passes through several services (Next.js, APIs, queues, databases) and you need to see where it slows down.
- **Vendor neutrality**: you want to switch between Datadog, Grafana, or Honeycomb without rewriting instrumentation.
- **Custom metrics and spans**: you need to measure specific business operations, not just page loads.
- **Distributed debugging**: you need to follow one request end to end across microservices or serverless functions.

Skip it for a small app with one service, where Vercel Analytics and Sentry are enough.

One service means your whole app runs as a single deployable unit, like a Next.js app that talks directly to Supabase, with no other backend services, queues, or microservices in between.

With only one hop to trace, there's nothing to follow across services, so Vercel Analytics and Sentry already show you what you need.