# Security

- **SOC 2 Type II**: an audit report verifying a company's controls over security, availability, processing integrity, confidentiality, and privacy have operated effectively over a period of time (typically 6-12 months), commonly required by SaaS/tech vendors
- **PCI DSS**: Payment Card Industry Data Security Standard — a set of security requirements for any organization that stores, processes, or transmits credit card data
- **HIPAA**: Health Insurance Portability and Accountability Act (US) — governs the privacy and security of protected health information (PHI), applies to healthcare providers, insurers, and their vendors
- **FERPA**: Family Educational Rights and Privacy Act (US) — protects the privacy of student education records, applies to schools and institutions receiving US federal funding

## SOC 2

- SOC 2: an auditing standard (Security, Availability, Processing Integrity, Confidentiality, Privacy) that verifies a company's controls over customer data are properly designed and operating.
- Immutability of audit logs: once a log entry (who/what/when/why) is written, it can never be altered or deleted, only appended to — proving the record wasn't tampered with after the fact.
- It's a **general standard**, not industry-specific.
- Developed by the AICPA (American Institute of CPAs), applicable to any service organization that stores/processes customer data — SaaS, fintech, healthcare tech, trust admin software like ProTrustee, etc.
- Only **Security** is mandatory across all 5 criteria; the other 4 (Availability, Processing Integrity, Confidentiality, Privacy) are chosen based on what's relevant to the business.
- Two types:
  - **Type I** — checks if controls are designed properly at a point in time
  - **Type II** — checks if controls actually operated effectively over a period (usually 6–12 months) — this is the one most B2B customers require
- No industry-specific version exists, but which criteria you emphasize (e.g. Confidentiality/Privacy for a company handling trust/fiduciary financial data) depends on your data sensitivity and customer expectations.

#### Implementation

SOC 2 isn't something you "implement" in code — it's an operational/compliance process. Rough path:

- Pick your scope: which Trust Services Criteria apply (Security is mandatory; add Confidentiality/Privacy given fiduciary data)
- Choose Type I (point-in-time) or Type II (6–12 month observation) — most B2B customers require Type II
- Engage a compliance platform (e.g. Vanta, Drata, Secureframe) to automate evidence collection and gap analysis
- Implement required controls: access control/MFA, encryption at rest & in transit, audit logging (like we discussed), vendor risk management, incident response plan, employee security training
- Fix gaps the platform/readiness assessment flags
- Hire a licensed CPA firm to conduct the actual SOC 2 audit
- Undergo the audit period (continuous evidence collection for Type II)
- Receive the SOC 2 report, share with customers/prospects under NDA

#### Example

Controls that map directly to what we're designing:

- **Audit logging** → the append-only `audit_log` table (Security, Processing Integrity)
- **Access control / authZ** → row-level checks so trust officers only see trusts they manage (Security, Confidentiality)
- **Encryption at rest & in transit** → Postgres encryption + TLS on all API calls (Security, Confidentiality)
- **MFA** → enforced at auth layer, not app-level DB design (Security)
- **Data retention/deletion policy** → audit_log retention period + soft-delete pattern on PII (Privacy)
- **Least-privilege DB roles** → `REVOKE UPDATE, DELETE ON audit_log` we already wrote (Security)
- **Monitoring/alerting** → logs, metrics on failed authZ attempts, anomalous access patterns (Security, Availability) — this is literally in the JD's "Monitor and operate in production" bullet
- **Incident response** → operational process, not schema, but ties to the alerting you build

Want to go deeper on authZ design (e.g. row-level security vs. app-layer checks) next, since that's a strong SOC2 + JD overlap?

## Audit Log

```sql
CREATE TABLE audit_log (
  id              BIGSERIAL PRIMARY KEY,
  trust_id        UUID NOT NULL REFERENCES trusts(id),
  entity_type     TEXT NOT NULL,        -- e.g. 'transaction', 'account'
  entity_id       UUID NOT NULL,
  action          TEXT NOT NULL,        -- 'CREATE' | 'UPDATE' | 'DELETE'
  actor_id        UUID NOT NULL REFERENCES users(id),
  reason          TEXT,
  before_state    JSONB,
  after_state     JSONB,
  created_at      TIMESTAMPTZ NOT NULL DEFAULT now()
);

-- append-only: no UPDATE/DELETE grants for app role
REVOKE UPDATE, DELETE ON audit_log FROM app_role;
GRANT INSERT, SELECT ON audit_log TO app_role;

CREATE INDEX idx_audit_entity ON audit_log (entity_type, entity_id);
CREATE INDEX idx_audit_trust ON audit_log (trust_id, created_at);
```

Corresponding TypeScript interface:

```typescript
interface AuditLogEntry {
  id: number;
  trustId: string;
  entityType: "transaction" | "account";
  entityId: string;
  action: "CREATE" | "UPDATE" | "DELETE";
  actorId: string;
  reason?: string;
  beforeState?: Record<string, unknown>;
  afterState?: Record<string, unknown>;
  createdAt: string;
}
```

So beforeState on row N = afterState on row N-1. Nothing is lost — you get the full chain by querying all rows for that entity_id, ordered by created_at.

```json
// row 1: CREATE
{ "action": "CREATE", "beforeState": null, "afterState": { "status": "PENDING", "amount": 5000 } }

// row 2: UPDATE
{ "action": "UPDATE", "beforeState": { "status": "PENDING", "amount": 5000 }, "afterState": { "status": "APPROVED", "amount": 5000 } }

// row 3: UPDATE
{ "action": "UPDATE", "beforeState": { "status": "APPROVED", "amount": 5000 }, "afterState": { "status": "PAID", "amount": 5000 } }
```

## Proctor

Here's a concise script (~2-3 min at natural speaking pace, ~350-400 words):

**Intro (15s)**
Hi, I'm [Name], a software engineer with hands-on experience building AI/ML-powered systems, most recently an exam proctoring platform for a CBT (Computer-Based Testing) exam web app.

**Problem/Context (20s)**
The core challenge: how do you ensure exam integrity remotely, without a human proctor watching every candidate live? My solution was a multi-modal AI proctoring web service.

**What I built (60-70s)**

- Location verification to confirm candidates are testing from approved/expected locations
- Live video monitoring with AI-based face detection and behavior analysis to flag suspicious movement or multiple faces
- Audio monitoring to detect background voices or conversation during the exam
- Screen-share capture to detect tab-switching, unauthorized apps, or screen anomalies
- Image/snapshot analysis at intervals for identity verification and environment checks

**Technical highlights (30-40s)**

- Integrated ML models for face detection/recognition and anomaly scoring
- Built real-time data pipelines handling video/audio streams with low latency
- Designed the system to flag violations automatically and generate a proctoring report for exam admins to review

**Impact (15-20s)**
This reduced manual review time significantly and gave exam administrators confidence in remote testing integrity at scale.

**Closing (10s)**
That's a snapshot of my AI/ML work — happy to dive deeper into any part of it.

**AI (rule-based/inference, not learned from data by you):**

- Location verification (geolocation checks against rules)
- Screen-share anomaly detection (tab-switching, app-switching rules)
- Automated flagging/report generation logic

**ML (models trained on data, pattern recognition):**

- Face detection/recognition (identity verification)
- Behavior analysis from video (movement, multiple-face detection)
- Audio analysis (voice/background noise detection)
- Image snapshot analysis (environment/identity checks)

Note: face detection and audio analysis are technically ML _applications_ — you likely used pretrained models/APIs (not trained your own), which is worth being precise about in the video if asked follow-up questions.
