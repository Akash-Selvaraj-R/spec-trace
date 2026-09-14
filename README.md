# SpecTrace

> **Your README says it works. SpecTrace proves it.**

SpecTrace is an AI-powered release verification platform that traces product requirements through **code, APIs, UI, tests, and runtime behavior** to determine whether a software product actually delivers what it promises.

Instead of asking *"Does this feature exist?"*, SpecTrace asks:

**"Can we prove that this requirement is implemented, connected, tested, and working?"**

---

## The Problem

Modern software projects accumulate requirements across:

- Product specifications
- README files
- Tickets and acceptance criteria
- Frontend components
- Backend services
- APIs
- Database models
- Automated tests
- Runtime behavior

These sources frequently drift apart.

A feature may be:

- Documented but never implemented
- Implemented but not connected to the UI
- Connected but never tested
- Tested but broken at runtime
- Partially implemented while appearing complete

Traditional code analysis finds symbols and files.  
Testing verifies individual behaviors.  
Documentation describes intended behavior.

Very few tools connect all of these signals into a single **evidence-backed release decision**.

That's where SpecTrace comes in.

---

## What SpecTrace Does

SpecTrace takes two inputs:

```text
Product Specification
+
Software Repository
        ↓
   SpecTrace Agents
        ↓
Requirement Decomposition
        ↓
Code + UI + API + Test Analysis
        ↓
   Runtime Verification
        ↓
  Evidence Correlation
        ↓
     Reality Graph
        ↓
  Release Readiness
```

Every important conclusion is backed by evidence.

### Example

```text
REQ-002 — OAuth Login

Status: PARTIAL

Evidence
├── frontend/src/pages/Login.tsx
│   └── OAuth button exists
├── backend/auth/oauth.py
│   └── OAuth route implemented
├── tests/test_auth.py
│   └── No OAuth integration test
└── Runtime
    └── OAuth callback returns configuration error

Confidence: 91%
Release Impact: HIGH
```

Instead of simply saying "OAuth is incomplete", SpecTrace explains **why**.

---

## Core Features

### 1. AI Requirement Analysis

SpecTrace decomposes natural-language requirements into structured, traceable acceptance criteria.

```text
"Users should be able to reset their password"

        ↓

REQ-007
├── Reset request endpoint
├── Email/token generation
├── Token validation
├── Password update
├── Expiration handling
└── Integration test
```

### 2. Multi-Agent Software Investigation

SpecTrace uses specialized AI agents instead of a single generic prompt.

| Agent          | Responsibility                                      |
|----------------|-----------------------------------------------------|
| **Spec Agent**     | Understands the product specification and creates structured requirements |
| **Code Agent**     | Maps requirements to backend implementation, functions, classes, models, and services |
| **Frontend Agent** | Checks routes, components, forms, interactions, and frontend-to-API connectivity |
| **Test Agent**     | Determines whether requirements are covered by automated tests |
| **Runtime Agent**  | Runs safe verification commands and checks real application behavior |
| **Judge Agent**    | Synthesizes all evidence and determines requirement status, confidence, release risk, missing evidence, and recommended action |

### 3. Evidence-Backed Verification

SpecTrace does not treat an AI-generated answer as proof.

Evidence can include:

- File + line range
- Function / symbol
- Component
- API endpoint
- Test
- Command result
- Runtime response
- Build result

This makes the system **auditable** rather than merely conversational.

### 4. Reality Score

Every analyzed project receives a **Reality Score** representing how closely the actual software matches its stated requirements.

```text
71  REALITY SCORE

Implementation  82%
Integration     67%
Testing         54%
Runtime         61%
Documentation   89%
```

The score is derived from verification evidence, not a manually entered demo value.

### 5. Requirement Traceability

Each requirement receives a verification state:

| Status       | Meaning                                                        |
|--------------|----------------------------------------------------------------|
| `VERIFIED`   | Requirement is implemented and supported by evidence           |
| `IMPLEMENTED`| Implementation exists but complete verification is unavailable |
| `PARTIAL`    | Only part of the requirement is satisfied                      |
| `MISSING`    | No meaningful implementation was found                         |
| `UNVERIFIED` | Evidence is insufficient                                       |
| `BLOCKED`    | Verification could not safely complete                         |

### 6. Reality Graph

SpecTrace converts the investigation into a visual dependency graph.

