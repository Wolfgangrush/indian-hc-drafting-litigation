---
name: _hc_pleading_base
description: Universal Indian High Court pleading skeleton, bench-config-driven. Shared base for all 13 case-type drafting skills. Holds the standard structure (Cause Title → Parties → Statutory Opening → Prelude → FACTS → GROUNDS → PRAYER → Counsel block → Index → Synopsis → List of Annexures → Accompanying Applications). The skeleton itself is structural and uncopyrightable; bench-specific values (Court header, parties separator, section-header style, annexure prefix, counsel block layout, paper/font/margins) are sourced from the user's case-folder `bench-config.md` at run-time. NOT invoked directly — case-type skills extend this.
allowed-tools: []
---

# Indian HC Pleading — Universal Skeleton (bench-config-driven)

This is the SHARED structure that every Indian High Court pleading follows. The 13 case-type skills extend this with their own statutory openings, grounds structure, prayer language, and accompanying applications.

**Bench-config-driven design:** the structural shape below is universal across Indian HCs. Specific Registry-facing values (Court header text, parties separator, section-header style, annexure prefix, counsel block) vary from bench to bench and are sourced from `<case-folder>/bench-config.md` at run-time. The Format agent substitutes the placeholders below from the user's bench-config; the Drafter renders the final pleading in the user's bench's idiom.

→ See `${CLAUDE_PLUGIN_ROOT}/skills/_drafting_common/SKILL.md` for the bench-config-driven rules and the bench-coverage research.
→ See `${CLAUDE_PLUGIN_ROOT}/bench-config/exemplars/` for bench-config exemplars per HC (Bombay-[bench city], Bombay-Principal, Delhi, Karnataka, Madras, Calcutta, Allahabad, Punjab & Haryana, Gujarat, Kerala, Rajasthan, etc.).

## BENCH-CONFIG PLACEHOLDERS USED IN THIS SKELETON

Every `{{bench_config.X}}` placeholder below resolves to a value in the user's `<case-folder>/bench-config.md`. The Format agent substitutes at run-time; the Drafter ships the final pleading.

| Placeholder | Resolves to |
|---|---|
| `{{bench_config.court_header}}` | The exact Court header line accepted by the bench's Registry |
| `{{bench_config.parties_separator}}` | `///VERSUS///` (Bombay), `...VERSUS...` (some HCs / applications), `vs.` (some practices) |
| `{{bench_config.section_headers_style}}` | `spaced` (Bombay) or `title-case` (most other HCs) |
| `{{bench_config.salutation_opener}}` | Bench's preferred opener phrase |
| `{{bench_config.annexure_prefix}}` | `ANNEXURE-` (Bombay), `Annexure P/` (Punjab & Haryana, Orissa), `Annexure P-` (Rajasthan), `Exhibit` (Kerala default), `Document No.` (Madras OS), etc. |
| `{{bench_config.annexure_letter_omissions}}` | `[]` (most HCs) or `["I"]` (Karnataka — letter I omitted) |
| `{{bench_config.respondent_annexure_prefix}}` | `R/` (Punjab & Haryana) or none (most HCs) |
| `{{bench_config.counsel_place}}` | `[PLACE]` ([Your Bench]), `MUMBAI` (Principal Bench), `NEW DELHI` (Delhi), etc. |
| `{{bench_config.advocate_block_template}}` | Bench's preferred Counsel/Advocate signature-block layout |
| `{{bench_config.foot_of_pleading_requirements}}` | e.g., Delhi 2018: advocate name + enrolment + phone + email mandatory at foot |
| `{{bench_config.paper_size}}` | `A4` (most) / `Legal` (some Original Side practices) |
| `{{bench_config.line_spacing}}` | `1.5` (most), `2.0` (Delhi 2018, Punjab & Haryana, double-spacing benches) |
| `{{bench_config.font_size_body}}` | `14` (most), `12` (some State Manuals) |
| `{{bench_config.margins}}` | bench-specific margin block |

## THE OUTPUT UNIT

For every case type, the final output is a SINGLE `.docx` file containing all sections in this order:

