<div align="center">

# LATTE Study Suite

**A single-file, serverless study toolkit for nursing students — powered by the Gemini API.**

Five AI-powered tools in one HTML file.
No server. No install. No account. Just open and go.

[**↓ Download Study Suite**](LATTE-Study-Suite.html) · [Get a Gemini API Key](https://aistudio.google.com/apikey)

-----

</div>

## What Is This?

One HTML file containing five study tools, all built around the **LATTE clinical framework** and a **3-tier priority system** that maps directly to how nursing exams test clinical reasoning.

Upload your lecture PowerPoints, textbook PDFs, and review materials. The tools generate study guides, flashcards, priority analysis, and practice questions — all processed in your browser using Google’s Gemini API.

-----

## The Study Pipeline

Each tool feeds the next. The LATTE tags are the thread that ties everything together.

|Step             |Tool                 |What It Does                                      |
|-----------------|---------------------|--------------------------------------------------|
|**01 — Read**    |Study Guide Generator|Builds the big picture from your source files     |
|**02 — Triage**  |Priority Analyzer    |Sorts content into Tier 1/2/3 by exam importance  |
|**03 — Memorize**|Anki Generator       |Creates atomic cloze cards for spaced repetition  |
|**04 — Apply**   |NCLEX Extractor      |Tests whether you can use it in clinical scenarios|

-----

## Tools

### 📖 LATTE Study Guide Generator

Upload lecture PPTs and textbook PDFs → comprehensive, exam-ready study guide organized by the LATTE framework.

- **Two-phase pipeline**: Extraction (Flash model, per-file) → Synthesis (Pro model with optional thinking)
- Mandatory Step 0 extraction log with source-cited tables (conditions, meds, labs, numerical values)
- One LATTE section per condition — never combined
- Supplemental reference tables A–J (Pharmacology, Diagnostics, Scoring Tools, Formulas, DO vs DO NOT, Complications, Outcome Mapping, Points Verification, Contradictions)
- Overlap context carry-forward between files
- Course name, exam name, outcomes, and points fields
- Export: Copy · .md · .txt · PDF

-----

### △ Pyramid Priority Analyzer

Upload a study guide → content triaged into Tier 1/2/3 using Elsevier’s textbook pedagogy hierarchy.

- **Two-phase chunked pipeline**: Flash extraction per chunk → Pro synthesis with streaming
- Previous-chunk context carry-forward for consistent tier assignments
- Configurable chunk size and overlap
- Color-coded tier output sections
- Additional context field to steer prioritization
- Export: Copy · .md · .txt · PDF

-----

### 🖥 LATTE Anki Generator

Upload PDFs → Anki-ready cloze flashcards with LATTE tagging, 3-tier priority system, and a coverage ledger audit trail.

**Powered by the v10c Master Prompt** — 17,000+ characters, 19 processing phases:

|Phase     |What It Does                                       |
|----------|---------------------------------------------------|
|0         |Input handling — clean artifacts, deduplicate      |
|1         |LATTE bucket assignment for every fact             |
|1.25      |Fast-review compression (punchy, not textbook)     |
|1.5       |Atomicity rules (one fact = one card)              |
|1.75      |List handling (never test 3+ items in one cloze)   |
|1.9       |Anti-redundancy + anti-overfragmentation           |
|2         |Substantive detail threshold                       |
|3         |Exhaustive extraction by LATTE bucket              |
|3.5       |Extra field rules (lean by default, 0–12 words)    |
|3.75      |Extra field grounding tiers (no hallucinated facts)|
|4         |Zero-skip coverage audit                           |
|5         |Pre-output audit (format, dedup, specificity)      |
|Final Gate|Coverage ledger with line-number mapping           |

**Additional features:**

- Optional Focus Context fields (Outcomes, Points, Additional Context) to guide generation toward specific exam objectives
- Non-nursing adaptation — auto-switches tags for A&P, chemistry, biology (uses `Topic::` instead of `Condition::` and subject-appropriate domain tags)
- Page overlap in chunking with automatic deduplication
- Tier filtering in review UI (T1/T2/T3 buttons with counts)
- Table and List view with inline editing
- Coverage ledger output for verification
- Export: .txt (pipe-delimited Anki import)

-----

### 🔀 Anki Deck Merger

Upload two Anki .txt exports → AI-powered analysis, comparison, deduplication, and merged deck for LPN-to-RN bridge / HESI prep.

- Deck comparison with overlap analysis and bridge relevance scoring
- LPN→RN gap analysis identifying scope-expansion topics
- Batched merging with configurable batch size
- Card-level review with category tagging, search, and tag filtering
- Inline editing and bulk select/deselect
- Export: .txt with preserved cloze formatting

-----

### ✅ NCLEX Question Extractor

Upload nursing review PDFs → extracted practice questions with rationales, strategies, and disease tagging.

|Mode           |Use Case                                                          |
|---------------|------------------------------------------------------------------|
|📄 **Inline**   |Q&A on same pages — standard review books                         |
|📑 **Split Q&A**|Questions and answers on separate pages (Davis Test Success style)|

- Split mode: configurable page ranges for question and answer sections
- Multi-pattern regex pairing with AI fallback when regex finds too few matches
- Automatic PDF page count detection with smart default ranges
- Filters: test-taking strategy, disease/keyword search
- Expandable question cards with rationale, tips, strategy, and clinical judgment skill
- Export: Copy · .md · .txt · PDF

-----

## The LATTE Framework

LATTE splits every clinical condition into six buckets that mirror the nursing process:

```
L — Brief Patho    →  What is going wrong mechanically?
L — Look           →  What do you observe? (signs, symptoms, hallmark findings)
A — Assess         →  What does the nurse DO to gather data?
T — Tests          →  Labs, diagnostics, imaging — values and interpretations
T — Treatments     →  Meds (doses, routes, hold/notify), nursing interventions
E — Educate        →  Patient/family teaching, discharge, when to seek care
```

-----

## Tag System

Every Anki card gets tagged on three independent axes, creating a filterable matrix:

```
Nursing::LATTE::Treatments::Meds     ←  WHAT type of knowledge
Condition::HeartFailure               ←  WHICH condition
Tier::1                                ←  HOW important for exams
```

**Filter by tier** — `Tier::1` = pass the exam. `Tier::2` = get the B. `Tier::3` = get the A.

**Filter by LATTE bucket** — Weak on assessments? Filter `Nursing::LATTE::Assess` and drill.

**Filter by condition** — Before cardiac exam, filter `Condition::HeartFailure` for the complete clinical picture — patho through education in one view.

-----

## Tier System

|Tier                     |Distribution|What It Covers                                                                                                          |
|-------------------------|------------|------------------------------------------------------------------------------------------------------------------------|
|**Tier 1 — Must Know**   |50-60%      |Safety-critical content, hallmark signs, priority interventions, major meds, hold/notify thresholds. Nail Tier 1 = pass.|
|**Tier 2 — Should Know** |25-35%      |Supporting pathophysiology, secondary signs, additional monitoring, less common drug effects. T1 + T2 = the B.          |
|**Tier 3 — Good to Know**|10-15%      |Deep mechanism details, rare exceptions, edge cases. If time permits after mastering T1 and T2.                         |

### Tier Strategy with FSRS

For compressed study windows (3 days before an exam):

1. Create a filtered deck: `tag:Tier::1`
1. Set high daily review limit
1. Review until retention is solid on Tier 1
1. If time remains, add `tag:Tier::2`
1. Let Tier 3 stay on normal FSRS schedule

-----

## Adapting for Non-Nursing Content

The Anki Generator’s Focus Context fields allow adaptation for any subject:

1. Enter learning objectives in the **Outcomes** field
1. Enter specific topics in the **Points** field
1. Add context in the **Additional Context** field (e.g., “This is an anatomy textbook, Chapter 10 only”)

When non-nursing content is detected, the tag hierarchy auto-adapts:

- `Topic::` instead of `Condition::`
- Subject-appropriate domain tags (e.g., `AandP::Musculoskeletal::Structure`, `Bio::CellBiology::Mitosis`)
- Tier system and card quality standards stay the same

-----

## Shared Infrastructure

### API & Models

- **Single API key entry** shared across all tools
- Key stored in `sessionStorage` — cleared when you close the tab
- **Flash model** for extraction (default: `gemini-3-flash-preview`)
- **Pro model** for synthesis/thinking (default: `gemini-3.1-pro-preview`)
- Configurable model IDs — update when new models release
- **Thinking mode** toggle with level selector (Low / Medium / High)
- Uses `thinkingConfig: { thinkingLevel }` — never `thinkingBudget`

### Large File Handling

- Files ≤ 15MB → `inline_data` (base64, fast)
- Files > 15MB → **Google File API** (resumable upload, supports up to 2GB)
- Automatic detection — no user action needed
- Uploaded files cleaned up after pipeline completes

### Architecture

- **Single HTML file** (~150KB) — no build step, no dependencies, no server
- React 18 + Babel (in-browser JSX transpilation)
- pdf.js for client-side PDF text extraction
- marked.js for Markdown rendering
- html2pdf.js for PDF export
- All processing happens in the browser — files never leave your machine except to call Google’s Gemini API

-----

## Quick Start

1. **Download** `LATTE-Study-Suite.html`
1. **Open** it in any modern browser (Chrome, Firefox, Edge, Safari)
1. **Enter** your [Gemini API key](https://aistudio.google.com/apikey) in the config sidebar
1. **Select** a tool from the left nav rail
1. **Upload** your course files and generate

-----

## Security

|                            |                                                                                  |
|----------------------------|----------------------------------------------------------------------------------|
|🔒 **Session-Only Storage**  |API key stored in `sessionStorage` — cleared when you close the tab               |
|🌐 **Direct to Google**      |Key sent only to `generativelanguage.googleapis.com` via HTTPS                    |
|💻 **Client-Side Processing**|All files processed in your browser — nothing leaves your machine except API calls|
|📄 **No Secrets in File**    |The HTML contains zero credentials — safe to host publicly                        |

-----

## Requirements

- A modern web browser
- A [Google Gemini API key](https://aistudio.google.com/apikey) (free tier available)
- PDF, PPTX, or image files to process
