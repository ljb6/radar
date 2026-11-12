# Project Overview

> Built for **Hack Brasil 2026**, in the **Payments & finance** track. The product has no name yet.
> Starting document for spec-driven development (SDD). Version 0.3, 2026-11-12 (hackathon rules checked against the official rules).
>
> Terminology: a *call* (Portuguese: *edital*) is a public funding announcement: a grant, credit line, scholarship, prize or acceleration program with its own eligibility rules and deadline.

---

## How to use this document

This file is the source of truth for the **why** and the **what** of the project. Each feature spec derives from it and must not contradict it. If a spec needs to change something here, update this file first.

Proposed SDD flow for each feature:

1. **Requirements:** user stories and verifiable acceptance criteria.
2. **Design:** how it will be built (components, data, interfaces).
3. **Tasks:** small, ordered steps, each tied to an acceptance criterion.
4. **Implementation and validation:** a task is only closed when its criterion passes.

Markers used in the text:

- **[DECIDED]**: already settled.
- **[PROPOSAL]**: initial suggestion, may change.
- **[OPEN]**: needs a decision (listed in section 15).

Suggested folder structure:

```
docs/
├── foundation.md          ← this file
├── specs/
│   ├── F1-collection/
│   │   ├── requirements.md
│   │   ├── design.md
│   │   └── tasks.md
│   ├── F2-extraction/
│   └── ...
└── decisions/             ← short records of technical decisions (ADRs)
```

---

## 1. Context: Hack Brasil 2026

> Rules checked against the official rules (hackbrasil.com/regulamento) on 2026-11-12. Numbers in parentheses are rule item numbers.

| Item | Detail |
|---|---|
| Online phase | From the end of the opening session (Nov 4, 9pm) to Nov 30 |
| Submission | Until Nov 30, 11:59pm. This is also the last commit that is evaluated |
| Finalists | Announced Dec 2; attendance confirmation until Dec 4, 11:59pm |
| In-person final | Dec 12, in São Paulo, with winners announced |
| Teams | 1 to 4 people; each person can only be on one team. This project is a solo team [DECIDED] |
| Tools | **Free choice.** No sponsor tool is mandatory (6.3) |
| Judging criteria (9) | Four equally weighted criteria, each scored 0 to 10: technical execution; technical implementation (architecture, code quality, use of technologies); impact on the problem and the track's audience; quality of communication (video and final presentation). In the online phase, a project needs at least 20 of 40 points to reach the final |
| Track | **Payments & finance** [DECIDED] |

Even though no tool is mandatory, the project uses Firecrawl (collection) and Resend (email) because they are part of the product. Tools only count toward the technical implementation criterion, with the same weight for any of them.

**Deliverables (7.2)**

- Name, tagline and project description.
- Chosen track.
- Link to each GitHub repository.
- Link to a working demo, which must stay online for the whole evaluation (7.3).
- Link to a video of up to 3 minutes, accessible without login, showing the product working.
- Acceptance of the rules.

**Rules that affect the project**

- **New repository (6.1):** public on GitHub and created after Nov 4, 9pm. All event code must be in it. A prior repository, a fork or imported history means disqualification. Continuing an existing idea is allowed, but copying earlier code that was not public is not (6.2).
- **Visibility (6.7) and freeze (8.4):** the repository stays public until at least Dec 15. Between the submission and the final it is frozen, and commits in that period can lead to disqualification.
- **License (6.6):** open source is recommended. A license that prevents judges from reading, running or testing the code means disqualification.
- **AI (6.4):** allowed and encouraged.
- **Prohibited themes (6.8):** adult content, illegal substances, weapons and violence, harassment and hate, malware and academic fraud, gambling and financial schemes. The project touches none of them.
- **Real data (6.9):** the demo must not expose real personal data of third parties, and finance projects use test or simulated environments. Note: the legal name of a MEI (Brazilian individual micro-entrepreneur) often contains the owner's name, so the demo should use the CNPJ (Brazilian company tax ID) of a company that is not a MEI, or fictional data.
- **Sponsor credits and prizes (10.3):** Firecrawl gives credits to the top 3 and to members of approved drafts (up to 2,000 people). Resend gives US$ 10k in credits to the top 3 teams and 3 months of the Pro plan to each finalist team. Devin gives a US$ 20 coupon to each member of an approved draft. No prize requires using the sponsor's product (10.4).
- **Credits form:** has 3 steps, starting with "initial draft" and "organizer review". Idea, links and track can change until the deadline; each change goes back to review, and credits already released remain valid.