```
┌─────────────────────────────────────────────────────────┐
│  ① MAIN PLEADING                                         │
│  ────────────────                                        │
│  Cause Title  (Court header per bench-config)           │
│  Parties Block  (separator per bench-config)            │
│  Statutory Opening  (case-type-specific)                │
│  Prelude  (salutation per bench-config)                 │
│  FACTS  (with inline annexure markers per bench-config) │
│  GROUNDS  (case-type-specific structure)                │
│  PRAYER  (case-type-specific reliefs + catchall)        │
│  Counsel block  (per bench-config)                      │
│  Notes / Limitation (where applicable)                  │
│                                                         │
│  ② INDEX (table)                                        │
│  ③ SYNOPSIS                                              │
│      Dates–Events table                                 │
│      POINT(S) TO BE CONSIDERED                          │
│      ACTS & RULES                                       │
│      CITATIONS                                          │
│  ④ LIST OF ANNEXURES (consolidated)                     │
│                                                         │
│  ⑤ ACCOMPANYING APPLICATIONS (case-type-specific)        │
│     each with its own cause title + prayer + counsel    │
└─────────────────────────────────────────────────────────┘
```

## MARKDOWN HEADING DISCIPLINE (load-bearing — Drafter must follow)

The Drafter writes Markdown. Pandoc converts the Markdown to `.docx` using the **`reference.docx` shipped at `${CLAUDE_PLUGIN_ROOT}/skills/_hc_pleading_base/reference.docx`**, which has locked Word styles matching the **filing-grade Bombay HC convention** (extracted from an actual filed Second Appeal pleading and validated by the author):

- **Body (Normal)** — TNR 14pt, 1.5 line spacing, justified, 0.5cm first-line indent
- **Heading 1** — TNR 14pt **bold + centered** (NOT underlined) — for the Court header line and the case-number line
- **Heading 2** — TNR 14pt **bold + UNDERLINED + centered + letter-spacing** — for the spaced section headers (`F A C T S`, `G R O U N D S`, `P R A Y E R`, `I N D E X`, `S Y N O P S I S`, `L I S T   O F   A N N E X U R E S`)
- **Heading 3** — TNR 14pt **bold + UNDERLINED + centered** — for the unspaced section headers (`SUBSTANTIAL QUESTIONS OF LAW`, `ACTS & RULES`, `CITATIONS`) and the statutory opening line (`SECOND APPEAL UNDER SECTION 100 CPC`, `WRIT PETITION UNDER ARTICLE 226 …`)
- **Heading 4** — TNR 14pt **bold + UNDERLINED + left-aligned** — for `MOST RESPECTFULLY SHEWETH:` style left-margin anchors
- **Tables** — `tblLayout = fixed`; first row bold centered; cell margins locked

**For the styles to apply, the Drafter MUST use Markdown headings — not plain text — for the following structural elements:**

| Markdown | Rendered as | Used for |
|---|---|---|
| `# Heading 1` | Bold centered (no underline) | Court header line; case-number line |
| `## Heading 2` | Bold centered UNDERLINED with letter-spacing | Spaced section headers: `## F A C T S`, `## G R O U N D S`, `## P R A Y E R`, `## I N D E X`, `## S Y N O P S I S`, `## L I S T   O F   A N N E X U R E S`, `## V E R I F I C A T I O N` |
| `### Heading 3` | Bold centered UNDERLINED | Unspaced section headers + statutory opening: `### SUBSTANTIAL QUESTIONS OF LAW`, `### ACTS & RULES`, `### CITATIONS`, `### WRIT PETITION UNDER ARTICLE 226 READ WITH ARTICLE 227 OF THE CONSTITUTION OF INDIA` |
| `#### Heading 4` | Bold left UNDERLINED | Left-anchored bold-underlined headings: `#### MOST RESPECTFULLY SHEWETH:` |
| Body paragraph | TNR 14pt justified, 1.5 spacing, 0.5cm first-line indent | Everything else |
| `**Bold inline**` | Bold | Property descriptors / annexure markers / key terms inline within Facts narrative |

**Numbered paragraphs (Facts and Grounds) use BOLD numbers.** The Drafter writes:
```markdown
**1.**    It is most respectfully submitted that…
**2.**    That the Petitioner…
```
(four-space tab after the bold number; pandoc + reference.docx renders this as the gold-standard pleading layout.)

**Tables (Index, List of Annexures, Synopsis Dates–Events) — column widths are FORCED by a post-pandoc Python script.** Pandoc pipe-tables do NOT reliably honour the reference.docx's `tblLayout=fixed` for column widths; left to itself, pandoc apportions widths from the column-header text length, which produces narrow stacking columns (the v0.2.0 Index-table defect). The Drafter MUST run the shipped `fix_docx_tables.py` post-pandoc:

```bash
pandoc draft-v1.md -o draft-v1.docx \
  --reference-doc="${CLAUDE_PLUGIN_ROOT}/skills/_hc_pleading_base/reference.docx" \
  --from=markdown+pipe_tables+raw_tex
python3 "${CLAUDE_PLUGIN_ROOT}/skills/_hc_pleading_base/fix_docx_tables.py" draft-v1.docx
```

