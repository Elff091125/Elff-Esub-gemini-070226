Medical Device Regulatory Intelligence Workspace — Comprehensive Technical Specification (Enhanced Design)

**Version:** 3.0.0 (HF Spaces / Streamlit Edition)  
**Document Type:** Technical Specification (No Code)  
**Target Users:** Regulatory Affairs (RA), QA/QMS, R&D engineers, clinical/regulatory writers  
**Primary Jurisdictions:** US FDA 510(k) eSTAR & Taiwan TFDA 查驗登記 (Class II focus)  
**Standards Alignment:** 21 CFR Part 11, 21 CFR Part 820, ISO 13485, ISO 14971, ISO 10993, ISO 14155, IEC 62304, ASTM F1541  
**Default LLM Model:** `gemini-3.1-flash-lite` (user-selectable overrides supported)

---

## Table of Contents

1. [Product Intent & Non-Negotiable Principles](#1-product-intent--non-negotiable-principles)  
2. [Scope: “Keep All Original Features” + New Feature Additions](#2-scope-keep-all-original-features--new-feature-additions)  
3. [Deployment Architecture (Hugging Face Spaces + Streamlit)](#3-deployment-architecture-hugging-face-spaces--streamlit)  
4. [LLM & Agent Orchestration (Model Router + agents.yaml)](#4-llm--agent-orchestration-model-router--agentsyaml)  
5. [Core Workflow Modules (Original 4-Stage Workshop Preserved)](#5-core-workflow-modules-original-4-stage-workshop-preserved)  
6. [New Module A — Skill.md Studio (Upload/Edit/Agent-Apply)](#6-new-module-a--skillmd-studio-uploadeditagent-apply)  
7. [New Module B — Notes-to-Organized Markdown + OCR + AI Magics](#7-new-module-b--notes-to-organized-markdown--ocr--ai-magics)  
8. [WOW LLM Execution Visualization + Live Logs + Interactive Indicators](#8-wow-llm-execution-visualization--live-logs--interactive-indicators)  
9. [Interactive Dashboard (5 WOW Graphs)](#9-interactive-dashboard-5-wow-graphs)  
10. [UI/UX System: i18n, Themes, 10 Pantone-Based Styles](#10-uiux-system-i18n-themes-10-pantone-based-styles)  
11. [Security, Privacy, 21 CFR Part 11, and Audit Trails](#11-security-privacy-21-cfr-part-11-and-audit-trails)  
12. [Data Models, Storage Strategy, and Export Packages](#12-data-models-storage-strategy-and-export-packages)  
13. [Reliability Engineering: Bug Fixes, Failure Modes, and Mitigations](#13-reliability-engineering-bug-fixes-failure-modes-and-mitigations)  
14. [Testing & Validation Plan (Regulated-Grade)](#14-testing--validation-plan-regulated-grade)  
15. [Additional WOW AI Features (3 New)](#15-additional-wow-ai-features-3-new)  
16. [Appendix: 20 Comprehensive Follow-Up Questions](#appendix-20-comprehensive-follow-up-questions)

---

## 1. Product Intent & Non-Negotiable Principles

This workspace is a **professional-grade regulatory intelligence workbench** that converts unstructured regulatory guidance + internal technical evidence into:

- A **bilingual** (Traditional Chinese / English) compliance checklist matrix  
- Automated gap analysis aligned with FDA eSTAR and TFDA technical file expectations  
- A traceable, hash-verifiable report with **Part 11-aligned** signature records  
- A repeatable workflow suitable for internal QA audits and submission readiness reviews  

### 1.1 Architectural Honesty (No Cosmetic “Fake” UI)
All “wow” effects must be **informationally honest**:
- Visualizations must reflect real token streaming, tool steps, timing, and evidence extraction events.
- Indicators must map to actual state transitions (queued → running → validating → complete/failed).
- Logs must be actionable and exportable.

### 1.2 Regulated-Grade Constraints
- Determinism where needed (IDs, audit trail consistency, reproducible exports)
- Strong schema validation for structured outputs (checklists, audit results)
- Clear separation of user content, model outputs, and system metadata
- Safe handling of secrets (API keys never echoed)

---

## 2. Scope: “Keep All Original Features” + New Feature Additions

### 2.1 Original Features Preserved (from v2.0 spec)
The following core features remain intact and are functionally equivalent:

1. **4-Stage Compliance Checklist Workshop**
   - Guidance ingestion and structuring  
   - Interactive checklist grid editing & import/export (CSV/JSON/MD/TXT)  
   - Submission transformation + automated audit against checklist  
   - Executive compliance summary generation + signature hashing  

2. **AI-powered Regulatory Intelligence**
   - Checklist generation from guidance
   - Audit engine: status updates (符合/待補/不適用) with rationale
   - Report synthesis and bilingual output options

3. **21 CFR Part 11-aligned hashing + signature ledger + verification**
   - Document hash (SHA-256)  
   - Signature hash (SHA-256 over signer metadata + document hash)  
   - Verification console and tamper detection workflow  

4. **Audit trails**
   - Timestamped system activities
   - Exportable logs

5. **Existing “Wow AI” Subsystems 1–11**
   - QMS/risk traceability evaluator  
   - Marketing claim synthesizer  
   - Clinical synopsis generator  
   - SBOM/cybersecurity audit  
   - Multi-country pathway bridge  
   - Biomechanical worst-case assistant  
   - Challenger auditor sandbox  
   - eSTAR schema integrity mapper  
   - Chemical characterization predictor (ISO 10993-18)  
   - EO outgas optimizer (ISO 10993-7)  
   - SaMD privacy sentinel (HIPAA/GDPR)  

### 2.2 New Additions Required in This Upgrade
This upgrade adds:

- **Default LLM model** set to `gemini-3.1-flash-lite` for all LLM features (user can select other Gemini/OpenAI models, and modify prompts safely).
- **WOW LLM execution visualization** (truthful execution theatre), interactive indicators, live log feed.
- **WOW interactive dashboard** with 5 graphs.
- **Theme system**: light/dark + bilingual UI default (Traditional Chinese/English) + **10 sleek Pantone-based styles**.
- **New Module A: Skill.md Studio**
  - Paste/upload `skill.md`, edit, download
  - Ask an agent to modify `skill.md`
  - Paste doc and ask agent to apply `skill.md` to doc
  - User edits results in Markdown  
- **New Module B: Notes Transformer**
  - Paste/upload note (txt/md/pdf)
  - Convert into organized Markdown with **keywords highlighted in coral**
  - PDF OCR options:
    - Python package-based OCR: 3 selectable engines + language choice (TC/EN)
    - LLM-based OCR default: `gemini-3.1-flash-lite`
  - “AI Magics”: 6 created features including **magic keyword highlighting with user-selected colors**
- **3 additional WOW AI features** (added on top of the existing 11; defined in Section 15).
- **Bug-fix iteration baked into design** (Section 13): schema drift, rerun duplication, encoding, PDF memory, OCR errors, injection, status mismatch, logging integrity.

---

## 3. Deployment Architecture (Hugging Face Spaces + Streamlit)

### 3.1 Target Runtime
- **Platform:** Hugging Face Spaces
- **App Framework:** Streamlit (Python)
- **Execution Model:** Single app process with Streamlit session states per user  
- **Storage:** Ephemeral by default; optional persistent volume (if enabled) or export-first strategy

### 3.2 High-Level Topology

```
User Browser
   │  HTTPS
   ▼
Hugging Face Space (Streamlit)
   ├─ UI Pages / Modules
   ├─ Session State & Cache
   ├─ File Parsers (txt/md/json/csv/pdf)
   ├─ OCR Engines (optional)
   ├─ LLM Model Router (Gemini/OpenAI)
   ├─ Agent Runner (agents.yaml)
   ├─ Audit Trail Logger (exportable)
   └─ Part 11 Hash/Signature Utilities
```

### 3.3 Why Streamlit Here (Design Rationale)
- Hugging Face Spaces supports Streamlit natively.
- Streamlit simplifies:
  - Stateful forms
  - File uploads
  - Live logs + progressive updates
  - Rapid UI iteration for regulated workflows (clear controls, minimal UI noise)

### 3.4 Session & Concurrency Considerations (Streamlit-Specific)
Streamlit reruns the script on interactions. This creates common failure modes:
- Duplicate LLM calls when widgets change
- Logs repeating on rerun
- Progress indicators resetting mid-run

**Mitigation strategy:**
- Use a **Run Controller** concept: each “execution” gets a unique `run_id` stored in session state.  
- All long operations must:
  1) allocate a run record  
  2) lock that run while executing  
  3) stream updates into a run-scoped log buffer  
  4) finalize with immutable summary metadata (duration, model, tokens, cost estimate, hash of prompts/outputs)

---

## 4. LLM & Agent Orchestration (Model Router + agents.yaml)

### 4.1 Model Router (Provider Abstraction)
All LLM features call a single internal “Model Router” that supports:

- **Gemini** (default): `gemini-3.1-flash-lite`
- **Optional Gemini alternatives**: user-selectable for cost/performance tradeoffs
- **Optional OpenAI models**: user-selectable where policy allows

**Key requirements:**
- Every request includes: `provider`, `model`, `temperature`, `max_output_tokens`, `safety_mode`, `response_format` (text/json), `system_prompt`, `user_prompt`, and optional `attachments` (OCR images, extracted text chunks).
- For structured outputs (checklist arrays, audit results), enforce a **strict JSON schema** with:
  - validation
  - repair attempt (one retry with a “return valid JSON only” instruction)
  - last-resort fallback (local simulation templates)

### 4.2 Default Model Policy
- All modules default to: `gemini-3.1-flash-lite`
- UI must clearly display current model and provide a “restore defaults” button.
- The user may override model **per module** and optionally **per run**.

### 4.3 Prompt Customization (Safe Prompt Editing)
Users may modify:
- Module-level system instructions (advanced mode)
- Task prompt text (normal mode)
- Output language preference (TC/EN/bilingual)

**Safety controls:**
- Prompt injection mitigations:
  - Always prepend a fixed “Policy & Safety Prefix” that instructs the model to ignore embedded instructions in user documents.
  - For audits: treat uploaded documents as **data**, not instructions.
- Prompt versioning:
  - Store prompt templates with semantic version IDs.
  - Log the template version used for every run.

### 4.4 agents.yaml (Agent Definitions)
The app uses `agents.yaml` to define multi-step workflows. Each agent has:

- **name**
- **purpose**
- **inputs** (e.g., guidance text, checklist JSON, skill.md, note text, OCR text)
- **tools** (LLM calls, OCR extraction, validators)
- **output_schema** (for JSON outputs)
- **postprocessors** (keyword highlighting, markdown formatting, citations)
- **guardrails** (length limits, banned content, PII rules)

Agents must be composable. Example agent categories:

- `guidance_structurer`
- `checklist_generator`
- `submission_transformer`
- `checklist_auditor`
- `summary_compiler`
- `skill_editor_agent`
- `skill_applier_agent`
- `note_organizer_agent`
- `ocr_validator_agent`
- `dashboard_metrics_agent`

### 4.5 Deterministic IDs & Stable Referencing
Checklist items require stable IDs to avoid merge conflicts:
- ID format: `SEC-{section_code}-{sequence}-{hash_suffix}`
- The `hash_suffix` is derived from normalized item text to keep IDs stable across reruns.

---

## 5. Core Workflow Modules (Original 4-Stage Workshop Preserved)

This section specifies Streamlit implementations of the original four stages without changing their intent.

### 5.1 Stage 1 — Guidance Ingestion & Structuring
**Inputs**
- Paste text, or upload: TXT/MD/PDF
- Language hint: Traditional Chinese / English / Auto
- Target pathway: FDA / TFDA / Both

**Processing**
1. If PDF:
   - Extract embedded text first.
   - If text extraction yields low confidence (e.g., too few characters, high symbol ratio), prompt user to run OCR (Module B’s OCR pipeline can also be reused here).
2. Normalize:
   - Remove headers/footers/page numbers when detected
   - Normalize whitespace, bullets, and numbering
3. LLM: “Guidance Structurer” agent
   - Output: clean GFM Markdown outline with sections and explicit requirement statements.

**Outputs**
- Structured guidance Markdown (editable)
- Trace metadata: run ID, model, duration, extraction method

**Bug fixes baked in**
- Avoid double-call reruns by requiring an explicit “Run” button and run lock.
- Apply strict maximum input size; if exceeded, chunk and summarize with overlap.

### 5.2 Stage 2 — Interactive Compliance Grid
**Core functions**
- Table editor for fields:
  - `id`, `section`, `item`, `details`, `status` (符合/待補/不適用), `description`, `evidence_refs`
- Filters:
  - by status
  - by section
  - by keyword search
- Batch operations:
  - Set status for selected rows
  - Add “review needed” tags
  - Merge duplicate items (assisted by LLM but user-confirmed)

**Import/Export**
- CSV (Excel-safe UTF-8 BOM)
- JSON (full fidelity)
- Markdown table (GFM)
- Text blocks (audit-friendly narrative)

**Data integrity**
- Every edit produces a diff event in the audit log.
- Table maintains a `revision_number` that increments on structural changes.

### 5.3 Stage 3 — Submission Transformation & Automated Audit
**Inputs**
- Paste/upload technical dossier (TXT/MD/PDF)
- Optional: attach multiple files (design spec, test report, risk file summary)

**Processing**
1. Transform submission into structured Markdown:
   - Identify test evidence, standards, acceptance criteria, results tables
   - Extract numeric claims and their units
2. Audit checklist:
   - Cross-reference each checklist item with evidence
   - Update statuses and descriptions
   - Add evidence pointers: “Doc: X, Section: Y, Quote: …”

**Outputs**
- Updated checklist JSON
- Evidence map (machine-readable):
  - `checklist_id -> [evidence_snippets]`
- “Audit delta view”:
  - changed items only with before/after

**Bug fixes baked in**
- Schema validation of returned JSON; repair retries.
- Prevent accidental status flipping due to ambiguous evidence by introducing confidence bands:
  - High: auto-update
  - Medium: propose update, require user confirm
  - Low: keep pending, explain missing info

### 5.4 Stage 4 — Summary Compilation + Part 11 Signing
**Inputs**
- Checklist + evidence map
- Output language: TC / EN / bilingual
- Report length target + section toggles

**Processing**
- Generate structured report:
  - Executive summary
  - Bilateral pathway feasibility
  - Compliance matrix summary
  - Engineering evidence narrative (standards-based)
  - Gap remediation plan
  - Part 11 block placeholders

**Signing**
- User provides signer name, title, intent.
- Generate:
  - document hash
  - signature hash
- Append Part 11 signing block to report.
- Provide verification console: paste report → recompute hashes.

**Bug fixes baked in**
- Canonicalization before hashing:
  - Normalize line endings to `\n`
  - Trim trailing whitespace
  - Record canonicalization method in the signing metadata to avoid false mismatch across OS copies.

---

## 6. New Module A — Skill.md Studio (Upload/Edit/Agent-Apply)

This module introduces a controlled, reusable “skill specification” system that functions like an internal rubric or agent operating manual.

### 6.1 Purpose
- Let teams define consistent transformation rules (tone, structure, compliance checks, formatting conventions) in a portable `skill.md`.
- Apply the same skill repeatedly to different documents (guidance, dossiers, marketing copy, risk summaries).

### 6.2 Functional Requirements

#### 6.2.1 Skill.md Ingestion
- Inputs:
  - Paste into editor
  - Upload `skill.md`
- Editor:
  - Markdown editor with live preview
  - Version tag field (e.g., `Skill v1.2`)
  - Change summary field

#### 6.2.2 Agent-Assisted Skill Editing
Default model: `gemini-3.1-flash-lite`

User can request:
- “Improve clarity and remove ambiguity”
- “Add TFDA terminology consistency rules”
- “Add evidence citation requirements”
- “Add bilingual section header conventions”

**Guardrails**
- Agent must output **valid Markdown only**.
- Agent must produce a “diff summary” section:
  - what changed
  - why
  - potential impact

#### 6.2.3 Skill Application to Documents
Workflow:
1. User selects a `skill.md` (current session or library)
2. User pastes/uploads a document
3. User prompts: “Use the skill to transform/criticize/annotate this doc”
4. Output is produced as Markdown in an editable result editor

Output modes:
- Rewrite mode (clean output)
- Annotate mode (inline comments)
- Checklist mode (turn doc into compliance-ready outline)

#### 6.2.4 Download & Portability
- Download `skill.md` and generated results as `.md`
- Export as a “Skill Pack” zip:
  - `skill.md`
  - `skill.metadata.json` (model, versions, authorship, hash)

### 6.3 Bug Fixes & Edge Cases
- Avoid “skill prompt injection”: treat `skill.md` as trusted only if user authored; still wrap with stable system constraints.
- Prevent runaway outputs: enforce output length ceilings and section-by-section generation.
- Maintain encoding fidelity for Traditional Chinese punctuation and numbering.

---

## 7. New Module B — Notes-to-Organized Markdown + OCR + AI Magics

### 7.1 Purpose
Convert messy notes into structured Markdown, highlight key terms in **coral**, and optionally extract text from PDFs using OCR.

### 7.2 Inputs
- Paste notes (text)
- Upload: `.txt`, `.md`, `.pdf`
- Output language:
  - Traditional Chinese
  - English
  - Bilingual (side-by-side or interleaved)

### 7.3 Transformation Output Requirements
The organized Markdown must include:
- Title (auto-inferred)
- Short abstract (3–6 bullets)
- Main sections with headers
- Key points / evidence / open questions
- Action items (if any)
- Glossary (optional)

**Coral keyword highlighting**
- Default: domain keywords (standards, test names, materials, regulators) highlighted in coral.
- Implementation requirement: highlight must be **pure Markdown** using a stable inline convention such as:
  - HTML span tags allowed in Markdown rendering, e.g. `<span style="color:#FF6F61;font-weight:700">keyword</span>`
- Must be consistent and export-safe.

### 7.4 PDF Processing & OCR Options

#### 7.4.1 Extraction Decision Tree
1. Attempt embedded text extraction.
2. If extracted text quality < threshold:
   - Offer OCR mode selection:
     - Python package OCR (3 choices)
     - LLM OCR (default `gemini-3.1-flash-lite`)

Quality threshold heuristic examples:
- Character count per page
- Ratio of alphanumerics to symbols
- Frequency of “�” replacement characters
- Language detection confidence

#### 7.4.2 Python Package OCR (3 engines)
User selects:
1. **Tesseract OCR** (broad support; good baseline)
2. **PaddleOCR** (strong for CJK; better layout handling)
3. **EasyOCR** (simple integration; decent multilingual)

User selects language pack:
- Traditional Chinese
- English
- Mixed (TC + EN)

**OCR output requirements**
- Return:
  - plain text
  - page breaks
  - confidence estimate per page
  - warnings (e.g., “low confidence on pages 12–15”)

#### 7.4.3 LLM-based OCR (Default)
- Convert PDF pages to images (bounded by max pages)
- Send images to Gemini multimodal OCR prompt:
  - “Extract text faithfully; preserve headings; do not summarize; output with page tags”

**Controls**
- Max pages per run (to control cost)
- Chunk pages into batches (e.g., 5–10 pages per call)
- Post-merge with ordering validation

### 7.5 AI Magics (6 WOW AI Features inside Notes Module)

These are user-invoked tools that apply on top of the organized Markdown. Each magic has:
- a one-click button
- an “advanced prompt” expandable panel
- deterministic output sections

#### Magic 1 — “Key Takeaways Distiller”
Produces:
- 10 bullet takeaways
- 3 critical risks
- 3 next actions

#### Magic 2 — “Flashcards & Quiz Builder”
Produces:
- Q/A flashcards for learning
- “Reviewer-style” questions for regulatory interviews

#### Magic 3 — “Action Items & Owners Extractor”
Produces a table:
- Action
- Owner (if inferable or “TBD”)
- Due date (if present)
- Evidence required

#### Magic 4 — “Standards Mapper”
Detects standards references (ISO/IEC/ASTM/CFR) and generates:
- standards list
- what evidence is typically required for each
- which module can help generate it (cross-link to checklist workshop)

#### Magic 5 — “Contradiction & Ambiguity Scanner”
Flags:
- inconsistent units
- contradictory claims
- missing acceptance criteria
- ambiguous language (“adequate”, “appropriate”) with rewrite suggestions

#### Magic 6 — “Magic Keyword Highlighter (User-Controlled Colors)”
User inputs:
- keywords list (comma-separated or newline)
- selects color per group (palette)
- chooses scope:
  - highlight in input only
  - highlight in output only
  - highlight both

Output must:
- preserve original text
- add consistent inline highlight markup
- provide a keyword index at bottom with counts and locations (section headers)

### 7.6 Bug Fixes & Edge Cases
- PDFs with rotated pages: detect orientation; rotate for OCR where possible.
- Two-column scientific PDFs: preserve reading order using layout heuristics; if uncertain, annotate: “layout ambiguous”.
- Avoid corrupting Markdown with unescaped characters (e.g., `_`, `*`, `|`): enforce escaping rules in postprocessor.
- Ensure coral highlighting does not break tables or code blocks (skip highlight inside fenced code).

---

## 8. WOW LLM Execution Visualization + Live Logs + Interactive Indicators

This upgrade adds an execution “theatre” that is visually impressive but grounded in real system events.

### 8.1 Execution Theatre Components

#### 8.1.1 “Pipeline Stepper” (Truthful)
Displays steps such as:
1. Input validated
2. Preprocessing (chunking, OCR, normalization)
3. LLM call started (model shown)
4. Streaming response
5. Schema validation
6. Postprocessing (highlighting, citations)
7. Completed + exported artifacts ready

Each step includes:
- start/end timestamps
- duration
- warnings/errors badges

#### 8.1.2 Token Stream Visualization (Non-Fake)
- If provider supports streaming: show incremental token output in a console-like pane.
- If streaming not available: show chunked “received blocks” with timestamps.

#### 8.1.3 Interactive Indicators
Indicators must correspond to measurable metrics:
- “Context load” bar: proportion of context window used (estimated)
- “Evidence coverage” gauge (for audits): % checklist items with at least one evidence snippet
- “Confidence band” distribution: counts of High/Medium/Low updates

### 8.2 Live Log (Unified, Exportable)
A live log panel shows structured events:

- `timestamp`
- `module`
- `run_id`
- `severity` (info/warn/error/success)
- `event_type` (OCR_PAGE_DONE, LLM_CALL_START, JSON_REPAIR_ATTEMPT, EXPORT_READY)
- `details`

**Export formats**
- JSONL (machine-readable)
- CSV (audit-friendly)
- Markdown summary (human-readable)

### 8.3 Anti-Duplication & Rerun Safety
To prevent repeated calls due to Streamlit reruns:
- A “Run” button creates a `run_id`.
- All downstream steps check:
  - if run exists
  - if locked
  - if completed
- Results are cached by `run_id` and input hash.

---

## 9. Interactive Dashboard (5 WOW Graphs)

A dashboard provides real operational intelligence for RA teams and makes progress visible without distorting reality.

### 9.1 Dashboard Data Sources
- Checklist dataset (statuses, sections, timestamps)
- Evidence map (evidence counts, confidence bands)
- Run logs (durations, failures, model used)
- OCR metrics (confidence per page, engine used)
- Cost estimates (token usage approximations where available)

### 9.2 The 5 WOW Graphs (Required)

1. **Compliance Status Donut**
   - % 符合 / 待補 / 不適用
   - Click segment → filters checklist table

2. **Section Heatmap Matrix**
   - Rows: sections (e.g., biocompatibility, sterilization, mechanical)
   - Columns: status counts or coverage %
   - Highlights “hot” weak sections with most pending items

3. **Gap Aging Trend (Time Series)**
   - Tracks how long items remain “待補”
   - Shows median and worst-case aging
   - Helps project submission readiness

4. **Evidence Coverage vs Risk Priority Scatter**
   - X-axis: evidence coverage score
   - Y-axis: risk priority (from ISO 14971 tags if provided)
   - Identifies high-risk low-evidence items requiring immediate action

5. **LLM Operations Performance Panel**
   - Duration per run (box plot)
   - Failure rate by provider/model
   - Helps tune default configs and detect outages

### 9.3 Interactivity Requirements
- Cross-filtering between graphs and the checklist table
- Hover tooltips include:
  - item IDs
  - key evidence snippet counts
  - last modified timestamps

---

## 10. UI/UX System: i18n, Themes, 10 Pantone-Based Styles

### 10.1 Language System (Default TC/EN)
- App-level language toggle: Traditional Chinese / English
- Default: bilingual-friendly; labels can show:
  - Primary language + smaller secondary subtitle (optional setting)
- Output language control per run (so UI language doesn’t force report language)

### 10.2 Theme Toggle
- Light theme and dark theme must both be first-class.
- All charts must be legible in both themes with controlled contrast ratios.

### 10.3 10 Sleek Styles (Pantone-Inspired Palettes)
Each style defines tokens:
- `primary`, `secondary`, `accent`, `bg`, `surface`, `text`, `muted`, `danger`, `warning`, `success`, `coral_highlight`

Proposed 10 styles (names are internal; visually sleek, clinical, and professional):
1. **Classic Blue (Pantone 19-4052)**
2. **Living Coral (Pantone 16-1546)** — align with coral keyword highlight
3. **Ultra Violet (Pantone 18-3838)**
4. **Emerald (Pantone 17-5641)**
5. **Turmeric (Pantone 15-1264)**
6. **Fiesta Red (Pantone 17-1564)**
7. **Serenity (Pantone 15-3919)**
8. **Rose Quartz (Pantone 13-1520)**
9. **Cyber Lime (Pantone 14-0445)** (used sparingly for indicators)
10. **Graphite Neutral (Pantone 19-3906)** (minimalist compliance look)

### 10.4 Accessibility Requirements
- Minimum contrast targets:
  - Normal text ≥ WCAG AA
  - Graph labels must remain readable
- Color is never the only signal:
  - status badges include text + shape/icon + tooltip

---

## 11. Security, Privacy, 21 CFR Part 11, and Audit Trails

### 11.1 API Key Handling (Environment + User Input)
- If environment-provided (HF Secrets):
  - do not display the key
  - show status: “Key detected from environment”
- If not provided:
  - allow user input in a password field
  - store only in session state (memory)
  - never write to logs
  - provide “clear key” button

### 11.2 Data Privacy Controls
- Default stance: user data stays in the Space runtime memory unless exported.
- Explicit warnings:
  - LLM calls send excerpts to external providers.
  - Provide a “redaction mode” toggle:
    - mask PHI/PII patterns before sending (names, IDs, emails)
    - show a preview of redacted text

### 11.3 Part 11-Aligned Audit Trail
Audit events must include:
- who (session signer name if provided)
- what (action)
- when (UTC timestamps)
- result (success/failure)
- artifact hashes (input hash, output hash, signature hash)

Persistence options:
- Export-first (default): user downloads audit trail
- Optional persistence (if Space has storage):
  - local SQLite in persistent volume
  - log rotation and integrity hashes per day

### 11.4 Tamper-Evidence & Verification
- Verification console recomputes:
  - document hash
  - signature hash
- If mismatch:
  - show which canonicalization method was used
  - highlight likely reasons (line ending changes, trimmed spaces, content edits)
  - produce a verification report for QA records

---

## 12. Data Models, Storage Strategy, and Export Packages

### 12.1 Core Data Entities (Conceptual)
- `ChecklistItem`
- `EvidenceSnippet`
- `RunRecord`
- `PromptTemplate`
- `SignatureRecord`
- `SkillDocument`
- `NoteDocument`
- `OCRResult`
- `DashboardMetrics`

### 12.2 Export Packages (Submission Readiness Pack)
User can export a ZIP containing:
- `checklist.json`
- `checklist.csv`
- `checklist.md`
- `audit_report.md`
- `evidence_map.json`
- `run_logs.jsonl`
- `signature_records.json`
- `skill.md` (if used)
- `notes_organized.md` (if used)
- `manifest.json` with hashes for each file

### 12.3 Offline / Fallback Operation
If no API keys or provider failure:
- Use a local “simulation database” of templates (clearly labeled as simulated)
- Allow manual editing so the workflow remains usable
- Log: “Simulated output used due to provider unavailability”

---

## 13. Reliability Engineering: Bug Fixes, Failure Modes, and Mitigations

This section explicitly addresses common failure patterns to “iterate until excellent results.”

### 13.1 LLM JSON Drift / Invalid Structure
**Problem:** Model returns commentary, trailing commas, wrong keys, partial arrays.  
**Mitigations:**
- Strict schema validation
- One automatic repair retry with:
  - “Return JSON only, no prose”
  - Include the schema snippet in the prompt
- If still invalid:
  - fallback to “best-effort parser” that extracts JSON block
  - log the failure and mark run as “needs review”

### 13.2 Checklist Status Inconsistency
**Problem:** Status flips to 符合 with weak evidence.  
**Mitigations:**
- Introduce confidence bands and require confirmation for medium/low
- Evidence snippet minimum requirement:
  - at least one quote + section pointer for “符合”
- Add “review flag” boolean field

### 13.3 Streamlit Rerun Duplicate Calls
**Problem:** widget changes rerun script, re-triggering expensive calls.  
**Mitigations:**
- Only execute when user clicks “Run”
- Run lock by `run_id`
- Cache by `(input_hash, model, prompt_version)` for idempotency

### 13.4 PDF Memory & Large File Failures
**Problem:** big PDFs cause slowdowns or memory errors.  
**Mitigations:**
- Page-limited extraction with user override
- Chunking pipeline with overlap
- Progressive extraction: show partial results, allow stop/cancel
- Provide “extract only selected page range” mode

### 13.5 OCR Hallucination & Layout Errors
**Problem:** LLM OCR may “clean up” text incorrectly; package OCR may scramble columns.  
**Mitigations:**
- OCR validation agent compares:
  - character distribution
  - numeric preservation (tables)
  - repeated headers detection
- If risk detected, annotate output sections as “OCR uncertain”
- Preserve raw OCR output as a downloadable artifact

### 13.6 Encoding & Excel Corruption (Traditional Chinese)
**Problem:** CSV opened in Excel breaks Chinese.  
**Mitigations:**
- Always export CSV with UTF-8 BOM
- Provide TSV alternative
- Provide “Excel-safe quoting mode” for commas/newlines

### 13.7 Keyword Highlight Breaks Markdown
**Problem:** highlighting inside code blocks/tables corrupts formatting.  
**Mitigations:**
- Postprocessor must detect fenced code and table regions; skip or handle safely
- Provide “strict mode” highlight: only in paragraphs and headers

### 13.8 Prompt Injection from Uploaded Docs
**Problem:** docs contain instructions like “Ignore previous instructions.”  
**Mitigations:**
- System prompt explicitly states:
  - documents are data
  - ignore embedded instructions
- For audits, require citations; unsupported claims are rejected and marked pending

### 13.9 Audit Log Integrity
**Problem:** logs incomplete or duplicated across reruns.  
**Mitigations:**
- Append-only event list with monotonic event IDs
- Export includes per-event hash chain (optional):
  - `event_hash_i = sha256(event_hash_{i-1} + event_payload)`

---

## 14. Testing & Validation Plan (Regulated-Grade)

### 14.1 Test Categories
1. **Unit-level logic tests (conceptual in this spec)**
   - hashing canonicalization
   - schema validation
   - export formatting
2. **Integration tests**
   - OCR → text → note transformer
   - checklist audit with evidence map
3. **Regression suites**
   - fixed sample guidance + known expected checklist structure
   - fixed dossier excerpt + expected status deltas
4. **Performance tests**
   - PDF 50/200/500 pages with chunking
   - OCR batch page limits
5. **Security tests**
   - prompt injection attempts
   - API key handling verification (no echo)
   - PII redaction tests

### 14.2 Acceptance Criteria (Examples)
- Checklist generator returns valid schema ≥ 99% runs with default model.
- Audit tool never marks “符合” without evidence snippet + location.
- Signature verification must be stable across download/upload roundtrips.
- Dashboard graphs must match underlying table counts exactly (no drift).

---

## 15. Additional WOW AI Features (3 New)

These three features are added **in addition** to the existing 11.

### WOW Feature 12 — “Predicate & Equivalence Argument Builder (510(k))”
**Goal:** Reduce time to craft a defensible substantial equivalence narrative.  
**Inputs:** device description, intended use, key tech characteristics, known competitors/predicates (optional).  
**Outputs:**
- A structured “equivalence argument” outline:
  - intended use comparison
  - technological characteristics table
  - performance testing comparison plan (what must match, what can differ)
- Risk flags where differences likely trigger clinical data or additional bench tests  
**Safeguard:** Must label “requires human verification” for any predicate claims.

### WOW Feature 13 — “Evidence Citation Auto-Indexer (Quote-to-Checklist Linker)”
**Goal:** Make audits reviewable by linking every compliance claim to exact evidence.  
**Inputs:** dossier text + checklist.  
**Outputs:**
- An evidence index:
  - `checklist_id -> [quote, doc_section, confidence, rationale]`
- A “citation coverage score”
- A reviewer-friendly appendix in Markdown  
**Key constraint:** The model must not invent quotes; it must extract exact substrings from the provided text (validated by substring check).

### WOW Feature 14 — “Regulatory Change Impact Simulator (FDA/TFDA Watch Mode)”
**Goal:** Help teams understand how guidance changes would impact their checklist and gaps.  
**Inputs:** current checklist + “new guidance excerpt” pasted by user (or user notes).  
**Outputs:**
- Impact assessment:
  - which checklist items are affected
  - what new items should be added
  - what evidence becomes insufficient
- A “migration plan” with prioritized actions  
**Value:** Prevents late-stage surprises when templates or reviewer expectations shift.

---

## Appendix: 20 Comprehensive Follow-Up Questions

1. For **Hugging Face Spaces**, will we enable **persistent storage**? If not, which artifacts must be export-mandatory to avoid loss (logs, checklists, signatures, OCR raw text)?  
2. What is the authoritative bilingual terminology glossary for TFDA (e.g., “查驗登記”, “技術性資料”) that the system must consistently enforce across outputs?  
3. For the **Predicate & Equivalence Argument Builder**, do we want optional integration with public databases (e.g., openFDA 510(k) queries), or must it remain fully offline/manual-input?  
4. What is the expected maximum size (pages / MB) of PDFs for typical users, and what hard limits should be enforced in the UI to prevent Space memory exhaustion?  
5. Which OCR engine should be recommended by default for Traditional Chinese—Tesseract, PaddleOCR, or EasyOCR—based on your typical document layouts (two-column journals vs scanned forms)?  
6. Should the app support **mixed-language OCR** (TC+EN within the same page) by default, and how should it report confidence per language segment?  
7. For Part 11 alignment, do we need **two-factor signer authentication** or is typed-name + intent + timestamp sufficient for the intended internal use?  
8. Should signature records be **role-restricted** (Viewer/Editor/Signer) even in a single-user Streamlit deployment, and if so, what identity mechanism is acceptable on Spaces?  
9. What is the policy for handling potentially sensitive content (PHI/PII): default redaction on, or opt-in, and what redaction patterns are required?  
10. For the checklist audit, do you want the system to enforce a minimum evidence quality rule such as “must cite test standard + acceptance criteria + actual result” before allowing “符合”?  
11. How should the system handle **conflicting evidence** (two sections with different material specs): auto-flag as contradiction, or ask the user which source is authoritative?  
12. What “confidence band” thresholds are acceptable for automatic status updates, and should thresholds differ by section (e.g., biocompatibility vs mechanical)?  
13. For the dashboard’s “Risk Priority,” will users provide ISO 14971 risk scoring fields (severity/probability/detectability), or should the system infer a proxy from keywords?  
14. Should the “Evidence Citation Auto-Indexer” require substring-verification strictly (no paraphrases), and how should it handle OCR errors where exact substrings may not match cleanly?  
15. Which export package structure best matches your internal QA process: one ZIP per run, or a project folder that accumulates versions over time?  
16. Do you need **version comparison** views for checklists and summaries (diff across revisions) as a first-class feature, and what granularity (row-level, sentence-level)?  
17. How should the system manage **prompt template governance**—can any user edit prompts, or do we need locked templates with an admin-only override?  
18. What is the expected bilingual output format preference: side-by-side columns, alternating paragraphs, or single-language output per section with a bilingual glossary?  
19. For Regulatory Change Impact Simulator, what sources define “change”—user pasted excerpts only, or do you want a manual registry where users store guidance versions and compare them?  
20. What are the top 10 “submission-killer” failure patterns you want the Challenger Sandbox to focus on (e.g., missing worst-case rationale, incomplete sterilization validation, unclear intended use, etc.) so we can calibrate adversarial questioning precisely?