**Official description of the Payments & finance track:** projects about how people and companies pay, receive, save and invest money. Examples: payment infrastructure, trading bots, financial agents, personal and small-business financial management, and access to credit. Out of scope: gambling, casinos and games of chance; guaranteed-return promises and pyramid schemes; market manipulation; and issuing tokens or crypto-assets to raise money from the public.

**How the project fits:** it is a financial agent that finds money (credit and innovation grants) for small companies. In the pitch, say "access to financing for SMEs", not "funding call search". Include credit lines (Finep, BNDES) among the sources from the start and show amounts in reais (BRL) in the demo.

---

## 2. Project principles

Rules that apply to every spec:

1. **Traceability:** every piece of data shown or emailed links to its original source.
2. **Eligibility is "likely", never a verdict:** the product explains why the company seems to fit and what is still left to check.
3. **Public data only:** public calls and public CNPJ registry data. Respect robots.txt and each site's terms, and space out requests. In the demo, no real personal data of third parties (rules, 6.9).
4. **Demo first:** when in doubt about scope, prioritize what shows up in the video (up to 3 minutes) and in the demo.
5. **Quality over coverage:** a few well-extracted sources are worth more than many badly extracted ones.
6. **Email with consent:** only send to people who signed up, and every email has an unsubscribe link.
7. **Language** [DECIDED]: code, field names, docs and specs are in English. Everything the user sees (web interface, emails, error messages) is in Brazilian Portuguese.

---

## 3. Problem

Small companies and startups miss out on credit and non-reimbursable innovation funding because:

- calls are scattered across dozens of sites (Finep, BNDES, CNPq, 27 state research foundations known as FAPs, Sebrae, corporate programs), with no central place and no standard alert system;
- eligibility, amounts and deadlines are buried in long PDFs;
- calls get corrections and extensions that go unnoticed;
- monitoring today is manual. Sebrae, Firjan, Findes and state governments publish newsletters and dashboards of calls assembled by hand. This proves the demand exists and shows that nobody has solved the problem in an automatic, personalized way.

---

## 4. Solution

The product monitors funding and credit sources for innovation every day. It extracts each call's data with AI (amount, deadline, eligibility, counterpart) and matches it against the company's profile, built from its CNPJ. The company receives by email the compatible calls, with an explanation of the fit, alerts for new opportunities, deadline reminders and correction notices. When a source changes layout and the extractor breaks, Devin (or another tool) can be triggered to fix the code, if time allows.

**Pitch line:** "Every week, money for innovation opens up in Brazil that small companies never hear about. We find it, filter it and alert them."

---

## 5. Users

| Persona | Role | What they need |
|---|---|---|
| Startup founder or owner of an innovative SME | Main MVP user | To know, effortlessly, which open calls fit their company and until when |
| Grant-writing consultant | B2B buyer (post-hackathon) | To track opportunities for several clients at once |
| Manager of an incubator, accelerator or NIT (university technology transfer office) | B2B buyer (post-hackathon) | To distribute relevant opportunities to portfolio companies |

The MVP serves the founder. Consultants and incubators appear in the pitch as the business model.

---

## 6. MVP scope (until Nov 30)

### Features

| ID | Feature | Partner tool | Priority |
|---|---|---|---|
| F1 | Daily collection and detection of new calls | Firecrawl | Required |
| F2 | Structured extraction and validation of calls | Firecrawl (JSON and PDF) | Required |
| F3 | Company signup by CNPJ | — | Required |
| F4 | Matching with fit explanation | — | Required |
| F5 | Emails: welcome with matches, new-call alert, weekly digest, deadline reminder | Resend | Required |
| F6 | Tracking of open calls (corrections, extensions) | Firecrawl (change tracking) and Resend | High |
| F7 | Self-repair of broken extractors | Devin or another tool | Optional, only if time allows |
| F8 | Minimal web interface: signup, list of compatible calls, call detail | — | Required |

### Out of scope

- Public tenders and procurement: crowded market (Effecti, ConLicitação, Licitei, Settle).
- Cultural and social incentive laws: already served by, for example, AprovAI.
- Writing or submitting proposals.
- Covering every FAP and source in the country.
- Mobile app, billing and subscriptions.

---

## 7. Functional requirements (high level)

