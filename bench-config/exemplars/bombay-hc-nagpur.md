# bench-config — Bombay High Court, Nagpur Bench

**Validation depth:** Deep · battle-tested · author's primary practice court.
**Source authorities:** Bombay High Court (Appellate Side) Rules 1960; Bombay HC Nagpur Bench Practice Notes; Bombay HC Civil Manual; Bombay HC Criminal Manual.

---

## Section 1 — Court identification

```yaml
high_court: "Bombay High Court"
bench: "Nagpur Bench"
state: "Maharashtra"
court_header_line: |
  IN THE HIGH COURT OF JUDICATURE AT BOMBAY BENCH AT NAGPUR.
```

Note the period at the end of the Court header — Bombay HC Nagpur convention.

## Section 2 — Procedural Rules

```yaml
appellate_side_rules: |
  Bombay High Court (Appellate Side) Rules, 1960
original_side_rules: ""                    # Not applicable for Nagpur Bench
pil_rules: |
  Bombay High Court Public Interest Litigation Rules, 2010
```

## Section 3 — Cause Title and Parties

```yaml
case_number_format: |
  [CASE TYPE] NO._______/[YEAR]
act_code_line: yes                         # Required after case number line
parties_separator: "///VERSUS///"          # Preferred for appeals; ...VERSUS... acceptable for applications
```

## Section 4 — Section headers

```yaml
section_headers_style: spaced              # F A C T S, G R O U N D S, S Y N O P S I S, I N D E X
```

## Section 5 — Salutation and connective phrases

```yaml
salutation_opener: |
  The [Applicant/Petitioner/Appellant] named above most humbly and respectfully begs to submit as under: -
prayer_opener: |
  It is, therefore, prayed that this Hon'ble Court may kindly be pleased to:
prayer_catchall_last_clause: |
  Grant any other relief deems fit just and proper in the facts and circumstances of the case in favour of the [petitioner/appellant].
```

## Section 6 — Annexure marker convention

```yaml
annexure_prefix: "ANNEXURE-"
annexure_letter_omissions: []              # No letters omitted
respondent_annexure_prefix: ""             # No separate prefix
collective_annexure_suffix: " (Colly)"
inline_marker_template: |
  ...is annexed herewith and marked as **ANNEXURE-[A/B/C]**
annexure_column_label: "Annx"
```

## Section 7 — Counsel block

```yaml
counsel_place: "NAGPUR"
counsel_block_template: |
  NAGPUR                      ([NAME], Adv.)
  DATE:   .__.YYYY            COUNSEL FOR [APPELLANT/PETITIONER]
foot_of_pleading_requirements:
  - "Counsel name"
  - "(Optional) Bar Council enrolment number"
```

## Section 8 — Affidavit dispensation

```yaml
affidavit_dispensation_note: |
  Note: The [Appellant] is in jail therefore his affidavit may kindly be dispensed with.
```

## Section 9 — Paper size and Registry formatting

```yaml
paper_size: A4
font_family: "Times New Roman"
font_size_body: 14
line_spacing: 1.5
left_margin_cm: 4
right_margin_cm: 2.5
top_margin_cm: 2.5
bottom_margin_cm: 2.5
```

## Section 10 — Accompanying-application requirements

```yaml
accompanying_applications_per_case_type:
  pil_draft:
    - stay_application
  civil_wp_draft:
    - stay_application
  criminal_appeal_draft:
    - suspension_of_sentence
    - condonation_of_delay
  first_appeal_draft:
    - stay_application
```

## Section 11 — Limitation references

```yaml
limitation_act_schedule_article: |
  Limitation Act 1963, Schedule, Article [N]
```

## Section 12 — State Court-Fees Act citation

```yaml
state_court_fees_act_citation: |
  Schedule I, Article [N] of the Bombay Court-Fees Act, 1959, as amended.
```
