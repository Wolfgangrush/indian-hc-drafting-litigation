# Changelog — `indian-hc-drafting`

All notable changes to this plugin are documented here. Versioning follows [Semantic Versioning](https://semver.org/) (`MAJOR.MINOR.PATCH`) with an `-alpha` / `-beta` suffix during pre-release.

---

## [Unreleased]

### Pending before v0.1.0 stable
- User-paste style references into each case-type skill's `format-from-user.md`
- Bench-config validation pass for Bombay HC Principal Bench (Mumbai), Aurangabad Bench, Goa Bench
- Sample bench-config templates submitted by community contributors for non-Bombay HCs
- First Registry-validation pass on a sample filing at Bombay HC Nagpur

---

## [0.1.0-alpha] — 2026-05-15

### Renamed from `bombay-hc-drafting` to `indian-hc-drafting`

The plugin's scope has been broadened from Bombay HC Nagpur specifically to ALL High Courts of India via the new bench-config architecture. Bombay HC Nagpur remains the most-deeply-validated bench at this milestone; other benches are supported via bench-config supplied by the user at case-folder time. Validation deepening for non-Bombay benches will come from community contribution.

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