The fix script walks every table and forces the column-width profile that matches the table's column count (5-col = 8/8/60/14/10 percent for Sr.No/Annx/Particulars/Date/Pgs; 4-col = 10/10/65/15; 3-col = 10/75/15; 2-col = 18/82 for Synopsis Dates–Events). Also locks first-row bold + centered + vertically-centered cells. This is the only reliable path to filing-grade table rendering.

**Cover-page discipline (NON-NEGOTIABLE — Verifier checks):**
- INDEX, SYNOPSIS, and LIST OF ANNEXURES each begin on a new page (`\newpage` in Markdown).
- Each cover page carries ONLY: court header (`#`) + case-number line (`#`) + short cause-title (Petitioner short name `///VERSUS///` Respondent short name) + the section header (`##`) + the table.
- DO NOT repeat the full Petitioner/Respondent address block on cover pages. Full party block appears only on the Main Petition cover.

**Counsel block alignment:** the closing `[PLACE] / DATE / COUNSEL FOR THE PETITIONER` block is right-aligned. Write it in Markdown as a paragraph with the `right` attribute or use a 2-column layout via a pipe table with the right column carrying the counsel block.

## ① MAIN PLEADING — UNIVERSAL TEMPLATE (bench-config-substituted; Markdown-heading-disciplined)

```markdown
# {{bench_config.court_header}}

# [CASE TYPE LINE] NO._______/[YEAR]

{{bench_config.act_code_line_if_applicable}}

(In the matter of [case-specific descriptor — e.g., "challenging the judgment dated <date> passed by <lower court> in <case no>…"])

**[APPELLANT / PETITIONER / APPLICANT]:**

<Name> S/o / D/o <Father's name>,
Aged about <age> years,
Occupation – <occupation>,
Residing at <address>.

{{bench_config.parties_separator}}

**RESPONDENT[S]:**

1. <Respondent 1>
2. <Other respondents if any>

# [STATUTORY OPENING — case-type-specific. Fill from extending skill.]

{{bench_config.salutation_opener}}

[Opening fact paragraph: nature of the matter being challenged or the relief sought, with date(s) and authority being impugned. Include inline annexure marker for the impugned order: "…is annexed herewith and marked as **{{bench_config.annexure_prefix}}A**."]

## {{bench_config.section_header.facts}}

1. The [Petitioner/Appellant] is a bonafide citizen of India and a permanent resident of the above-mentioned address.

2. [Chronological narrative paragraphs. Every documentary fact gets an inline annexure marker (`{{bench_config.annexure_prefix}}A, B, C, …` observing `{{bench_config.annexure_letter_omissions}}` — Karnataka HC omits letter I). Each paragraph numbered.]

3. [Defence / petitioner's version, where applicable.]

4. By the impugned [order/judgment] dated <date>, the learned [court] in <case-no> [the disposition]. The [Petitioner/Appellant] is filing the present [petition/memo of appeal] on the following grounds, without prejudice to each other.

## {{bench_config.section_header.grounds}}

I. **[Ground heading]** — [The learned Court erred in law and facts of the case and failed to appreciate the evidence in proper perspective and wrongly [convicted/dismissed/granted/rejected]…]

II. **[Ground heading]** — [Additional grounds — case-type-specific structure. Each ground = one paragraph. Anchor to precedent paragraph numbers ONLY for precedents whose PDFs are supplied in `<case-folder>/law-pdfs/`.]

III. **[Ground heading]** — [That the order is illegal, erroneous and liable to be set aside.]

IV. **Reservation** — That the [Petitioner/Appellant] reserves [the] right to raise additional grounds at the time of hearing.

V. **Limitation and absence of parallel remedy** — That the present [petition/appeal] is filed within limitation and the impugned [order/judgment] has not been challenged before the Hon'ble Supreme Court of India or this Hon'ble High Court at any earlier time.

## {{bench_config.section_header.prayer}}

{{bench_config.prayer_opener}}

(a) [Primary relief — case-type-specific.]

(b) {{bench_config.prayer_catchall_last_clause}}

{{bench_config.counsel_block_template}}

[OPTIONAL: Affidavit dispensation note where applicable, per bench-config.]

[OPTIONAL — for appeals: "Notes on Limitation:" block with order date, last day for filing, actual filing date, days delay.]
```

## ② INDEX (cover page — short cause-title only; full party block does NOT appear here)

