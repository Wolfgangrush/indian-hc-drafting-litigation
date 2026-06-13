---
name: _drafting_common
description: Shared reference for all Indian High Court drafting skills in this plugin. Holds the enforcement rules, anti-pollution architecture, the High-Court AI-use risk constraints (Bombay HC, Madras HC, Delhi HC, and other HCs have all cautioned advocates against AI-fabricated citations — one hallucinated authority is career-threatening), and the bench-config-driven formatting conventions. Bench-specific Registry-facing values (Court header, parties separator, section-header style, annexure prefix, counsel block, paper / font / margins) are sourced from `<case-folder>/bench-config.md` at run-time — see `${CLAUDE_PLUGIN_ROOT}/bench-config/exemplars/` for per-HC exemplars. NOT invoked directly — referenced from every drafting skill via @-reference.
allowed-tools: []
---

# Shared Drafting Common — Rules & Constraints (Indian High Courts)

This file is referenced from every drafting skill in the `indian-hc-drafting` plugin. It is NOT invoked on its own.

The plugin's core design principle: a uniform structural skeleton across Indian HCs, with bench-specific Registry-facing values supplied by the user via `<case-folder>/bench-config.md` at run-time.

## THE ENFORCEMENT RULES (non-negotiable)

1. **No external-memory MCP tools in drafting skills.** Drafting skill `allowed-tools:` lists MUST exclude any external-memory, vault, or cloud-sync MCP tool. A drafting skill operates strictly on the case folder. Hard wall.

2. **Case-folder scoping.** Every drafting skill auto-fires only when the user is working inside a case folder. The plugin ships with NO hardcoded case path — the path is user-controlled.

3. **Per-case CLAUDE.md is OPT-IN, self-contained.** No external imports. Case context only — parties, court, judge, key dates, counsel's role.

4. **Bench-config is mandatory.** Every case folder must contain a `bench-config.md` identifying the user's HC bench and specifying the bench-specific values. The Reader agent halts the pipeline if `bench-config.md` is absent or has unfilled placeholders. **The plugin does NOT default to any specific HC's conventions.** Bombay HC values are the author's most-validated exemplar but they are NOT the universal default.

5. **🔴 LAYER 2 IS APPEND-ONLY FROM SKILL/AGENT SIDE.**
   - Skills/agents may: READ existing files in case folder, WRITE new draft files (case-facts.md, format-shell.md, draft-v*.docx, etc.), EDIT files they themselves created in this session
   - Skills/agents may NOT: rm, mv, rmdir, trash, rename, delete, overwrite-without-versioning

5.1. **🔴 WORKING-COPY RULE — never operate on originals.**
   When an agent needs to convert / extract / transform any existing case file, it MUST create a working copy under `~/.claude/working-copies/<case-name>/` and operate on the copy only. The original file is NEVER opened-for-write.

## LOCKED CONSTRAINTS (Indian High Court AI-use risk — all HCs, not Bombay only)

> Multiple Indian High Courts (Bombay, Delhi, Madras, Kerala) and the Supreme Court of India have publicly cautioned advocates against AI-use that produced hallucinated citations. **One hallucinated authority before any Indian HC = career-threatening.** This rule applies regardless of which HC bench the case is filed at.

These rules apply to every drafting agent:

