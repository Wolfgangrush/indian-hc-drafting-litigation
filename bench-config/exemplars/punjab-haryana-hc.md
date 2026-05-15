# bench-config — High Court of Punjab and Haryana

**Validation depth:** Researched · awaiting Registry validation.
**Source authorities:** Rules & Orders of the Punjab and Haryana High Court, Volume V; Punjab & Haryana HC PIL Rules.

---

## Section 1 — Court identification

```yaml
high_court: "High Court of Punjab and Haryana"
bench: "Principal Seat (Chandigarh)"
state: "Punjab, Haryana, Chandigarh (UT)"
court_header_line: |
  IN THE HIGH COURT OF PUNJAB AND HARYANA AT CHANDIGARH.
```

## Section 2 — Procedural Rules

```yaml
high_court_rules_and_orders: |
  Rules and Orders of the Punjab and Haryana High Court, Volume V
pil_rules: |
  Punjab and Haryana High Court PIL Rules
```

## Section 3 — Cause Title and Parties

```yaml
case_number_format: |
  [CASE TYPE] No. _____ of [YEAR]
parties_separator: "...VERSUS..."
```

## Section 4 — Section headers

```yaml
section_headers_style: title-case
```

## Section 6 — Annexure marker convention (CRITICAL — Punjab & Haryana-specific)

```yaml
annexure_prefix: "Annexure P/"              # PETITIONER's annexures: "P/1", "P/2", "P/3"
respondent_annexure_prefix: "Annexure R/"   # RESPONDENT's annexures: "R/1", "R/2", "R/3"
annexure_letter_omissions: []
collective_annexure_suffix: ""              # Punjab & Haryana doesn't use "Colly" suffix the same way
inline_marker_template: |
  ...a copy whereof is annexed herewith and marked as **Annexure P/[1/2/3]**
annexure_column_label: "Annexure"
```

**LOAD-BEARING:** Punjab & Haryana HC Rules & Orders Volume V — "every document accompanying a written statement or return shall bear an annexure mark on the right hand top corner of its opening sheet, with each annexure mark consisting of the letter 'R' followed by the serial number of the document; for example R. 1, R. 2, R. 3." Petitioner's annexures use `P/N`; Respondent's use `R/N`.

## Section 7 — Counsel block

```yaml
counsel_place: "CHANDIGARH"
counsel_block_template: |
  CHANDIGARH                                ([NAME], Advocate)
  DATE: <DD.MM.YYYY>                        Bar Council Enrolment No. [____]
                                            COUNSEL FOR THE [PETITIONER/RESPONDENT]
```

## Section 9 — Paper size and Registry formatting (CRITICAL — Punjab & Haryana-specific)

```yaml
paper_size: A4
paper_type: "watermarked plain paper OR clearly legible properly-spaced computer print"
font_family: "Times New Roman"
font_size_body: 14
line_spacing: 2.0                           # DOUBLE spacing per Punjab & Haryana HC Volume V Rules
left_margin_cm: 4
right_margin_cm: 2.5
top_margin_cm: 2.5
bottom_margin_cm: 2.5
```

**LOAD-BEARING:** Punjab & Haryana HC Rules — "Annexures to writ petitions shall be in the English language and shall be typed in **double spacing on one side of the paper only on watermarked plain paper** (or in legible properly spaced with proper font size computer prints)."

## Section 10 — Accompanying-application requirements

```yaml
accompanying_applications_per_case_type:
  civil_wp_draft:
    - stay_application                      # Common in P&H HC writ practice
```

## Section 12 — Court-Fees Act citation

```yaml
state_court_fees_act_citation: |
  Schedule I of the Court-Fees Act, 1870 (as extended to Punjab and Haryana, and as amended by the State)
```

---

## Special Punjab & Haryana HC notes

1. **Double spacing on watermarked paper is non-negotiable.** Failure = Registry rejection.
2. **Separate annexure prefixes for petitioner (P/) and respondent (R/)** — do not mix.
3. **Vakalatnama:** standard P&H format with advocate's enrolment number.