```markdown
\newpage

# {{bench_config.court_header}}

# [CASE TYPE] NO._______/[YEAR]

**[Petitioner/Appellant short name]**

{{bench_config.parties_separator}}

**[Respondent short name + "& Ors."]**

## {{bench_config.section_header.index}}

| Sr.No | {{bench_config.annexure_column_label}} | Particulars                                        | Date | Pgs |
|:-----:|:----:|:---------------------------------------------------|:----:|:---:|
| 1.    |      | Synopsis                                           |      |  i  |
| 2.    |      | [Appeal/Petition u/s …]                            |      |  1  |
| 3.    |      | List of Annexures                                  |      |     |
| 4.    | A    | Copy of [impugned order / primary document]        | <dt> |     |
| 5.    | B    | [(Colly) where applicable] Other annexed documents | <dt> |     |

{{bench_config.counsel_block_template}}
```

## ③ SYNOPSIS (cover page — short cause-title only)

```markdown
\newpage

# {{bench_config.court_header}}

# [CASE TYPE] NO._______/[YEAR]

**[Petitioner/Appellant short name]**

{{bench_config.parties_separator}}

**[Respondent short name + "& Ors."]**

## {{bench_config.section_header.synopsis}}

| Date | Event |
|:----:|:------|
| <dt> | <event narrative — one line per row> |
| <dt> | <event narrative> |
| <dt> | <event narrative> |

Hence this [Appeal/Petition].

**POINT(S) TO BE CONSIDERED:**

As raised in the Memo of [Appeal/Petition].

**ACTS & RULES:**

- <statute 1>
- <statute 2>
- <statute 3>

**CITATIONS:**

Will be cited at the time of hearing with the permission of this Hon'ble Court.

{{bench_config.counsel_block_template}}
```

## ④ LIST OF ANNEXURES (cover page — short cause-title only)

```markdown
\newpage

# {{bench_config.court_header}}

# [CASE TYPE] NO._______/[YEAR]

**[Petitioner/Appellant short name]**

{{bench_config.parties_separator}}

**[Respondent short name + "& Ors."]**

## {{bench_config.section_header.list_of_annexures}}

| Sr.No | {{bench_config.annexure_column_label}} | Particulars                       | Date | Pgs |
|:-----:|:----:|:----------------------------------|:----:|:---:|
| 1.    | A    | <particulars from inline markers> | <dt> |     |
| 2.    | B    | <particulars>                     | <dt> |     |
| 3.    | C    | <particulars>                     | <dt> |     |

{{bench_config.counsel_block_template}}
```

This list is auto-generated by Drafter from the inline markers in FACTS, observing the bench's annexure-letter-omission rule (e.g., Karnataka HC omits letter I). Verifier cross-checks.

## ⑤ ACCOMPANYING APPLICATIONS