```text
Requirement
│
├── implements ──→ Function
├── renders ─────→ Component
├── calls ───────→ API
├── tests ───────→ Test
└── verifies ────→ Runtime Check
```

The graph makes it possible to visually trace:

**Promise → Implementation → Integration → Test → Runtime**

### 7. Release Readiness

SpecTrace answers the question engineering teams actually care about:

> **Can we ship this?**

```text
REALITY SCORE        71%
CRITICAL BLOCKERS     2
HIGH RISKS            4
PARTIAL               7
VERIFIED              9

RELEASE STATUS
NOT READY
```

Instead of forcing engineers to manually inspect dozens of files, SpecTrace provides a single evidence-backed release decision.

### 8. Autonomous Fix Loop

SpecTrace can go beyond detection.

When safe remediation is possible:

```text
Detect
  ↓
Explain
  ↓
Generate Fix Plan
  ↓
Execute Safe Fix
  ↓
Run Tests
  ↓
Build
  ↓
Re-scan
  ↓
Prove Improvement
```

Example:

```text
BEFORE                    AFTER
Reality Score 71%   →    Reality Score 94%
Critical Blocks 2   →    Critical Blocks 0
```

The goal is not merely to identify problems.  
**The goal is to prove that the problems were actually fixed.**

---

## Architecture

```text
┌─────────────────────────────────────────────┐
│               React Client                  │
│  Landing · Dashboard · Investigation        │
│  Requirements · Reality Graph · Release     │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│                  FastAPI                    │
│  Project Ingestion · Requirement Processing │
│  Agent Orchestration · Evidence Engine      │
│  Scoring · Graph Construction               │
│  Runtime Verification · Remediation         │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│                Agent System                 │
│  Spec → Code → Frontend → Test → Runtime    │
│                    ↓                        │
│                  Judge                      │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│              Evidence Layer                 │
│  Files · Symbols · APIs · Tests · Runtime   │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
                 Reality Graph
                       │
                       ▼
               Release Decision
```

---

## Tech Stack

### Frontend
- React
- TypeScript
- Vite
- Tailwind CSS
- Framer Motion
- React Flow
- Lucide Icons

### Backend
- Python
- FastAPI
- Pydantic
- SQLAlchemy
- Uvicorn

### AI
SpecTrace uses a provider-agnostic agent architecture so the reasoning layer can be adapted to different AI providers and models.

AI is used for:
- Requirement decomposition
- Semantic code mapping
- Evidence interpretation
- Missing-feature detection
- Risk analysis
- Remediation planning

Deterministic logic is used where reliability matters:
- Scoring
- Schema validation
- Evidence aggregation
- Graph construction
- File indexing
- Command safety
- Verification orchestration

This hybrid architecture reduces the risk of letting an LLM arbitrarily determine the final system state.

---

## Security

Software repositories are treated as **untrusted input**.

SpecTrace's verification workflow is designed around controlled execution.

Safety principles include:
- Command allowlisting
- Path sanitization
- Directory traversal prevention
- No destructive commands
- No credential extraction
- No arbitrary secret exfiltration
- Controlled runtime verification
- Separation between analysis and execution

The system never treats repository-provided instructions as trusted system instructions.

---

## Example Investigation

Consider a SaaS project with these requirements:

```text
REQ-001  User Authentication
REQ-002  OAuth Login
REQ-003  Password Reset
REQ-004  Role-Based Access
REQ-005  User Profile
REQ-006  Notifications
REQ-007  CSV Export
REQ-008  Audit Logging
REQ-009  Rate Limiting
REQ-010  Email Verification
```

SpecTrace investigates each requirement independently.

Example result:

```text
REQ-001  Authentication       VERIFIED
REQ-002  OAuth Login          PARTIAL
REQ-003  Password Reset       MISSING
REQ-004  RBAC                 VERIFIED
REQ-005  User Profile         VERIFIED
REQ-006  Notifications        PARTIAL
REQ-007  CSV Export           VERIFIED
REQ-008  Audit Logging        MISSING
REQ-009  Rate Limiting        UNVERIFIED
REQ-010  Email Verification   PARTIAL
```

The resulting graph and evidence allow an engineer to drill directly from a requirement into the implementation and verification evidence.

---

## Project Structure