The criteria below are the starting point for each feature's spec.

**F1: Collection and detection**

- As the system, I want to check sources every day to discover new calls.
- WHEN the daily collection runs, the system SHALL fetch the listing page of every active source.
- WHEN the listing has not changed since the last collection, the system SHALL NOT reprocess the source.
- WHEN a call URL appears that is not in the database, the system SHALL send it to extraction.
- The system SHALL log each run per source (start, end, calls found, errors).

**F2: Extraction and validation**

- WHEN a new call is found, the system SHALL extract the fields of the Call schema (section 10) from the page and, if needed, from the PDF.
- IF the extraction fails schema validation, the system SHALL mark the call as `pending_review` and log the error.
- The system SHALL store the raw markdown of the page and the PDF, so it can reprocess without collecting again.

**F3: Signup by CNPJ**

- As a founder, I want to enter just the CNPJ and a short description, without filling in a long form.
- WHEN the user enters a valid CNPJ, the system SHALL automatically fill in legal name, CNAE (Brazilian industry classification code), company size, state (UF) and opening date.
- The user SHALL be able to add a company description and areas of activity.

**F4: Matching**

- As a founder, I want to see only the calls I probably fit and understand why.
- The system SHALL apply eliminatory filters: coverage (state), company size, applicant type, company age and call open.
- The system SHALL rank the remaining calls by fit with the profile.
- Each match SHALL show the reason for the fit, what is left to check (for example, counterpart funding or partnership with a research institution), the deadline and the source link.

**F5: Emails (Resend)**

- WHEN the company completes signup, the system SHALL send an email with the compatible open calls.
- WHEN a new compatible call is extracted, the system SHALL send an alert.
- The system SHALL send reminders 14 and 3 days before the deadline of compatible calls.
- Every email SHALL have an unsubscribe link.

**F6: Tracking of open calls**

- WHEN the deadline, status or amount of an open call changes, the system SHALL update the record and notify compatible companies.
- Closed calls SHALL leave monitoring.

**F7: Self-repair (Devin or another tool), optional**

- IF a source that used to have calls returns zero, or its extractions repeatedly fail validation, the system SHALL open a session in the repair tool with the failure context.
- The fix SHALL arrive as a pull request for human review, never directly in production.

**F8: Web interface**

- Minimal screens: signup (CNPJ, description and email), list of compatible calls and call detail.
- No authentication in the demo [DECIDED]. The signup email identifies the company.

---

## 8. Non-functional requirements

- Collection at least daily on every active source.
- Firecrawl credit usage under control: basic change tracking on the listing, JSON extraction only on new calls, and JSON monitoring only on open calls.
- Idempotent processing: running the collection twice does not duplicate calls or emails.
- Logs per source and per run, for debugging and, if F7 exists, to trigger the repair tool.
- Minimal personal data: only the user's email and the public CNPJ data.

---

## 9. Architecture [PROPOSAL]

```
 scheduler (daily cron)
        │
        ▼
 ┌──────────────┐  listing + change tracking    ┌───────────┐
 │  Collector   │ ─────────────────────────────▶│ Firecrawl │
 │  (F1)        │◀───────────────────────────── │           │
 └──────┬───────┘        new URLs               └───────────┘
        ▼
 ┌──────────────┐  JSON scrape (page/PDF)
 │  Extractor   │ ─────────────▶ Firecrawl
 │  + validation│
 │  (F2)        │── repeated failure ──▶ Fixer (F7, optional) ──▶ repair tool ──▶ PR
 └──────┬───────┘
        ▼
 ┌──────────────────────┐        ┌───────────────────┐
 │ Database (Postgres + │◀──────▶│ Matching (F4)     │◀── company profile (F3, BrasilAPI)
 │ pgvector)            │        └─────────┬─────────┘
 └──────────────────────┘                  ▼
                                Notifier (F5/F6) ──▶ Resend ──▶ email
                                           ▲
                           Web interface (F8) ┘
```

**Stack** [DECIDED]: Python on the backend and workers (FastAPI and Pydantic); Next.js with TypeScript on the frontend. Database: Postgres with pgvector [PROPOSAL]. Hosting is still [OPEN] and must support a daily cron.

**Extraction** [DECIDED]: initially only Firecrawl's JSON extraction. A custom LLM over the markdown is only considered if extraction quality is not good enough.

### Firecrawl