Case-type-specific. Examples (each with own cause title + own facts + own prayer + own counsel block, all rendered in the bench's idiom):

- **Criminal Appeal:**
  - APPLICATION UNDER SECTION 389(1) Cr.P.C. AND 430(1) BNSS FOR SUSPENSION OF SENTENCE AND FOR BAIL
  - APPLICATION UNDER SECTION 5 OF LIMITATION ACT FOR CONDONATION OF DELAY (where filed late)
- **Civil/Criminal WP, First Appeal:** Stay Application (where interim relief needed)
- **Bail/ABA/482/Contempt/PIL:** typically standalone, no accompanying

The extending case-type skill specifies which applications attach.

## CASE-TYPE SKILL CONTRACT

Every case-type skill that extends this base must provide:

```yaml
# In the case-type skill's SKILL.md:
extends: _hc_pleading_base

statutory_opening: |
  <case-type-specific opening clause, e.g.,
   "CRIMINAL APPEAL UNDER SECTION 374(2) OF Cr.P.C. READ WITH
    SECTION 415(2) OF BNSS, 2023.">

case_type_line: "CRIMINAL APPEAL"   # used in cause title
case_short_code: "APEAL"            # the HC taxonomy code (varies by HC)

grounds_structure: |
  <case-type-specific opening grounds + style notes>

prayer_template: |
  <case-type-specific primary prayer language>

accompanying_applications:
  - suspension_of_sentence
  - condonation_of_delay
```

## THE USER PROVIDES BENCH-CONFIG AND CASE-TYPE FORMAT

The skeleton above is **structure only**. Two layers are user-supplied:

1. **bench-config.md** in the case folder — provides every `{{bench_config.X}}` value for the user's specific HC bench. Exemplars for the major HCs are in `${CLAUDE_PLUGIN_ROOT}/bench-config/exemplars/`. The user copies the exemplar for their bench, then files the case-folder copy.

2. **format-from-user.md** in each case-type skill folder — provides the user's preferred drafting style for connective phrases within their bench's framework. Drafter uses this for style alignment.

The plugin does NOT assume any HC bench's specific values from training data. Every bench-specific value comes from the user's bench-config.

## BENCH-CONFIG EXEMPLAR INDEX

Validated bench-config exemplars in `${CLAUDE_PLUGIN_ROOT}/bench-config/exemplars/`:

| Exemplar | Validation depth | Source |
|---|---|---|
| `bombay-hc.md` | Researched · awaiting Registry validation | Bombay HC AS Rules 1960, Bombay HC bench Practice Notes |
| `bombay-hc-principal-mumbai.md` | Bench-config supported | Bombay HC AS + OS Rules, Principal-Bench Practice Notes |
| `bombay-hc-aurangabad.md` | Bench-config supported | Bombay HC AS Rules + Aurangabad Bench Practice |
| `bombay-hc-goa.md` | Bench-config supported | Bombay HC AS Rules + Goa Bench Practice |
| `delhi-hc.md` | Researched · awaiting Registry validation | Delhi HC (Original Side) Rules 2018 |
| `karnataka-hc.md` | Researched · awaiting Registry validation | Karnataka HC Rules 1959, Writ Proceedings Rules 1977 |
| `madras-hc.md` | Researched · awaiting Registry validation | Madras HC Original Side Rules 1956, Appellate Side Rules |
| `calcutta-hc.md` | Researched · awaiting Registry validation | Calcutta HC Original Side Rules 1914, Appellate Side Rules |
| `allahabad-hc.md` | Researched · awaiting Registry validation | Allahabad HC Rules 1952 |
| `punjab-haryana-hc.md` | Researched · awaiting Registry validation | Punjab & Haryana HC Rules & Orders Volume V |
| `gujarat-hc.md` | Researched · awaiting Registry validation | Gujarat HC Rules 1993 |
| `kerala-hc.md` | Researched · awaiting Registry validation | Rules of the High Court of Kerala 1971 |
| `rajasthan-hc.md` | Researched · awaiting Registry validation | Rajasthan HC Rules 1952 |
| `patna-hc.md` | Researched · awaiting Registry validation | Patna HC Rules (Chapter IIIA) |
| `orissa-hc.md` | Researched · awaiting Registry validation | Orissa HC Rules |
| `telangana-hc.md` | Researched · awaiting Registry validation | Telangana HC Rules + AP Writ Proceedings Rules 1977 |
| `andhra-pradesh-hc.md` | Researched · awaiting Registry validation | AP Writ Proceedings Rules 1977, Civil Rules of Practice 1990 |
| `gauhati-hc.md` | Stub · community contribution welcomed | Gauhati HC PIL Rules 2011 |
| `himachal-pradesh-hc.md` | Stub · community contribution welcomed | HP HC Rules |
| `jammu-kashmir-ladakh-hc.md` | Stub · community contribution welcomed | J&K + Ladakh HC Rules |
| `jharkhand-hc.md` | Stub · community contribution welcomed | Jharkhand HC Rules |
| `chhattisgarh-hc.md` | Stub · community contribution welcomed | Chhattisgarh HC Rules |
| `madhya-pradesh-hc.md` | Stub · community contribution welcomed | MP HC Rules |
| `uttarakhand-hc.md` | Stub · community contribution welcomed | Uttarakhand HC Rules |
| `manipur-hc.md` | Stub · community contribution welcomed | Manipur HC Rules |
| `meghalaya-hc.md` | Stub · community contribution welcomed | Meghalaya HC Rules |
| `sikkim-hc.md` | Stub · community contribution welcomed | Sikkim HC Rules |
| `tripura-hc.md` | Stub · community contribution welcomed | Tripura HC Rules |

**Validation depth taxonomy:**
- **Researched · awaiting Registry validation:** Bench-config values sourced from the bench's official Rules + public practice texts; awaiting community Registry-acceptance validation.
- **Stub · community contribution welcomed:** Bench is named but bench-config exemplar is a minimal placeholder; advocates practising at this bench are invited to submit a filled exemplar via PR.

## DEPENDENCY ON OTHER FILES

- `${CLAUDE_PLUGIN_ROOT}/skills/_drafting_common/SKILL.md` — rules and constraints (bench-config-driven)
- `${CLAUDE_PLUGIN_ROOT}/bench-config/exemplars/<hc-name>.md` — bench-config exemplars per HC
- `${CLAUDE_PLUGIN_ROOT}/bench-config/bench-config-template.md` — empty template for benches not yet exemplified
- `${CLAUDE_PLUGIN_ROOT}/agents/<agent>.md` — agent role definitions; Format agent reads bench-config and substitutes placeholders at run-time