```text
spec-trace/
├── backend/
│   ├── app/
│   │   ├── agents/
│   │   ├── models/
│   │   ├── routers/
│   │   ├── services/
│   │   └── utils/
│   └── ...
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── lib/
│   │   └── types/
│   └── ...
├── demo-project/
│   └── TaskFlow/
└── README.md
```

---

## Getting Started

### Prerequisites
- Node.js
- Python 3.11+
- npm / pnpm
- Git

### Clone

```bash
git clone https://github.com/Akash-Selvaraj-R/spec-trace.git
cd spec-trace
```

### Backend

```bash
cd backend
python -m venv .venv
```

**Windows**
```bash
.venv\Scripts\activate
```

**macOS / Linux**
```bash
source .venv/bin/activate
```

```bash
pip install -r requirements.txt
python -m uvicorn app.main:app --reload
```

### Frontend

Open another terminal:

```bash
cd frontend
npm install
npm run dev
```

The development server will provide the local application URL.

---

## Demo Project

SpecTrace includes an intentionally imperfect SaaS demo project designed to demonstrate requirement drift.

The demo contains a mixture of:
- Correct implementations
- Partial implementations
- Missing features
- Broken integrations
- Missing tests
- Runtime failures

This allows the verification engine to demonstrate a realistic investigation instead of analyzing an artificially perfect application.

---

## Product Flow

```text
PROMISE → TRACE → VERIFY → PROVE
```

| Stage    | Description                                      |
|----------|--------------------------------------------------|
| **PROMISE** | Define what the software claims to do          |
| **TRACE**   | Map each promise through the repository        |
| **VERIFY**  | Check implementation, integration, tests, and runtime behavior |
| **PROVE**   | Generate evidence-backed release confidence    |

---

## Why SpecTrace?

Most AI coding tools focus on:

> **"How do I build this?"**

SpecTrace focuses on:

> **"Did we actually build what we said we built?"**

That distinction matters.

Software organizations continuously deal with:
- Requirement drift
- Documentation drift
- Missing tests
- Broken integrations
- Incomplete implementations
- False confidence before release

SpecTrace turns these problems into a measurable verification workflow.

---

## What Makes It Different

| Aspect                    | SpecTrace Advantage                                      |
|---------------------------|----------------------------------------------------------|
| **Not just a code scanner**   | Connects requirements to actual engineering evidence   |
| **Not just an AI chatbot**    | Performs structured investigation instead of conversational guesses |
| **Not just test coverage**    | A passing test does not prove the entire requirement is satisfied |
| **Not just RAG**              | Builds relationships between requirements, code, UI, APIs, tests, and runtime |
| **Not just detection**        | Autonomous fix loop can remediate safe issues and re-verify the result |

---

## Design Philosophy

SpecTrace follows an intentionally restrained visual language:

```text
BLACK
WHITE
ONE ACID-GREEN ACCENT

THIN LINES
HUGE TYPOGRAPHY
TECHNICAL DETAILS
NEGATIVE SPACE
EVIDENCE FIRST
```

The interface is designed to feel closer to an engineering verification system than a conventional AI dashboard.

---

## Hackathon

Built for the **AI Builders Hackathon 2026**.

**Focus:** AI-powered software engineering and autonomous verification.

| Criterion                  | SpecTrace                                              |
|----------------------------|--------------------------------------------------------|
| Innovation                 | Requirement-to-runtime verification + Reality Graph    |
| Technical Implementation   | Multi-agent investigation + evidence engine            |
| Problem Solving & Impact   | Addresses software/release confidence                  |
| UX / Design                | Editorial industrial verification interface            |
| Presentation               | Clear investigation → proof → remediation story        |

---

## Demo Story

The intended product demonstration follows a simple question:

```text
"Can we actually ship this?"
```

```text
Analyze Project
      ↓
Agents Investigate
      ↓
Reality Score
      ↓
Critical Requirement
      ↓
Evidence
      ↓
Reality Graph
      ↓
Fix Plan
      ↓
Safe Fix
      ↓
Tests + Build
      ↓
Re-scan
      ↓
Prove Improvement
```

Final message:

> **SpecTrace doesn't ask whether your software works.**  
> **It proves it.**

---

## Status

🚧 **Hackathon Build — AI Builders Hackathon 2026**

The project is actively being developed and refined for the hackathon submission.

---

## License ✅

MIT License

---

## Author

**Akash Selvaraj R**
