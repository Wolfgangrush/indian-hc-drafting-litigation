# Changelog — `indian-hc-drafting`

All notable changes to this plugin are documented here. Versioning follows [Semantic Versioning](https://semver.org/) (`MAJOR.MINOR.PATCH`) with an `-alpha` / `-beta` suffix during pre-release.

---

## [Unreleased]

### Pending before v0.2.0 stable
- Reader / Format / Drafter context-caching layer so the three stages share one bench-config + skill load instead of three sequential loads
- Optional Haiku-routing for the Reader stage (extraction is pattern-match work, lower-tier-fit)
- Per-case-folder `reference.docx` override mechanism documented end-to-end
- First Registry-validation pass on a sample filing at Bombay HC Nagpur using the v0.2 render path

---

## [0.2.0-alpha] — 2026-05-24

### Critical render-defect repair (from the 2026-05-24 EPFO test run)

The v0.1.0-alpha render path produced filing-grade Markdown but the pandoc → `.docx` conversion failed Bombay HC Registry expectations on multiple counts (title not bold, `F A C T S` rendered left-aligned in plain body text, Index table column-headers wrapping vertically, Petitioner/Respondent block leaking onto Index cover page, INDEX rendered in blue Markdown-style heading, ~6,200-word bloat for a single-issue WP). This release repairs the render path.

### Added

- **Pre-customised Bombay HC Nagpur `reference.docx`** at `skills/_hc_pleading_base/reference.docx` with locked Word styles:
  - Body (Normal): TNR 14pt, 1.5 line spacing, justified, 0.5cm first-line indent
  - Heading 1: TNR 14pt **bold centered** (for court header, case-number line, cover-page anchors)
  - Heading 2: TNR 14pt **bold centered with letter-spacing** (renders `F A C T S` / `G R O U N D S` / `P R A Y E R` etc. correctly)
  - Heading 3: TNR 14pt **bold left-aligned** (for ground sub-headers, application titles)
  - Title style: TNR 14pt bold centered
  - Tables: `tblLayout = fixed` so pipe-table column proportions are honoured
  - Page setup: A4, 4cm left / 2.5cm right / 2.5cm top / 2.5cm bottom margins
  - Page numbers: centred at bottom, TNR 11pt
- **`build_reference_docx.py`** — reproducible build script for the shipped reference.docx. Plugin maintainers re-run this when styles need updating; advocates do not run it directly.
- **MARKDOWN HEADING DISCIPLINE** section in `_hc_pleading_base/SKILL.md` documenting the Markdown → Word-style mapping the Drafter must follow.
- **VERBOSITY DISCIPLINE** section in `_drafting_common/SKILL.md` setting per-case-type word-count targets and hard ceilings (Civil/Criminal WP target 3,500–5,000 words, hard ceiling 6,500).
- **PIPELINE-OPTIONALITY** section in `_drafting_common/SKILL.md` documenting Stages 4–6 (Verifier / Refiner / Overseer) as OPTIONAL QC layers. Default exit point is now after Stage 3 (Drafter) — advocate opts in to the QC stages.
- **COVER-PAGE DISCIPLINE** rule in `_hc_pleading_base/SKILL.md` — Index, Synopsis, and List of Annexures each begin on a new page and carry ONLY court header + case-number + short cause-title + section header + table + counsel block. Full Petitioner/Respondent address block stays on the Main Petition cover only.

### Changed

- **Skeleton in `_hc_pleading_base/SKILL.md`** rewritten to use Markdown headings (`# Court header`, `## F A C T S`, etc.) instead of plain text. Pandoc now maps the headings to the locked Word styles in `reference.docx`.
- **Drafter agent prompt in `agents/drafter/drafter.md`** extended with explicit instructions to: use Markdown headings; use the shipped reference.docx (not auto-generate one); honour verbosity ceilings; follow cover-page discipline; use pandoc pipe-table syntax with colon-anchored alignment row for fixed column widths.
- **Pandoc invocation documented end-to-end** in `_drafting_common/SKILL.md` §OUTPUT FORMAT. Required pandoc command:
  ```bash
  pandoc draft-v1.md -o draft-v1.docx \
    --reference-doc="${CLAUDE_PLUGIN_ROOT}/skills/_hc_pleading_base/reference.docx" \
    --from=markdown+pipe_tables+raw_tex
  ```

### Removed

- The auto-generation of a fresh `reference.docx` in the case-folder output directory (this was the source of the v0.1.0 render defects). Drafter now uses the shipped reference.docx or a per-case override only.
- The "Triple-verify is mandatory" framing from `_drafting_common/SKILL.md` — replaced with explicit OPTIONAL framing per the new Pipeline-optionality section.

### Migration note

Existing case folders produced under v0.1.0 are unaffected; their draft-v1.docx outputs remain on disk. To re-render a v0.1.0 draft using the v0.2.0 styles, re-run the Drafter on the existing `case-facts.md` + `format-shell.md`. The new reference.docx will produce a correctly-formatted draft.

### Cost / token-budget note

Running the full 6-agent pipeline burns approximately 600K tokens per draft, which can exhaust an advocate's Claude session limit in one drafting cycle. v0.2.0 makes Stages 4–6 OPTIONAL so a baseline Reader → Format → Drafter run (~280K tokens) is sufficient for routine pleadings. The optional QC stages remain available for high-stakes matters. v0.3 will add context-caching across Stages 1–3 to reduce the baseline further.

---

## [0.1.0-alpha] — 2026-05-15

### Renamed from `bombay-hc-drafting` to `indian-hc-drafting`

The plugin's scope has been broadened from Bombay HC Nagpur specifically to ALL High Courts of India via the new bench-config architecture. Per-bench specifics are supplied by the user via a `bench-config.md` file in the user's case folder at case-folder time. Registry-acceptance validation per bench will come from community contribution.

### Added (over and above the prior `bombay-hc-drafting` content)

#### Bench-config architecture
- `bench-config/bench-config-template.md` — twelve-section template for users to fill in their specific HC bench's procedural conventions:
  - Court identification (HC name, bench, Court header text)
  - Procedural Rules (Appellate Side / Original Side / PIL Rules)
  - Cause Title and Parties (case-number format, parties separator)
  - Section header style (spaced / title-case)
  - Salutation and connective phrases
  - Annexure marker convention
  - Counsel block layout
  - Affidavit dispensation note
  - Paper size and Registry formatting (paper, font, margins)
  - Accompanying-application requirements per case type
  - Limitation references
  - State Court-Fees Act citation

The user copies the template into their case folder, fills in values, and the plugin's Format agent reads it at run-time.

#### Documentation
- `README.md` — rewritten for multi-bench scope; bench coverage table with validation-depth honest declarations; vendor-neutral installation instructions
- `NOTICE.md` — to be updated for multi-bench scope (see "Pending" below)
- `CHANGELOG.md` — this file
- `USAGE.md` — to be added for end-user installation and invocation guide
- `_hc_pleading_base/REFERENCE-DOCX-CUSTOMISATION.md` — to be added for pandoc reference template customisation guide

### Preserved (from the prior `bombay-hc-drafting` content)

#### Shared infrastructure
- `skills/_drafting_common/SKILL.md` — anti-pollution rules, HC AI-use risk constraints, Bombay HC formatting conventions (to be made bench-config-aware in v0.1.0)
- `skills/_hc_pleading_base/SKILL.md` — universal HC pleading skeleton (to be made bench-config-aware in v0.1.0)

#### Thirteen case-type skills
- `skills/pil-draft/` — Public Interest Litigation under Article 226
- `skills/civil-wp-draft/` — Civil Writ Petition under Articles 226 / 227
- `skills/criminal-wp-draft/` — Criminal Writ Petition
- `skills/criminal-appeal-draft/` — Appeal against conviction
- `skills/application-482-draft/` — Application under Section 482 CrPC / Section 528 BNSS
- `skills/anticipatory-bail-draft/` — Anticipatory Bail under Section 438 CrPC / Section 482 BNSS
- `skills/bail-draft/` — Regular Bail under Section 439 CrPC / Section 483 BNSS
- `skills/contempt-petition-draft/` — Civil and Criminal Contempt
- `skills/first-appeal-draft/` — First Appeal (Civil)
- `skills/second-appeal-draft/` — Second Appeal (Civil)
- `skills/criminal-revision-draft/` — Sections 397/401 CrPC / Sections 438/442 BNSS
- `skills/mact-draft/` — Motor Accident Claims Tribunal claim petition
- `skills/mat-draft/` — Matrimonial petitions (HMA / SMA / divorce / RCR / maintenance)

#### Six-agent drafting pipeline
- `agents/reader/reader.md`
- `agents/format/format.md`
- `agents/drafter/drafter.md`
- `agents/verifier/verifier.md`
- `agents/refiner/refiner.md`
- `agents/overseer/overseer.md`

### Migration note for users of the prior `bombay-hc-drafting` plugin

Users who installed the earlier `bombay-hc-drafting` plugin should:
1. Uninstall the prior plugin from their Anthropic plugins folder.
2. Install `indian-hc-drafting` from this repository.
3. Copy `bench-config/bench-config-template.md` into each existing case folder and fill in the Bombay HC Nagpur values (default values in the template are already Bombay HC Nagpur — minimal edits needed).
4. Re-run the pipeline on the case folder.

No case-folder content needs to be migrated. Only the bench-config addition is required.

### Quality-gate audit (per `05-quality-gates.md` of the India-Legal Corpus Pipeline)

- Gate 1 · Copyright firewall — ✅ PASS (zero corpus prose transcribed; only public-domain statutory recitations verbatim)
- Gate 2 · Rule 36 BCI firewall — ✅ PASS
- Gate 3 · NOTICE.md doctrine — ✅ PASS
- Gate 4 · Statute currency — ✅ PASS (BNSS / BSA / BNS dual-citation enforced)
- Gate 5 · Bench scope honesty — ✅ PASS (bench-coverage validation depth declared honestly per HC; Bombay HC Nagpur deep, others bench-config-supported pending validation)
- Gate 6 · Falsification triggers — ✅ PASS

### Provenance

Patterns encoded in this plugin trace to public-domain procedural authority only. Bombay HC Nagpur conventions are validated against the Bombay High Court (Appellate Side) Rules 1960 + the Bombay High Court (Original Side) Rules + the Bombay HC Civil Manual + the Bombay HC Criminal Manual. Non-Bombay bench-config support relies on the user supplying the relevant bench's Rules / Practice Notes at case-folder time.

No drafted prose has been transcribed from any third-party advocate's drafts.
