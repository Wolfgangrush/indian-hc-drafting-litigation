# indian-hc-drafting

> **Open-source Claude-compatible plugin for drafting pleadings before any High Court of India.**
>
> Six-agent drafting pipeline · thirteen case-type skills · bench-config-aware across all twenty-five Indian High Courts.
>
> Released under MIT. Open infrastructure for the legal community. No commercial engagement offered through this repository — see Disclaimer below.

---

## Table of contents

1. [What this plugin does](#what-this-plugin-does)
2. [Bench coverage — all 25 Indian High Courts](#bench-coverage--all-25-indian-high-courts)
3. [Case-type skills (full inventory with statutory authority)](#case-type-skills-full-inventory)
4. [The 6-agent drafting pipeline (what each agent does)](#the-6-agent-drafting-pipeline)
5. [Installation](#installation) — Claude Desktop application
6. [Your first pleading — step-by-step walkthrough](#your-first-pleading--step-by-step-walkthrough)
7. [The `bench-config.md` file — how bench customisation works](#the-bench-configmd-file)
8. [Why MIT License (and not Apache 2.0, GPL, or anything else)](#why-mit-license)
9. [Sibling plugins (Wolfgang Rush legal-tech family)](#sibling-plugins)
10. [Why this exists](#why-this-exists)
11. [Roadmap](#roadmap)
12. [Contributing](#contributing)
13. [Contact](#contact)
14. [Author and brand](#author-and-brand)
15. [Provenance and privilege statement](#provenance-and-privilege-statement)
16. [Disclaimer and Bar Council of India Rule 36 compliance](#disclaimer-and-bar-council-of-india-rule-36-compliance)
17. [License](#license)

---

## What this plugin does

This plugin lets an Indian advocate, sitting inside the Claude Desktop application, point to a case folder on disk and obtain a complete High-Court pleading in `.docx` form — Cause Title, Facts, Grounds, Prayer, Verification, Index, Synopsis, List of Annexures, and the accompanying applications (stay / condonation of delay / exemption / urgency) — formatted in the **specific High Court bench's idiom** sourced from a `bench-config.md` file the user places in the case folder.

The pipeline is six agents running in sequence:

1. **Reader** — extracts facts from the case folder with a per-document audit log, identifies annexure candidates, and halts if any required statute PDF is missing.
2. **Format** — loads the case-type-specific skill template (e.g. `pil-draft`, `bail-draft`), reads the user's bench-config, substitutes the Court header / parties-separator / annexure-prefix / paper-size, and emits a `format-shell.md` ready for the Drafter.
3. **Drafter** — writes the actual narrative — Facts paragraphs with inline annexure markers, Grounds per the case-type structure, Prayer, Index, Synopsis, List of Annexures, and any accompanying application that the facts require. Outputs `draft-v1.docx` and `draft-v1.md`.
4. **Verifier** — anti-hallucination firewall. Compares every fact in the draft against the Reader's extracted `case-facts.md` line-by-line. Flags fabricated dates, mis-cited sections, orphan annexure markers, and unsupported assertions.
5. **Refiner** — applies Verifier flags, polishes language, enforces HC Registry formatting per the bench-config, strips AI-style markers (em-dashes / "moreover" / "furthermore" / "navigate" / etc.).
6. **Overseer** — reads the polished draft with an opposing-counsel lens. Flags weak prayers, contradictory facts, attackable defects, missing limbs of argument. Outputs `opposing-notes.md` and the final draft.

A built-in **code-substitution privacy firewall** replaces real client names with structural placeholders during drafting, so the underlying AI model never processes raw personal data; the final draft re-substitutes the real names locally on the user's machine.

The output is what an advocate would file before an Indian High Court. **Not a template. Not a checklist. A pleading** — ready for the advocate's review, professional verification, signature, and filing.

---

## Bench coverage — all 25 Indian High Courts

India has **twenty-five High Courts** under Article 214 and Article 231 of the Constitution. This plugin supports all of them through a bench-config architecture: the structural skeleton of any HC pleading is uniform (Cause Title → Parties → Statutory Opening → Prelude → Facts → Grounds → Prayer → Verification → Counsel block → Index → Synopsis → List of Annexures), and the bench-specific elements (Court header text, Appellate-Side / Original-Side Rules reference, annexure-marker convention, paper-size / font preference, section-headers style, prayer catchall) are supplied by the user via a `bench-config.md` file in the case folder.

The plugin ships with **28 ready-to-copy bench-config exemplars** — one per High Court, plus three additional Bombay HC sub-benches (Principal Bench at Mumbai, Nagpur Bench, Aurangabad Bench, Goa Bench at Panaji).

| # | High Court | Seat | Bench-config exemplar | Validation depth at v0.1.0-alpha |
|---|---|---|---|---|
| 1 | **Bombay High Court — Nagpur Bench** | Nagpur | `bench-config/exemplars/bombay-hc-nagpur.md` | **Deep · battle-tested** (author's primary practice court) |
| 2 | **Bombay High Court — Principal Bench (Mumbai)** | Mumbai | `bench-config/exemplars/bombay-hc-principal-mumbai.md` | bench-config supported · validation deepening v0.1.x |
| 3 | **Bombay High Court — Aurangabad Bench** | Aurangabad | `bench-config/exemplars/bombay-hc-aurangabad.md` | bench-config supported · validation deepening v0.1.x |
| 4 | **Bombay High Court — Goa Bench (Panaji)** | Panaji | `bench-config/exemplars/bombay-hc-goa.md` | bench-config supported · validation deepening v0.1.x |
| 5 | **Allahabad High Court** | Prayagraj (with circuit bench at Lucknow) | `bench-config/exemplars/allahabad-hc.md` | bench-config supported · community contribution welcomed |
| 6 | **Andhra Pradesh High Court** | Amaravati | `bench-config/exemplars/andhra-pradesh-hc.md` | bench-config supported · community contribution welcomed |
| 7 | **Calcutta High Court** | Kolkata (with circuit benches at Port Blair and Jalpaiguri) | `bench-config/exemplars/calcutta-hc.md` | bench-config supported · community contribution welcomed |
| 8 | **Chhattisgarh High Court** | Bilaspur | `bench-config/exemplars/chhattisgarh-hc.md` | bench-config supported · community contribution welcomed |
| 9 | **Delhi High Court** | New Delhi | `bench-config/exemplars/delhi-hc.md` | bench-config supported · community contribution welcomed |
| 10 | **Gauhati High Court** | Guwahati (with benches at Kohima, Aizawl, Itanagar) | `bench-config/exemplars/gauhati-hc.md` | bench-config supported · community contribution welcomed |
| 11 | **Gujarat High Court** | Ahmedabad | `bench-config/exemplars/gujarat-hc.md` | bench-config supported · community contribution welcomed |
| 12 | **Himachal Pradesh High Court** | Shimla | `bench-config/exemplars/himachal-pradesh-hc.md` | bench-config supported · community contribution welcomed |
| 13 | **Jammu and Kashmir and Ladakh High Court** | Srinagar and Jammu (with bench at Leh) | `bench-config/exemplars/jammu-kashmir-ladakh-hc.md` | bench-config supported · community contribution welcomed |
| 14 | **Jharkhand High Court** | Ranchi | `bench-config/exemplars/jharkhand-hc.md` | bench-config supported · community contribution welcomed |
| 15 | **Karnataka High Court** | Bengaluru (with circuit benches at Dharwad and Kalaburagi) | `bench-config/exemplars/karnataka-hc.md` | bench-config supported · community contribution welcomed |
| 16 | **Kerala High Court** | Kochi (Ernakulam) | `bench-config/exemplars/kerala-hc.md` | bench-config supported · community contribution welcomed |
| 17 | **Madhya Pradesh High Court** | Jabalpur (with benches at Indore and Gwalior) | `bench-config/exemplars/madhya-pradesh-hc.md` | bench-config supported · community contribution welcomed |
| 18 | **Madras High Court** | Chennai (with circuit bench at Madurai) | `bench-config/exemplars/madras-hc.md` | bench-config supported · community contribution welcomed |
| 19 | **Manipur High Court** | Imphal | `bench-config/exemplars/manipur-hc.md` | bench-config supported · community contribution welcomed |
| 20 | **Meghalaya High Court** | Shillong | `bench-config/exemplars/meghalaya-hc.md` | bench-config supported · community contribution welcomed |
| 21 | **Orissa High Court** | Cuttack | `bench-config/exemplars/orissa-hc.md` | bench-config supported · community contribution welcomed |
| 22 | **Patna High Court** | Patna | `bench-config/exemplars/patna-hc.md` | bench-config supported · community contribution welcomed |
| 23 | **Punjab and Haryana High Court** | Chandigarh | `bench-config/exemplars/punjab-haryana-hc.md` | bench-config supported · community contribution welcomed |
| 24 | **Rajasthan High Court** | Jodhpur (with bench at Jaipur) | `bench-config/exemplars/rajasthan-hc.md` | bench-config supported · community contribution welcomed |
| 25 | **Sikkim High Court** | Gangtok | `bench-config/exemplars/sikkim-hc.md` | bench-config supported · community contribution welcomed |
| 26 | **Telangana High Court** | Hyderabad | `bench-config/exemplars/telangana-hc.md` | bench-config supported · community contribution welcomed |
| 27 | **Tripura High Court** | Agartala | `bench-config/exemplars/tripura-hc.md` | bench-config supported · community contribution welcomed |
| 28 | **Uttarakhand High Court** | Nainital | `bench-config/exemplars/uttarakhand-hc.md` | bench-config supported · community contribution welcomed |

*Note: row 6 (AP HC) and row 26 (Telangana HC) reflect the post-bifurcation (2019) reality. The Calcutta HC's territorial jurisdiction extends to the Union Territory of the Andaman and Nicobar Islands; the Madras HC's extends to Puducherry; the Kerala HC's extends to Lakshadweep — these are handled through bench-config overlay.*

**How to use a bench-config:** copy the appropriate exemplar from `bench-config/exemplars/` into your case folder, rename it to `bench-config.md`, edit any values that have changed (e.g. if the bench has issued a new Practice Direction), and the plugin renders the pleading in that bench's idiom automatically.

---

## Case-type skills (full inventory)

The plugin ships **thirteen case-type skills**, each grounded in the statutory authority below. Each skill encodes the case-type-specific structure that the Drafter agent uses; the Format agent layers the bench-config on top.

### 1. `pil-draft` — Public Interest Litigation (Article 226)

**Statutory authority:** Article 226 of the Constitution + the *PIL Rules* of the specific High Court (e.g. Bombay HC Public Interest Litigation Rules 2010). **Use case:** writ for enforcement of fundamental rights or statutory rights affecting the public at large, or a class of persons unable to approach the Court themselves. **Facts the skill asks for:** locus standi affidavit basis, the public-rights violation, the respondent authority's failure to act, the prior representations made (if any), the prayer (mandamus / certiorari / prohibition / quo warranto / specific direction). **Output:** complete PIL ready to file, with the bench's mandatory PIL-checklist annexure and the PIL Rules disclosures pre-filled.

### 2. `civil-wp-draft` — Civil Writ Petition (Articles 226 / 227)

**Statutory authority:** Articles 226 and 227 of the Constitution. **Use case:** writ in civil matters — service-law disputes, regulatory orders, education law, property challenges to authority action, certiorari against quasi-judicial tribunals, mandamus to compel statutory duty. **Facts the skill asks for:** the impugned action / order, the statutory framework, the alternative-remedy position (and why this remedy is more efficacious), the violation of statutory or constitutional right. **Output:** complete civil writ with grounds laid out under specific Article-226 limbs (*violation of Article 14 / 19 / 21*, *jurisdictional excess*, *natural justice failure*, *patent illegality*, *no alternative remedy*).

### 3. `criminal-wp-draft` — Criminal Writ Petition

**Statutory authority:** Article 226 + Article 21 of the Constitution + the inherent jurisdiction recognised by the SC in *State of Haryana v. Bhajan Lal (1992) Supp. 1 SCC 335*. **Use case:** writ for quashing of FIR / quashing of chargesheet / habeas corpus / preventive-detention challenge / regulatory-criminal-process challenge. **Facts the skill asks for:** the FIR / proceeding details, the *Bhajan Lal* category invoked, the constitutional violation. **Output:** complete criminal writ with the *Bhajan Lal* ground-structure pre-mapped.

### 4. `criminal-appeal-draft` — Criminal Appeal

**Statutory authority:** Section 374 / Section 386 CrPC 1973 (or Section 415 / Section 427 BNSS 2023, as applicable to the date of the impugned order). **Use case:** appeal against a conviction or sentence passed by a Sessions Court or Special Court. **Facts the skill asks for:** the trial-court judgment under challenge, the prosecution case (in summary), the defence case (in summary), the points for determination, the grounds of appeal. **Output:** complete criminal appeal with the Memo of Appeal + grounds + accompanying applications (suspension of sentence / bail pending appeal, where the case requires).

### 5. `application-482-draft` — Application u/s 482 CrPC / Section 528 BNSS

**Statutory authority:** Section 482 CrPC 1973 / Section 528 BNSS 2023 — the inherent powers of the High Court. **Use case:** quashing of FIR / proceedings under the *Bhajan Lal* categories; preventing abuse of process; securing the ends of justice. **Facts the skill asks for:** the FIR / proceeding, the *Bhajan Lal* category invoked, the supporting documents (settlement deed, repayment receipt, complainant's affidavit, etc. as relevant). **Output:** complete Section 482 / 528 application ready to file.

### 6. `anticipatory-bail-draft` — Anticipatory Bail (Section 438 CrPC / Section 482 BNSS)

**Statutory authority:** Section 438 CrPC 1973 / Section 482 BNSS 2023. **Use case:** pre-arrest bail in anticipation of arrest on a non-bailable charge. **Facts the skill asks for:** the FIR particulars, the offence and sentencing range, the applicant's antecedents, the apprehension of arrest, the parameters under *Siddharam Satlingappa Mhetre v. State of Maharashtra (2011) 1 SCC 694*. **Output:** complete anticipatory-bail application with the *Mhetre* parameters mapped to the facts.

### 7. `bail-draft` — Regular Bail (Section 439 CrPC / Section 483 BNSS)

**Statutory authority:** Section 439 CrPC 1973 / Section 483 BNSS 2023. **Use case:** regular bail by an arrested accused. **Facts the skill asks for:** the FIR particulars, the offence, the period in custody, the parameters under *Sanjay Chandra v. CBI (2012) 1 SCC 40*, the medical / age / family / overcharging grounds, any prior bail rejection orders. **Output:** complete regular-bail application ready to file.

### 8. `contempt-petition-draft` — Civil and Criminal Contempt

**Statutory authority:** Contempt of Courts Act 1971 + Article 215 of the Constitution + the Rules of the specific High Court for Contempt Proceedings (e.g. *Bombay High Court (Contempt of Court Proceedings) Rules 1994*). **Use case:** civil contempt (wilful disobedience of court order) or criminal contempt (scandalising the court / obstruction of justice). **Facts the skill asks for:** the order alleged to be disobeyed, the disobedience particulars, the consent of Advocate General (for criminal contempt) where required. **Output:** complete contempt petition + supporting affidavit + statutory disclosures.

### 9. `first-appeal-draft` — First Appeal (Civil)

**Statutory authority:** Section 96 CPC 1908 + Order XLI CPC. **Use case:** first appeal from a decree of a District Court / Civil Judge (Senior Division) to the High Court in civil matters. **Facts the skill asks for:** the suit, the trial decision, the points for determination, the grounds of appeal under Section 96 / Order XLI. **Output:** complete first appeal with Memo of Appeal + grounds + accompanying applications (stay of execution / condonation of delay / etc.).

### 10. `second-appeal-draft` — Second Appeal (Civil)

**Statutory authority:** Section 100 CPC 1908 + Order XLII CPC. **Use case:** second appeal from a first-appellate decree, on a substantial question of law. **Facts the skill asks for:** the trial decree, the first-appellate decree, the substantial question of law proposed, the case-law on the question. **Output:** complete second appeal with the substantial-question-of-law proposition front-loaded as Section 100 mandates.

### 11. `criminal-revision-draft` — Criminal Revision (Section 397 / 401 CrPC / Sections 438 / 442 BNSS)

**Statutory authority:** Sections 397, 401 CrPC 1973 / Sections 438, 442 BNSS 2023. **Use case:** revision against interlocutory or final orders not amenable to appeal — discharge, framing of charge, summoning order, sentence revision, etc. **Facts the skill asks for:** the impugned order, the revisional limb invoked (jurisdiction / illegality / propriety), the supporting case-law. **Output:** complete criminal revision with grounds mapped to Section 397 limbs.

### 12. `mact-draft` — Motor Accident Claims Tribunal claim petition

**Statutory authority:** Sections 165, 166 of the Motor Vehicles Act 1988 + the Claims Tribunal Rules of the relevant State. **Use case:** claim for compensation arising out of a motor-vehicle accident. **Facts the skill asks for:** the accident particulars (date, time, place, vehicle numbers, drivers, FIR), the injury / death particulars, the deceased's / injured's income basis, the dependents (for fatal claims), the insurance position. **Output:** complete MACT claim petition with the *Sarla Verma v. DTC (2009) 6 SCC 121* + *National Insurance v. Pranay Sethi (2017) 16 SCC 680* compensation-computation matrix applied.

### 13. `mat-draft` — Matrimonial petitions

**Statutory authority:** Hindu Marriage Act 1955 (HMA) / Special Marriage Act 1954 (SMA) / Indian Christian Marriage Act 1872 / Family Courts Act 1984 / Section 125 CrPC and Section 144 BNSS / Protection of Women from Domestic Violence Act 2005. **Use case:** divorce, restitution of conjugal rights, judicial separation, nullity, maintenance, custody, domestic-violence reliefs — at the High Court level (e.g. transfer of matrimonial proceedings, appeal from Family Court orders). **Facts the skill asks for:** the marriage particulars, the ground invoked, the relief sought, the dependent particulars. **Output:** complete matrimonial petition or appeal in the High Court's matrimonial idiom.

### Shared infrastructure skills

- **`_drafting_common`** — anti-pollution rules, encoding standards, language conventions, AI-style-marker blacklist, citation discipline, common phrases.
- **`_hc_pleading_base`** — universal High Court pleading skeleton (Cause Title template, parties block, statutory opening, prelude, prayer template, verification clause, counsel block, index template, synopsis template, list of annexures template) — reads bench-specific values from the user's `bench-config.md`.

---

## The 6-agent drafting pipeline

The plugin is built on the **Anthropic Agent SDK** convention — six markdown agent files (`agents/<name>/<name>.md`) with YAML frontmatter declaring `name`, `description`, and `allowed-tools`. Each agent is invoked in sequence on a case folder and reads/writes specific files in that folder.

### 1. `reader` — first agent

**What it reads:**
- Every file in the case folder (`*.pdf`, `*.docx`, `*.txt`, `*.md`, `*.eml`, scanned images via OCR where present)
- The case-type skill instruction (e.g. `skills/pil-draft/case-facts-questions.md`)

**What it writes:**
- `case-folder/case-facts.md` — extracted facts with per-document audit log
- `case-folder/annexure-candidates.md` — which documents map to which proposed annexures (A, B, C, ...)
- `case-folder/missing-laws.md` — list of statutes referenced but not supplied as PDFs (if any required law is missing, the Reader halts and asks the user to supply the PDF before the pipeline proceeds)

**Why it exists:** without a faithful fact-extraction step, the Drafter would either hallucinate facts or process raw client documents through the AI — both of which the plugin prevents.

**Skills loaded:** `_drafting_common` (for AAAK-substitution / privacy firewall rules) + the specific case-type skill's `case-facts-questions.md`.

### 2. `format` — second agent

**What it reads:**
- `case-folder/case-facts.md` (from Reader)
- `case-folder/bench-config.md` (user-supplied)
- `skills/<case-type>-draft/SKILL.md` and `skills/<case-type>-draft/format-from-user.md`
- `skills/_hc_pleading_base/SKILL.md`
- The relevant bench exemplar at `bench-config/exemplars/<hc>.md` (for reference)

**What it writes:**
- `case-folder/format-shell.md` — the case-type template with all bench-specific values (Court header, parties-separator, annexure-prefix, paper-size, section-headers style, prayer catchall) substituted from the bench-config

**Why it exists:** the Drafter should not have to handle bench-specific formatting decisions inline. The Format agent pre-substitutes everything that depends on which bench you are filing in, so the Drafter can focus entirely on writing the narrative.

**Skills loaded:** `_hc_pleading_base` + the case-type skill (e.g. `pil-draft`).

### 3. `drafter` — third agent

**What it reads:**
- `case-folder/case-facts.md`
- `case-folder/format-shell.md`
- `case-folder/bench-config.md`
- `skills/<case-type>-draft/SKILL.md` (for the case-type-specific Facts/Grounds/Prayer structure)
- `skills/_hc_pleading_base/SKILL.md`
- Law PDFs in `case-folder/laws/` (for citing exact section text)

**What it writes:**
- `case-folder/draft-v1.md` — full markdown intermediate
- `case-folder/draft-v1.docx` — final form, generated from markdown via pandoc using the bench's reference template

**Why it exists:** this is the actual drafting brain. It writes Facts paragraphs in narrative form (not bullet-point summary), Grounds in the case-type-specific structure, Prayer with primary + interim reliefs, Index, Synopsis, List of Annexures, and any accompanying applications the facts require.

**Skills loaded:** `_drafting_common` (style + anti-pollution rules) + `_hc_pleading_base` (skeleton) + the case-type skill.

### 4. `verifier` — fourth agent

**What it reads:**
- `case-folder/draft-v1.md`
- `case-folder/case-facts.md`
- The law PDFs in `case-folder/laws/`

**What it writes:**
- `case-folder/verification-report.md` — fact-by-fact comparison, flagging:
  - Fabricated dates (date appears in draft but not in case-facts)
  - Mis-cited sections (statute section in draft doesn't match the law PDF)
  - Orphan annexure markers (`ANNEXURE-D` referenced in text but D not in the annexure list)
  - Unsupported assertions (claim in draft without corresponding fact in case-facts)
  - Hallucinated citations (case name + citation not traceable to a user-supplied source)

**Why it exists:** the Verifier is the anti-hallucination firewall. Without it, the plugin would be no safer than asking a general-purpose AI to draft. With it, the plugin can be trusted to produce drafts that the advocate can verify in minutes rather than hours.

**Skills loaded:** `_drafting_common` (verification ruleset).

### 5. `refiner` — fifth agent

**What it reads:**
- `case-folder/draft-v1.md`
- `case-folder/verification-report.md`
- `case-folder/bench-config.md`

**What it writes:**
- `case-folder/draft-v2.md`
- `case-folder/draft-v2.docx`

**Why it exists:** applies the Verifier's flags (corrects fabrications, fixes citations, removes orphan markers), polishes the language (removes AI-style markers like *moreover*, *furthermore*, *navigate*, em-dashes, sentence-final *thereby*; enforces HC formal register — *that*, *whereas*, *it is most respectfully submitted*), and enforces the bench's Registry formatting (paper size, font, line spacing, margins per the bench-config).

**Skills loaded:** `_drafting_common` (style enforcement) + `_hc_pleading_base` (formatting).

### 6. `overseer` — sixth and final agent

**What it reads:**
- `case-folder/draft-v2.md`
- `case-folder/case-facts.md`

**What it writes:**
- `case-folder/opposing-notes.md` — attackable defects, weak prayers, missing limbs, contradictory facts, ground-by-ground critique from an opposing-counsel lens
- `case-folder/final-draft.docx` (a copy of `draft-v2.docx` with any final hardening applied)

**Why it exists:** because the strongest test of a pleading is what an opposing counsel would say. The Overseer reads the draft as if it had been served on her, and writes a critique. The advocate uses that critique to harden the draft before signing.

**Skills loaded:** `_drafting_common` (opposing-counsel ruleset).

---

## Installation

This is a Claude-compatible plugin in the Anthropic plugin format, designed to run inside the **Claude Desktop application** (available at <https://claude.ai/download>). The plugin folder location depends on your OS:

| OS | Plugin folder path |
|---|---|
| **macOS** | `~/Library/Application Support/Claude/plugins/` |
| **Windows** | `%APPDATA%\Claude\plugins\` (typically `C:\Users\<you>\AppData\Roaming\Claude\plugins\`) |
| **Linux** | `~/.config/Claude/plugins/` |

Clone the plugin into that folder:

```bash
# macOS / Linux
mkdir -p ~/Library/Application\ Support/Claude/plugins   # adjust per OS table
cd ~/Library/Application\ Support/Claude/plugins
git clone https://github.com/Wolfgangrush/indian-hc-drafting-litigation.git indian-hc-drafting

# Windows (PowerShell)
mkdir -Force $env:APPDATA\Claude\plugins
cd $env:APPDATA\Claude\plugins
git clone https://github.com/Wolfgangrush/indian-hc-drafting-litigation.git indian-hc-drafting
```

Restart the Claude Desktop application. The plugin will be auto-discovered on the next session start.

### Anthropic Plugin Marketplace (when available)

When the plugin lands on the Anthropic Plugin Marketplace, you will be able to install it from inside the application's plugin browser without using `git` directly. Until then, the manual clone steps above are the canonical install method.

### Verifying the install

In a Claude session, type any of the following:

- *"draft criminal appeal"* — should trigger `criminal-appeal-draft`
- *"draft second appeal"* — should trigger `second-appeal-draft`
- *"draft application 482"* — should trigger `application-482-draft`
- `/criminal-appeal-draft` — explicit slash-invocation

Claude should respond by reading the skill's instructions and asking you for the case folder path or for the case-specific facts. If Claude does not pick up the skill, restart the Desktop app and confirm the plugin folder is at the correct path.

---

## Your first pleading — step-by-step walkthrough

Suppose you wish to draft a **Criminal Appeal** before the **Allahabad High Court** against a conviction order passed by the Sessions Court.

### Step 1 — create a case folder

```
~/Desktop/cases/
└── crl-appeal-CASE-NUMBER/
    ├── bench-config.md           ← copied from bench-config/exemplars/allahabad-hc.md
    ├── facts/
    │   ├── trial-court-judgment-DD.MM.YYYY.pdf
    │   ├── charge-sheet-DD.MM.YYYY.pdf
    │   ├── prosecution-evidence-summary.pdf
    │   ├── defence-evidence-summary.pdf
    │   └── sentence-order-DD.MM.YYYY.pdf
    ├── laws/
    │   ├── crpc-1973.pdf
    │   ├── bnss-2023.pdf
    │   └── ipc-1860.pdf
    └── notes.md                   ← your free-form notes
```

### Step 2 — copy the bench-config exemplar

In the Claude application's file browser, navigate to the plugin's folder and copy the bench-config exemplar for your bench:

```
plugin_folder/bench-config/exemplars/allahabad-hc.md  →  case_folder/bench-config.md
```

Open `bench-config.md` in any text editor and verify the values (Court header, parties-separator, annexure-prefix, paper-size, etc.). Edit any value that has changed per a recent Practice Direction issued by your bench.

### Step 3 — open the case folder in Claude

In the Claude Desktop application, point Claude at the case folder using the application's file-browser feature.

### Step 4 — invoke the skill

```
draft criminal appeal
```

The plugin will run the **Reader** agent first — it will read your case folder, extract facts, write `case-facts.md` and `annexure-candidates.md`, and halt if any required law PDF is missing.

Review `case-facts.md`. Add anything the Reader missed. Save.

### Step 5 — continue the pipeline

The plugin will then run **Format → Drafter → Verifier → Refiner → Overseer** in sequence. At the end, you will have:

- `draft-v1.md` and `draft-v1.docx` — initial draft
- `verification-report.md` — Verifier flags
- `draft-v2.md` and `draft-v2.docx` — Refiner output
- `opposing-notes.md` — Overseer critique
- `final-draft.docx` — for your review

### Step 6 — review, sign, file

Open `final-draft.docx` in Microsoft Word or LibreOffice. Read every paragraph. Verify the citations. Verify the facts. Verify the Prayer. Sign. File.

**The advocate is responsible for the pleading. The plugin is responsible for the first draft.**

---

## The `bench-config.md` file

The `bench-config.md` is how the plugin knows *which High Court* you are filing in. Every bench-specific value the Drafter needs lives in this file. A typical bench-config has fields like:

```yaml
court_header: "IN THE HIGH COURT OF JUDICATURE AT BOMBAY, BENCH AT NAGPUR."
parties_separator: "...Petitioner    Versus    ...Respondent"
annexure_prefix: "ANNEXURE-A"          # ANNEXURE-A / Annexure P/1 / Exhibit A / etc.
paper_size: "A4"
font_family: "Times New Roman"
font_size: 14
line_spacing: 1.5
left_margin_cm: 4
section_headers_style: "spaced-caps"    # F A C T S, G R O U N D S, P R A Y E R
salutation_opener: "MOST RESPECTFULLY SHEWETH:"
prayer_catchall_last_clause: "Pass any other order/orders as this Hon'ble Court may deem fit and proper in the facts and circumstances of the case and in the interest of justice."
appellate_side_rules: "Bombay High Court Appellate Side Rules 1960"
original_side_rules: "Bombay High Court Original Side Rules"
practice_directions: "Bombay High Court Practice Notes and Circulars"
state_overlay_acts:
  - "Maharashtra Civil Courts Act 1869"
  - "Bombay Court Fees Act 1959"
```

The Format agent reads this file and substitutes every value into the case-type skill template. If your bench has issued a new Practice Direction or changed an annexure convention, you edit the bench-config — never the plugin source.

---

## Why MIT License

The plugin is released under the **MIT License**. This was a deliberate choice. The alternatives — and why they were rejected — are below.

### MIT vs the alternatives

| License | Suitable for this plugin? | Reasoning |
|---|---|---|
| **MIT** ✅ chosen | Yes | Permissive · 3-line attribution requirement · zero copyleft · zero patent-grant complexity · compatible with the Anthropic Plugin Marketplace TOS · compatible with big-firm legal-tech adoption · allows a future paid commercial layer to ship under a separate corporate entity without dual-license complexity. |
| **Apache 2.0** | Close second | Adds an explicit patent grant — but Indian procedural drafting content is non-patentable subject-matter under Section 3(k) of the Patents Act 1970 (algorithms, business methods, and computer programs *per se* are not patentable in India). The patent grant is therefore dead weight, while the NOTICE-file ceremony and verbosity add friction. |
| **GPL-3.0** | ❌ Disqualifying | Copyleft would propagate to the user's case folder. The user's pleading — generated from the plugin — could be argued to be a "derivative work" under GPL-3, forcing the pleading itself to be GPL-licensed. No advocate can ship privileged client material under any open-source licence. This is a hard structural blocker. |
| **AGPL-3.0** | ❌ Disqualifying | Same problem as GPL-3, plus the network-use clause triggers if anyone runs the plugin as part of a SaaS legal-tech product. Effectively blocks all commercial integration — and many corporate legal departments have a blanket no-AGPL policy. |
| **LGPL-3.0** | ❌ Awkward | Designed for shared libraries, not for plugins that produce derivative documents. The "library exception" doesn't map cleanly to "the plugin emits a `.docx` that you sign and file". |
| **BSD-3-Clause / BSD-2-Clause** | Functionally equivalent to MIT | Slightly different attribution language; no practical advantage. MIT is more widely understood. |
| **Unlicense / CC0** | ❌ Forfeits authorship | Drops the copyright assertion entirely. The author loses the moral-rights claim under Section 57 of the Indian Copyright Act 1957, and the project loses the derivative-misuse traceability that the copyright assertion provides. |
| **Creative Commons (any variant)** | ❌ Wrong instrument | Creative Commons licences are designed for *creative content* (text, images, video) and are not recommended for *software* — they lack the software-specific warranty disclaimers, the contributor-licence-agreement compatibility, and the patent-grant clarity that software-grade licences (MIT / Apache / BSD / GPL) provide. |

### One-paragraph rationale

The plugin is released under MIT because Indian advocates and law firms — from solo practitioners on a District Court roster to the litigation teams at Cyril Amarchand, AZB, Shardul Amarchand, Khaitan, and the in-house counsel at every major Indian corporate — must be able to clone, fork, adapt, and integrate this plugin alongside their privileged client material without the licence propagating into their case folders or attaching to the pleadings they file. Only MIT (and equivalently BSD and Apache 2.0) satisfies that constraint. MIT was preferred over Apache 2.0 because the patent-grant language Apache adds carries no practical benefit in the Indian context (procedural-drafting content is unpatentable under Section 3(k) of the Patents Act 1970), and MIT's three-line clarity is friendlier to advocates who are not professional software developers and who will read the LICENSE file before adopting the plugin in chambers.

### Compatibility statement

The MIT licence under which this plugin is released is compatible with:

- The Apache License 2.0 (a downstream user may relicense as Apache 2.0 if they wish)
- The BSD 2-Clause and BSD 3-Clause licences
- The GPL family (a downstream user may incorporate MIT code into a GPL project, though they cannot relicence this repository as GPL because they are not the author)
- The Anthropic Plugin Marketplace Terms of Service (which require an OSI-approved permissive licence for community plugins)
- All major commercial-software integration policies

---

## Sibling plugins

This plugin is part of the **Wolfgang Rush legal-tech family** of open-source India-legal-drafting plugins:

- **`indian-hc-drafting`** — this plugin · [github.com/Wolfgangrush/indian-hc-drafting-litigation](https://github.com/Wolfgangrush/indian-hc-drafting-litigation)
- **`supreme-court-drafting`** — Supreme Court of India pleadings · [github.com/Wolfgangrush/supreme-court-drafting-litigation](https://github.com/Wolfgangrush/supreme-court-drafting-litigation)
- **`district-court-drafting`** — District Court civil + criminal pleadings, all-India · [github.com/Wolfgangrush/district-court-drafting-litigation](https://github.com/Wolfgangrush/district-court-drafting-litigation)
- **`indian-family-drafting`** (forthcoming) — Family Court matters under HMA / SMA / Special Marriage Act / Indian Divorce Act / Guardians and Wards Act / Domestic Violence Act
- **`indian-contracts-drafting`** (forthcoming) — commercial contracts, conveyancing, personal estate
- **`indian-regulatory-drafting`** (forthcoming) — IT Act, Income Tax, Consumer Protection, Motor Vehicles Act regulatory notices and responses

Each plugin ships independently. Install only the ones you use.

---

## Why this exists

India has roughly **1.4 million enrolled advocates** and **twenty-five High Courts**. There is currently no Claude-compatible drafting plugin that respects Indian High Court Registry formatting, Indian procedural law (CPC, CrPC, BNSS), bench-specific conventions, or the structural distinction between privileged client material and public procedural knowledge.

Foreign legal-AI tools cannot fill this gap. The training data does not exist outside the country; the procedural conventions are jurisdiction-specific; and the formatting requirements at the Registry counter of a Bombay or Madras or Calcutta High Court are matters of bench practice that no foreign tool has encountered.

This plugin opens that door. It is most-deeply-validated for the **Bombay High Court (Nagpur Bench)** — the author's primary practice court. Other benches are supported via bench-config and the depth of per-bench validation will come from community contribution by advocates who file regularly at those benches.

---

## Roadmap

- [x] **v0.1.0-alpha (current)** — universal HC pleading skeleton + 13 case-type skills + 6-agent pipeline + bench-config architecture + 28 bench exemplars
- [ ] **v0.1.x** — bug fixes, quality-gate iteration, language-register polish, formatting refinements driven by user feedback
- [ ] **v0.x onward** — bench-config calibration deepening per High Court, additional case-type skills, and procedural-rule updates as they arrive
- [ ] **v1.0.0** — Stable release after community-validated formatting and field-testing

Per-bench deep validation will arrive in the order advocates contribute. The plugin's bench-config architecture means any advocate filing regularly before a given bench can deepen the calibration for that bench by opening an issue or pull request with their bench's idiom — no central roadmap is needed to enable that. The roadmap above is therefore intentionally open-ended.

---

## Contributing

Advocates who file regularly before any Indian High Court are invited to contribute bench-config calibration for the specific bench they practise before. Open a GitHub issue with:

- Your practice bench (e.g., *"Karnataka HC at Bengaluru"*)
- Your bench's Court header text
- Your bench's Appellate-Side / Original-Side Rules reference
- Your bench's annexure-marker convention
- Any other bench-specific formatting overlay (paper size, font, section-header style, prayer catchall, etc.)
- Recent Practice Directions issued by the bench affecting pleading format

Pull requests are welcome with a one-paragraph explanation of the change and a reference to the bench rule or Practice Direction that justifies it.

This plugin is open source under MIT.

---

## Contact

All inquiries and feedback are handled via **GitHub Issues** on the project repository.

Bug reports · feature requests · bench-config contributions · improvements: open an issue.

This project does not have an email contact channel and does not accept private legal-services inquiries through this repository. **No commercial engagement is offered through this plugin or its repository.**

*(Future releases may introduce a commercial layer published under a separate corporate entity — at that point this section will be updated. v0.x.x is open-source-only infrastructure with no commercial channel.)*

---

## Author and brand

This plugin is authored by **Rushikesh R. Mahajan**, Advocate, enrolled with the Bar Council of Maharashtra and Goa, practising before the Bombay High Court (Nagpur Bench).

The plugin is published under the **Wolfgang Rush** open-source brand — the author's publishing handle for legal-technology infrastructure. All commits to this repository are signed under the Wolfgang Rush GitHub identity. The real-identity declaration appears here, and again in `NOTICE.md`, so that the Bar Council Rule 36 accountability mechanism (advocate-as-individual responsibility) is preserved transparently rather than displaced by the publishing handle.

---

## Provenance and privilege statement

See [`NOTICE.md`](./NOTICE.md) for the full provenance and privilege statement.

**In brief:** this plugin contains only public procedural knowledge — High Court Registry conventions, CPC / CrPC / BNSS references, bench-specific formatting derived from public rules of court, and generic placeholders. It does **not** contain any specific client matter, communication, document, or personal data. The legal distinction between privileged client communications (protected under Section 132 of the Bharatiya Sakshya Adhiniyam 2023 / Section 126 of the Indian Evidence Act 1872) and general professional knowledge of procedural law (public, sharable, the same knowledge underlying every legal-drafting textbook from Mulla to Sarkar to Ratanlal & Dhirajlal) is set out in `NOTICE.md` in full.

---

## Disclaimer and Bar Council of India Rule 36 compliance

This plugin is **open-source infrastructure released free of cost** under the MIT licence. It is published as a contribution to the legal community and to the broader open-source developer ecosystem.

**This plugin:**

- Does **not** constitute legal advice.
- Does **not** create an advocate-client relationship between the author and any user.
- Does **not** solicit professional work from any user, group, or audience.
- Does **not** advertise the professional services of the author or any advocate.
- Does **not** offer paid legal services, paid consultations, or commercial legal engagements through this repository or any associated channel.

**It is:**

- A drafting aid for use by **enrolled advocates** who retain full professional responsibility for every pleading produced.
- A reference implementation of open-source legal-tech infrastructure for Indian High Court practice.
- Released under the Bar Council of India Rules, Part VI, Chapter II, Section IV, **Rule 36** (Conduct and Etiquette — restriction on advertising and solicitation), to which the author and every Indian advocate is bound.

**Every advocate using this plugin is reminded:** the advocate retains full professional responsibility for the verification of facts, the accuracy of citations, the correctness of legal grounds, the propriety of the prayer, and the signature on every pleading filed. AI-generated drafting output is **starting material, not a finished pleading**.

---

## License

**MIT.** See [`LICENSE`](./LICENSE) for the full text.

Copyright (c) 2026 Wolfgang Rush. Authored by Rushikesh R. Mahajan, Advocate, publishing under the Wolfgang Rush open-source brand.