| Feature | Use in the project |
|---|---|
| `/scrape` with `changeTracking` | Detect whether the listing page changed (status `new`, `same`, `changed` or `removed`). Basic mode has no extra cost |
| `/scrape` with `links` format | Get the call URLs from the listing and compare them with saved URLs |
| `/scrape` with JSON format and schema | Extract the call fields from the page |
| PDF `parsers` (modes `fast`, `auto` or `ocr`, with `maxPages`) | Read the call PDF, limiting page count to control cost |
| `/map` with text filter | Discover call URLs on sites without a good listing page |
| `changeTracking` in JSON mode | Monitor deadline, status and amount of open calls (5 credits per page) |
| `/search` (optional) | Discover corporate challenges outside the source list |

### Resend

Transactional emails: welcome with matches, new-call alert, weekly digest, deadline reminder and correction notice. Simple templates, in Brazilian Portuguese, linking to the call detail and to the source.

### Self-repair tool (optional)

Neither the rules (6.3) nor the project require Devin, and its sponsorship is a US$ 20 coupon per approved-draft member (10.3). So F7 is off the main path [DECIDED]. It only comes in if the main flow (F1 to F5 and F8) is done and time remains, using Devin or another tool:

- **During development:** if wanted, use the coupon to have Devin write source adapters.
- **In the product:** the fixer creates a session through Devin's v3 API (`POST /v3/organizations/{org_id}/sessions`, authenticated with a `cog_` service-user key), sending the source, the error, a markdown sample and the expected schema, and Devin opens a PR fixing the extractor. First, check whether the coupon gives API access.

---

## 10. Data model [PROPOSAL]

**Call**

| Field | Description |
|---|---|
| `id`, `source_id`, `url`, `title`, `agency` | Identification |
| `funding_type` | `grant`, `credit`, `scholarship`, `prize` or `acceleration` |
| `min_amount`, `max_amount`, `counterpart_pct` | Amounts |
| `applicants` | List: `startup`, `micro_small`, `medium`, `research_institution`, `researcher` |
| `coverage` | List of states (UFs) or `national` |
| `max_company_age_years` | When applicable |
| `topics` | List of thematic areas |
| `requires_research_partner` | Boolean |
| `opening_date`, `submission_deadline`, `stages` | Schedule |
| `documents`, `submission_link` | Submission |
| `summary` | Short text generated at extraction |
| `raw_markdown`, `content_hash` | Reprocessing and change detection |
| `status` | `open`, `closed` or `pending_review` |
| `embedding` | Vector for semantic matching |

**Other entities**

- **Source:** listing URL, adapter, active (yes or no), last run.
- **Company:** CNPJ, legal name, CNAE, size, state, opening date, description, topics, email, embedding.
- **Match:** company, call, score, fit reason, open items.
- **Notification:** type, company, call, sent date, Resend message id.
- **CollectionRun:** source, start, end, calls found, errors.

---

## 11. Initial sources [PROPOSAL]

| Source | Funding type | Listing page | Priority |
|---|---|---|---|
| Finep | Grants and credit | finep.gov.br/chamadas-publicas | 1 (spike) |
| BNDES | Credit and programs | To be mapped | 1 (spike) |
| FAPERGS | Grants (RS) | To be mapped | 1 (spike) |
| CNPq | Calls and scholarships | To be mapped | 2 |
| FAPESP (PIPE) | Grants (SP) | To be mapped | 2 |
| EMBRAPII | R&D co-financing | To be mapped | 2 |
| Sebrae | Programs and calls | To be mapped | 2 |
| Innovation for Industry platform (SESI/SENAI) | Calls | To be mapped | 2 |
| FAPEMIG, FAPERJ, FACEPE | State grants | To be mapped | 3 |

The spike on the three priority-1 sources measures extraction quality before the rest is built.

---

## 12. Video script (up to 3 minutes)

The video is a required deliverable and counts toward the communication criterion. It must be accessible without login. The live demo must stay online for the whole evaluation.

1. The problem in one sentence, with a manual newsletter on screen as proof.
2. The person types a CNPJ and the profile fills itself in.
3. The compatible open calls appear, with the total potential amount, the reason for each fit and the open items.
4. The welcome email arrives live (Resend).
5. Only if F7 exists: an extractor breaks and the repair tool opens the PR that fixes it.
6. Closing: business model and next steps.

---

## 13. Market, competition and business model

**Competition in Brazil**