- **NO internet for facts.** No WebSearch, no WebFetch for case content. Hardcoded sources only (the case folder + law PDFs supplied by the user).
- **Statutes from training data ONLY for:** Constitution of India, CPC 1908, CrPC 1973, IPC 1860, IEA 1872, BNS 2023, BNSS 2023, BSA 2023. All other statutes (POCSO, NDPS, MV Act, IT Act, Arbitration Act, etc.) must be supplied by the user as PDF before they can be cited. Reader flags missing law PDFs and STOPS.
- **Case citations — STRICT.** Every case citation in the output MUST trace to the user-supplied `citations.md`. Drafter NEVER generates a case name + citation pair from training memory. Where a ground requires support and no user-supplied citation matches, the Drafter writes `[CITATION NEEDED: <legal proposition>]` and the Verifier flags it.
- **File-based pipeline.** Each agent writes its output to a file → next agent reads. Auditable chain of custody.
- **Triple-verify is OPTIONAL.** Verifier + Refiner + Overseer = 3 independent QC passes available to the advocate at their discretion. None is mandatory before filing. See §Pipeline-optionality below.
- **Final draft must be indistinguishable from a manually-drafted pleading.** No "AI-style" markers.
- **The user remains the responsible advocate.** The plugin is a drafting aid; every draft must be reviewed before filing.

## BENCH-CONFIG-DRIVEN FORMATTING CONVENTIONS

The plugin operates on a uniform structural skeleton; **bench-specific Registry-facing values are sourced from `<case-folder>/bench-config.md` at run-time.** No bench's conventions are hardcoded in this plugin's skills or agents. Every `{{bench_config.X}}` placeholder in the case-type skills resolves to a value the user supplies in their bench-config.

Per-HC bench-config exemplars in `${CLAUDE_PLUGIN_ROOT}/bench-config/exemplars/` cover the major Indian HCs:

| HC | Court header (illustrative — verify against the bench's current Practice Notes) | Annexure prefix | Notable difference |
|---|---|---|---|
| Bombay HC | `IN THE HIGH COURT OF JUDICATURE AT BOMBAY BENCH AT [BENCH CITY].` (period at end) | `ANNEXURE-` | `///VERSUS///` separator · spaced section heads (`F A C T S`) · 1.5 line spacing |
| Bombay HC Principal (Mumbai) | `IN THE HIGH COURT OF JUDICATURE AT BOMBAY.` | `ANNEXURE-` | similar to [bench city] with bench-specific Practice Notes |
| Bombay HC Aurangabad | `IN THE HIGH COURT OF JUDICATURE AT BOMBAY BENCH AT AURANGABAD.` | `ANNEXURE-` | similar to [bench city] |
| Bombay HC Goa | `IN THE HIGH COURT OF BOMBAY AT GOA.` | `ANNEXURE-` | similar to [bench city] with Goa-specific overlay |
| Delhi HC | `IN THE HIGH COURT OF DELHI AT NEW DELHI.` | `Annexure-` (some `P-1` style) | **A4 + DOUBLE spacing** + advocate name + enrolment + phone + email at foot of pleading (Delhi HC Original Side Rules 2018) |
| Karnataka HC | `IN THE HIGH COURT OF KARNATAKA AT BANGALORE.` | `Annexure-` | **Letter `I` is OMITTED** from annexure marks (Karnataka HC Writ Proceedings Rules 1977 sequence: A, B, C, D, E, F, G, H, J, K, L, M, N, O, P, Q, R, S, T, U, V, W, X, Y, Z) |
| Madras HC | `IN THE HIGH COURT OF JUDICATURE AT MADRAS.` | `Document No.` (often) / `Annexure-` (sometimes) | Original Side / Appellate Side distinct procedures (Madras HC OS Rules 1956 + AS Rules) |
| Calcutta HC | `IN THE HIGH COURT AT CALCUTTA.` | `Annexure-` | Original Side has AOR concept similar to SC (Calcutta HC OS Rules 1914) |
| Allahabad HC | `IN THE HIGH COURT OF JUDICATURE AT ALLAHABAD.` (Lucknow Bench: `AT LUCKNOW`) | `Annexure-` | Schedule III Forms 1-100 govern specific case-type proformas (Allahabad HC Rules 1952) |
| Punjab & Haryana HC | `IN THE HIGH COURT OF PUNJAB AND HARYANA AT CHANDIGARH.` | `Annexure P/` (petitioner) · `Annexure R/` (respondent) | **DOUBLE spacing on watermarked plain paper** (Punjab & Haryana HC Rules & Orders Volume V) |
| Gujarat HC | `IN THE HIGH COURT OF GUJARAT AT AHMEDABAD.` | `Annexure-` | foolscap paper with 2-inch margin (Gujarat HC Rules 1993) |
| Kerala HC | `IN THE HIGH COURT OF KERALA AT ERNAKULAM.` | `Exhibit` (default) or `Annexure-` | foolscap, 4cm outer + 1.5cm inner margins, book-stitched (Kerala HC Rules 1971) |
| Rajasthan HC | `IN THE HIGH COURT OF JUDICATURE FOR RAJASTHAN, JODHPUR.` (Jaipur Bench: `, JAIPUR BENCH, JAIPUR.`) | `Annexure P-` | bench-specific Practice Notes per Jodhpur / Jaipur (Rajasthan HC Rules 1952) |
| Telangana HC | `IN THE HIGH COURT FOR THE STATE OF TELANGANA AT HYDERABAD.` | per Writ Proceeding Rules 1977 | post-2019 separation from AP HC |
| Andhra Pradesh HC | `IN THE HIGH COURT OF ANDHRA PRADESH AT AMARAVATI.` | per Writ Proceeding Rules 1977 + AP Civil Rules of Practice 1990 | post-2019 separation |
| Patna HC | `IN THE HIGH COURT OF JUDICATURE AT PATNA.` | `Annexure P` seriatim (P1, P2, ...) | Chapter IIIA Patna HC Rules + Appendix A(i) civil / A(ii) criminal proforma |
| Orissa HC | `IN THE HIGH COURT OF ORISSA AT CUTTACK.` | `Annexure P/` | distinct cause-title format |
| Gauhati HC | `IN THE GAUHATI HIGH COURT.` | per Gauhati HC PIL Rules 2011 | covers four NE States (Assam, Nagaland, Mizoram, Arunachal Pradesh) |
| Himachal Pradesh HC | `IN THE HIGH COURT OF HIMACHAL PRADESH AT SHIMLA.` | per HP HC Rules | community contribution welcomed |
| J&K and Ladakh HC | `IN THE HIGH COURT OF JAMMU & KASHMIR AND LADAKH.` | per J&K HC Rules | post-2019 reorganisation |
| Jharkhand HC | `IN THE HIGH COURT OF JHARKHAND AT RANCHI.` | per Jharkhand HC Rules | community contribution welcomed |
| Chhattisgarh HC | `IN THE HIGH COURT OF CHHATTISGARH AT BILASPUR.` | per Chhattisgarh HC Rules | community contribution welcomed |
| Madhya Pradesh HC | `IN THE HIGH COURT OF MADHYA PRADESH AT JABALPUR.` (Gwalior / Indore Benches) | per MP HC Rules | community contribution welcomed |
| Uttarakhand HC | `IN THE HIGH COURT OF UTTARAKHAND AT NAINITAL.` | per Uttarakhand HC Rules | community contribution welcomed |
| Manipur HC | `IN THE HIGH COURT OF MANIPUR AT IMPHAL.` | per Manipur HC Rules | post-2013 establishment |
| Meghalaya HC | `IN THE HIGH COURT OF MEGHALAYA AT SHILLONG.` | per Meghalaya HC Rules | post-2013 establishment |
| Sikkim HC | `IN THE HIGH COURT OF SIKKIM AT GANGTOK.` | per Sikkim HC Rules | smallest HC by case volume |
| Tripura HC | `IN THE HIGH COURT OF TRIPURA AT AGARTALA.` | per Tripura HC Rules | post-2013 establishment |

Validation depth taxonomy:
- **Researched · awaiting Registry-acceptance validation:** Bombay ([bench city], Principal, Aurangabad, Goa), Delhi, Karnataka, Madras, Calcutta, Allahabad, Punjab & Haryana, Gujarat, Kerala, Rajasthan, Patna, Orissa, Telangana, Andhra Pradesh — bench-config values sourced from each HC's official Rules + public practice texts; awaiting community Registry-acceptance validation.
- **Stub · community contribution welcomed:** Gauhati, HP, J&K+Ladakh, Jharkhand, Chhattisgarh, MP, Uttarakhand, Manipur, Meghalaya, Sikkim, Tripura.

## ANNEXURE MECHANISM (bench-config-driven)

Inline marker in Facts → consolidated table at end of pleading. The marker style is **bench-config-driven**:

```
{{bench_config.section_header.facts}}

  - "...the Judgment dated <DD.MM.YYYY> ... is annexed herewith and marked as {{bench_config.annexure_prefix}}A."
  - "...the FIR dated <DD.MM.YYYY> is annexed herewith and marked as {{bench_config.annexure_prefix}}B."
  - "...depositions of <N> witnesses are annexed collectively as {{bench_config.annexure_prefix}}C (Colly)."
  - (For Karnataka HC: skip letter I per Writ Proceedings Rules 1977. Use the next letter J directly.)

LIST OF ANNEXURES
| Sr.No | {{bench_config.annexure_column_label}} | Particulars                                | Date          | Pgs |
| 1.    | A                                          | Copy of Judgment ... <Case No./Year>       | <DD.MM.YYYY>  | <N> |
| 2.    | B                                          | Copy of FIR                                 | <DD.MM.YYYY>  | <N> |
| 3.    | C (Colly)                                  | Depositions of <N> witnesses                | various       | <N> |
```

Drafter MUST keep inline markers and List of Annexures in sync. Verifier checks for orphan markers AND checks the bench-specific letter-omission rule (Karnataka HC: letter I).

## STANDARD PLEADING SECTIONS (in order, all in one .docx)

For every Indian HC pleading, the `.docx` contains:

1. **Main pleading** (Cause title → Parties → Statutory opening → Prelude → FACTS → GROUNDS → PRAYER → Counsel block → Notes/Limitation if applicable)
2. **Index** (table form)
3. **Synopsis** (Dates–Events + Points to be Considered + Acts & Rules + Citations)
4. **List of Annexures** (consolidated)
5. **Accompanying applications** (case-type-specific):
   - Criminal Appeal → +Suspension of Sentence (S.389/430 BNSS) +Condonation of Delay (S.5 Lim Act, where late)
   - Civil/Criminal WP → +Stay App (sometimes)
   - First Appeal → +Stay App (sometimes)
   - Bail/ABA/482/Contempt/PIL → typically standalone

Each accompanying application repeats its own cause title (in the bench's idiom), has its own facts, its own prayer, its own counsel block.

## OUTPUT FORMAT

- **File type:** `.docx`
- **Conversion tool:** pandoc (required) with the **shipped** `reference.docx` template at `${CLAUDE_PLUGIN_ROOT}/skills/_hc_pleading_base/reference.docx`. The shipped reference has locked Word styles for Bombay HC formatting (TNR 14pt, 1.5 line spacing, 4cm left margin, A4, Heading 1 = bold centered, Heading 2 = bold centered with letter-spacing). For benches requiring different formatting (Delhi double-spaced, Karnataka I-omission, etc.), the advocate may supply a `<case-folder>/reference.docx` override. **The Drafter MUST use either the shipped or the override — never auto-generate a fresh one in the case folder (that produces the v0.1.0 render defects).**
- **Pandoc invocation:**
  ```bash
  pandoc draft-v1.md -o draft-v1.docx \
    --reference-doc="<shipped or override reference.docx>" \
    --from=markdown+pipe_tables+raw_tex
  ```
- **Output filename convention:** `<case-type>_<draft-version>_<YYYY-MM-DD>.docx`
- **NEVER overwrite an existing draft.** Each run produces a new versioned file.

## PIPELINE-OPTIONALITY (load-bearing — advocate-cost discipline)

The full 6-agent pipeline (Reader → Format → Drafter → Verifier → Refiner → Overseer) is **NOT** mandatory. As of v0.2.0-alpha, only the first three stages are required to produce a filing-grade draft. The remaining three are OPTIONAL quality-control layers that the advocate explicitly invokes.

```
┌────────────────────────────────────────────────────────────┐
│  REQUIRED PIPELINE (default exit point)                     │
│  ─────────────────────────────────────────                  │
│  Stage 1  Reader   →  case-facts.md   (extract & audit)     │
│  Stage 2  Format   →  format-shell.md (bench-substitute)    │
│  Stage 3  Drafter  →  draft-v1.docx   (filing-grade draft)  │
│                                                             │
│  ── default exit ──                                         │
│                                                             │
│  OPTIONAL QC PIPELINE (advocate opts in)                    │
│  ─────────────────────────────────────────                  │
│  Stage 4  Verifier  →  verification-report.md               │
│  Stage 5  Refiner   →  draft-v2.docx                        │
│  Stage 6  Overseer  →  final-draft.docx + opposing-notes.md │
└────────────────────────────────────────────────────────────┘
```

**Why optional:** each stage is itself a Claude subagent run (~80–120K tokens). Running all six on every draft can exhaust an advocate's Claude session limit in a single drafting cycle. The QC stages are valuable for high-stakes matters but disproportionate for routine pleadings.

**When to invoke the QC stages:**
- Verifier: when the brief carries multiple precedent-PDFs and the advocate wants a paragraph-by-paragraph anti-hallucination check.
- Refiner: when the Verifier flagged ≥3 critical issues, or when the advocate wants a polished v2 in a different bench's idiom.
- Overseer: when the matter is materially adversarial (contested final hearing, not chamber motion) and the advocate wants an opposing-counsel pressure-test.

**Default behaviour:** the Drafter signals "READY FOR REVIEW" after writing `draft-v1.docx` and STOPS. The advocate reads the draft and decides whether to invoke the QC stages. Do not auto-chain.

## VERBOSITY DISCIPLINE (load-bearing — Verifier flags bloat)

The Drafter writes formal Indian pleading register, not academic prose. Word-count budgets per case-type:

| Case type | Main pleading target | Hard ceiling |
|---|---|---|
| Civil WP / Criminal WP / Section 482 / PIL / Contempt | 3,500–5,000 words | 6,500 |
| First Appeal / Second Appeal / Criminal Appeal | 4,000–5,500 words | 7,500 |
| Bail / Anticipatory Bail / Criminal Revision | 2,500–3,500 words | 4,500 |
| MACT / MAT OA | 3,000–4,500 words | 6,000 |

Compression rules:
- **One paragraph per ground — not three.** A ground is a single legal proposition with one or two sentences of doctrinal anchor.
- **Ceremonial phrases used sparingly** — "It is most respectfully submitted that…", "By reason of the matters aforesaid…", "In the premises aforesaid…" — these add register, not legal content. Use at most twice per pleading section.
- **Synopsis Dates–Events table = 8–14 rows** — every dated event from `case-facts.md` chronology, deduplicated.
- **Facts paragraphs = numbered, each fact = one paragraph.** No multi-fact paragraphs.
- **If draft exceeds the ceiling, compress before signalling Verifier.** Bloated drafts are pleadings that lose the Court's attention — both a render defect and an advocate-quality defect.

## MARKDOWN-HEADING DISCIPLINE (load-bearing — pandoc reference.docx contract)

Pandoc converts the Drafter's Markdown to `.docx` using the shipped `reference.docx` at `${CLAUDE_PLUGIN_ROOT}/skills/_hc_pleading_base/reference.docx`. The reference.docx has locked Word styles. For the styles to apply, the Drafter MUST use Markdown headings — not plain text — for the structural elements.

See `_hc_pleading_base/SKILL.md` §MARKDOWN HEADING DISCIPLINE for the full convention table. Briefly:

- `# Heading 1` for court header, case-number line, and cover-page anchors of INDEX / SYNOPSIS / LIST OF ANNEXURES.
- `## Heading 2` for `## F A C T S`, `## G R O U N D S`, `## P R A Y E R`, `## I N D E X`, `## S Y N O P S I S`, `## L I S T   O F   A N N E X U R E S`, `## V E R I F I C A T I O N`.
- `### Heading 3` for ground sub-headers, prayer sub-clause anchors, and Accompanying Application titles.
- Tables use pandoc pipe-table syntax with colon-anchored alignment row to control column widths.
- Cover-page discipline: INDEX, SYNOPSIS, LIST OF ANNEXURES each begin on `\newpage` and carry ONLY court header + case-number + short cause-title + section header + table + counsel block. Full party block stays on the Main Petition cover only.

## RECOVERY / AUDIT

If anyone asks "how was this drafted":
1. Show the file chain: `case-facts.md` → `bench-config.md` → `format-shell.md` → `draft-v1.docx` → `verification-report.md` → `draft-v2.docx` → `opposing-notes.md` → `final-draft.docx`
2. Each file has timestamp + agent that produced it
3. Inputs (source PDFs, law PDFs, bench-config) all listed in `case-facts.md` Section 1
4. Bench-config explicitly cites the HC bench's Rules + Practice Notes that anchor the formatting choices

This is the audit-defense kit for any AI-use challenge before any Indian HC.


---

## v0.2.2 OUTPUT-PAIRING DISCIPLINE (load-bearing — every agent must follow)

**Every `.md` output artifact MUST be paired with a `.docx`.** Advocates do not natively read Markdown — they read Word. Every pipeline output (case-facts.md from Reader, format-shell.md from Format, draft-v1.md from Drafter, verification-report.md from Verifier, draft-v2.md from Refiner, opposing-notes.md from Overseer) must have a corresponding `.docx` rendered with the same locked Word styles.

**This plugin produces pleadings** — the shipped reference.docx is the pleading variant (TNR 14pt 1.5 spacing, Heading 2 bold + UNDERLINED + centered with letter-spacing for the spaced `F A C T S` effect).

### How to produce the paired `.docx`

Every agent runs the shipped helper script as its final post-`.md`-write step:

```bash
bash "${CLAUDE_PLUGIN_ROOT}/skills/_hc_pleading_base/pair_md_to_docx.sh" <output.md>
```

The helper:
1. Resolves the reference.docx in `${CLAUDE_PLUGIN_ROOT}/skills/_hc_pleading_base/reference.docx`
2. Runs pandoc with `--reference-doc` and `--from=markdown+pipe_tables+raw_tex` to produce the `.docx`
3. Runs the shipped `fix_docx_tables.py` to force column widths on every table

For overriding (e.g., a per-case-folder reference.docx), pass the reference.docx as the second argument:

```bash
bash "${CLAUDE_PLUGIN_ROOT}/skills/_hc_pleading_base/pair_md_to_docx.sh" \
    <output.md> <case-folder>/reference.docx
```

### Per-agent output-pairing map

| Agent | `.md` output | Paired `.docx` |
|---|---|---|
| Reader | `case-facts.md` | `case-facts.docx` |
| Format | `format-shell.md` | `format-shell.docx` |
| Drafter | `draft-v1.md` | `draft-v1.docx` |
| Verifier | `verification-report.md` | `verification-report.docx` |
| Refiner | `draft-v2.md` | `draft-v2.docx` |
| Overseer | `opposing-notes.md` + `final-draft.md` | `opposing-notes.docx` + `final-draft.docx` |

Every agent calls `pair_md_to_docx.sh` once for each `.md` it writes. Skipping this step leaves the advocate with `.md` files that cannot be opened natively in Word.
