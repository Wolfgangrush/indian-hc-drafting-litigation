# bench-config — Delhi High Court

**Validation depth:** Researched · awaiting Registry validation.
**Source authorities:** Delhi High Court (Original Side) Rules **2018**; Delhi HC Rules; Delhi HC Practice Directions; Delhi HC PIL Rules.

---

## Section 1 — Court identification

```yaml
high_court: "High Court of Delhi"
bench: "Principal Seat (New Delhi)"
state: "Delhi (NCT)"
court_header_line: |
  IN THE HIGH COURT OF DELHI AT NEW DELHI.
```

## Section 2 — Procedural Rules

```yaml
appellate_side_rules: |
  Delhi High Court Rules (Appellate Side)
original_side_rules: |
  Delhi High Court (Original Side) Rules, 2018
pil_rules: |
  Delhi High Court (Public Interest Litigation) Rules, 2010
ipr_division_rules: |
  Delhi High Court Intellectual Property Rights Division Rules, 2021
```

Delhi HC has dedicated IPR Division Rules (2021) — for IP matters, additional formatting requirements may apply.

## Section 3 — Cause Title and Parties

```yaml
case_number_format: |
  [CASE TYPE] (CIVIL/CRIMINAL) NO. _____ OF [YEAR]
act_code_line: no                          # Delhi HC does not use "ACT CODE-" line
parties_separator: "...VERSUS..."          # Title Case bold "Versus" common; ...VERSUS... acceptable
```

## Section 4 — Section headers

```yaml
section_headers_style: title-case          # "Facts", "Grounds", "Synopsis" — NOT spaced like Bombay HC
```

## Section 5 — Salutation and connective phrases

```yaml
salutation_opener: |
  The humble petition of the Petitioner above-named most respectfully showeth:
prayer_opener: |
  It is, therefore, most respectfully prayed that this Hon'ble Court may graciously be pleased to:
prayer_catchall_last_clause: |
  Pass any other or further order(s) as this Hon'ble Court may deem fit and proper in the facts and circumstances of the case and in the interest of justice.
```

## Section 6 — Annexure marker convention

```yaml
annexure_prefix: "Annexure-"                # Title Case, not all-caps
annexure_letter_omissions: []
respondent_annexure_prefix: ""              # No separate prefix
collective_annexure_suffix: " (Colly.)"
inline_marker_template: |
  ...a true copy whereof is annexed hereto and marked as **Annexure-[A/B/C]**
annexure_column_label: "Annexure"
```

## Section 7 — Counsel block (CRITICAL — Delhi HC 2018 Rules mandate)

```yaml
counsel_place: "NEW DELHI"
counsel_block_template: |
  NEW DELHI                                 ([NAME], Advocate)
  DATE: <DD.MM.YYYY>                        Bar Council Enrolment No. [____]
                                            Phone: [____]
                                            Email: [____]
                                            COUNSEL FOR THE [PETITIONER/RESPONDENT]
foot_of_pleading_requirements:
  - "Counsel name + signature"
  - "Bar Council enrolment number — MANDATORY per Delhi HC Original Side Rules 2018"
  - "Phone number — MANDATORY per Delhi HC Original Side Rules 2018"
  - "Email — MANDATORY per Delhi HC Original Side Rules 2018"
  - "Address for service"
```

**LOAD-BEARING:** Delhi HC Original Side Rules 2018 require the advocate's name + enrolment number + phone + email at the foot of every pleading and vakalatnama. Failure = Registry rejection.

## Section 8 — Affidavit dispensation

```yaml
affidavit_dispensation_note: |
  Note: The [Petitioner] is in judicial custody therefore the supporting affidavit may kindly be dispensed with subject to such conditions as this Hon'ble Court may deem fit to impose.
```

## Section 9 — Paper size and Registry formatting (CRITICAL — Delhi HC 2018 Rules)

```yaml
paper_size: A4
font_family: "Times New Roman"
font_size_body: 14
line_spacing: 2.0                          # DOUBLE spacing per Delhi HC Original Side Rules 2018 Rule 1
left_margin_cm: 4
right_margin_cm: 2.5
top_margin_cm: 2.5
bottom_margin_cm: 2.5
paper_type: "white A4, lithographed or printed on ONE SIDE only"
```

**LOAD-BEARING:** Delhi HC 2018 Rules Rule 1 — "every Plaint, Written Statement, Application, Petition and the like presented to Court shall be lithographed or printed in double spacing on one side of A4 size white paper."

## Section 10 — Accompanying-application requirements

```yaml
accompanying_applications_per_case_type:
  pil_draft:
    - application_for_directions          # Common in Delhi HC PIL practice
    - stay_application
  civil_wp_draft:
    - stay_application
  criminal_appeal_draft:
    - suspension_of_sentence
    - condonation_of_delay
```

## Section 11 — Limitation references

```yaml
limitation_act_schedule_article: |
  Limitation Act 1963, Schedule, Article [N]
```

## Section 12 — Court-Fees Act citation

```yaml
state_court_fees_act_citation: |
  Schedule I of the Court-Fees Act, 1870 (as extended to the National Capital Territory of Delhi)
```

---

## Special Delhi HC notes

1. **Memo of Parties:** Delhi HC 2018 Rules require a separate Memo of Parties with full name, parentage, age, occupation, address — distinct from the main pleading body.
2. **Index numbering:** pleadings paginated numerically; Index lists every section + page span.
3. **Service requirements:** the application/petition shall be accompanied by written proof of intimation and respective service, indicating name(s) of all opposite parties.
4. **IP matters:** if the case is in the IP Division, additional formatting per Delhi HC IPR Division Rules 2021.