- **Public tenders:** crowded and funded market. Effecti covers over 1,400 portals, Licitei raised R$ 3.5 million and Settle raised US$ 3.08 million in pre-seed. Out of scope, but useful in the pitch: it shows the "AI structuring public announcements" thesis attracts capital.
- **Incentive laws:** AprovAI (Brada) helps draft projects and also finds compatible calls.
- **Innovation funding:** only manual newsletters and dashboards (Sebrae, Firjan's "Radar de Recursos", Findes' Capta360 with over 120 initiatives, Goiás' Radar de Editais). We found no automatic tool with company-profile matching. This still needs better validation.

**International reference:** Instrumentl (US) matches grants for nonprofits, with plans from US$ 179 to US$ 499 per month and over 20,000 active grants. It serves nonprofits, consultants and proposal writers, the same kind of B2B buyer as this project.

**Business model** [PROPOSAL]

- Free for startups: weekly digest and alerts.
- Paid for grant-writing consultancies, incubators and NITs: dashboard with multiple clients or with portfolio companies.
- Future: proposal assistant and success fee.

---

## 14. Risks

| Risk | Mitigation |
|---|---|
| PDFs with tables and attachments hurt extraction | Extract only key fields, limit pages, always show the source link and use the `pending_review` status |
| Ambiguous eligibility rules | Present as "likely", with reasons and open items |
| Slow or unstable sites (gov.br) | Generous timeouts, retries and asynchronous collection |
| Credit cost | Basic change tracking on the listing; JSON only where needed |
| Demo offline during evaluation (7.3) | Stable, simple deploy with basic monitoring |
| Exposing real personal data in the demo (6.9) | Use the CNPJ of a non-MEI company, or fictional data |
| Large scope for a solo developer in the time available | Prioritize F1 to F5 and F8; F6 and F7 only after the main flow works |

---

## 15. Open questions

1. Where to host the project (must support a daily cron)?
2. What is the product's final name?

**Decided in this version:** solo project (no team section needed); stack is Python (backend) and Next.js with TypeScript (frontend); extraction starts with Firecrawl JSON only; no authentication in the demo for now; Devin (or another tool) only if time remains; code and docs in English, user-facing text in Brazilian Portuguese.

---

## 16. References

**Hackathon**
- [Hack Brasil 2026 rules](https://hackbrasil.com/regulamento)

**Problem and demand**
- [Funding calls: where to find them (fragmentation, lack of alerts)](https://www.doutoranathalia.com.br/blog/editais-de-fomento-onde-encontrar-e-como-concorrer/)
- [Funding Calls and Actions Newsletter, Sebrae CE (Jan 2026)](https://sebrae.com.br/Sebrae/Portal%20Sebrae/UFs/CE/Anexos/Boletim%20de%20inova%C3%A7%C3%A3o%20-%20Janeiro%202026.pdf)
- [Portal da Indústria: Capta360 (Findes) and Radar de Recursos (Firjan)](https://noticias.portaldaindustria.com.br/noticias/inovacao-e-tecnologia/quer-inovar-plataformas-do-sistema-industria-mostram-os-recursos-disponiveis-para-inovacao/)
- [Radar de Editais, State of Goiás](https://goias.gov.br/inovacao/radar-de-editais/)

**Competition**
- [Effecti](https://effecti.com.br/?p=409)
- [Licitei raises R$ 3.5 million (Startupi)](https://startupi.com.br/?p=248204)
- [Settle (Bloomberg Línea)](https://www.bloomberglinea.com.br/startups/settle-usa-agentes-de-ia-para-destravar-mercado-de-licitacoes-publicas-de-r-1-tri/)
- [AprovAI, by Brada (Startupi)](https://startupi.com.br/?p=247956)
- [Instrumentl (Software Advice)](https://www.softwareadvice.com/nonprofit/instrumentl-profile/)
- [Instrumentl: plans and pricing (battle card)](https://instrumentl.notion.site/GrantHub-Pro-b90e67a9eccc4ccd8e2a9862cb52dc58)

**Technical documentation**
- [Firecrawl: Advanced Scraping Guide](https://docs.firecrawl.dev/advanced-scraping-guide.md)
- [Firecrawl: Change Tracking](https://docs.firecrawl.dev/features/change-tracking)
- [Devin API v3: usage examples](https://docs.devin.ai/api-reference/v3/usage-examples.md)
