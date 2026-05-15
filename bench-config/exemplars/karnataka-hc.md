# bench-config — Karnataka High Court

**Validation depth:** Researched · awaiting Registry validation.
**Source authorities:** Karnataka High Court Rules **1959**; Karnataka HC Writ Proceedings Rules **1977**; Karnataka HC Practice Directions.

---

## Section 1 — Court identification

```yaml
high_court: "High Court of Karnataka"
bench: "Principal Seat (Bangalore)"        # Also has Benches at Dharwad and Kalaburagi
state: "Karnataka"
court_header_line: |
  IN THE HIGH COURT OF KARNATAKA AT BANGALORE.
```

For other benches:
- Dharwad Bench: `IN THE HIGH COURT OF KARNATAKA, DHARWAD BENCH AT DHARWAD.`
- Kalaburagi Bench: `IN THE HIGH COURT OF KARNATAKA, KALABURAGI BENCH AT KALABURAGI.`

## Section 2 — Procedural Rules

```yaml
appellate_side_rules: |
  Karnataka High Court Rules, 1959
writ_proceedings_rules: |
  Karnataka High Court Writ Proceedings Rules, 1977
```

## Section 3 — Cause Title and Parties

```yaml
case_number_format: |
  [CASE TYPE] No. _____ of [YEAR]
act_code_line: no
parties_separator: "...VERSUS..."          # Karnataka HC default
```

## Section 4 — Section headers

```yaml
section_headers_style: title-case          # "Facts", "Grounds", "Synopsis" — Title Case bold
```

## Section 5 — Salutation and connective phrases

```yaml
salutation_opener: |
  The humble Petitioner above-named most respectfully showeth:
prayer_opener: |
  It is, therefore, most respectfully prayed that this Hon'ble Court may be pleased to:
```

## Section 6 — Annexure marker convention (CRITICAL — Karnataka-specific rule)

```yaml
annexure_prefix: "Annexure-"
annexure_letter_omissions:
  - "I"                                     # CRITICAL: Karnataka HC Writ Proceedings Rules 1977 — letter I OMITTED
respondent_annexure_prefix: ""
collective_annexure_suffix: " (Colly.)"
inline_marker_template: |
  ...a copy whereof is produced herewith and marked as **Annexure-[A/B/C]**
annexure_column_label: "Annexure"
```

**LOAD-BEARING:** Karnataka HC Writ Proceedings Rules 1977 — "every annexure produced by the petitioner along with the writ petition shall be marked in the alphabetical order, namely, as annexure 'A', annexure 'B', and so on (**omitting the alphabet I**)."

Annexure sequence: A, B, C, D, E, F, G, H, **J** (NOT I), K, L, M, N, O, P, Q, R, S, T, U, V, W, X, Y, Z, AA, BB, etc.

## Section 7 — Counsel block

```yaml
counsel_place: "BANGALORE"                  # or DHARWAD / KALABURAGI for other benches
counsel_block_template: |
  BANGALORE                                 ([NAME], Advocate)
  DATE: <DD.MM.YYYY>                        Bar Council Enrolment No. [____]
                                            COUNSEL FOR THE [PETITIONER/RESPONDENT]
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
  civil_wp_draft:
    - stay_application                      # Common in Karnataka HC writ practice
    - urgent_hearing_application
```

## Section 12 — Court-Fees Act citation

```yaml
state_court_fees_act_citation: |
  Schedule I of the Karnataka Court-Fees and Suits Valuation Act, 1958
```

---

## Special Karnataka HC notes

1. **Letter I omission is non-negotiable.** Any annexure marked with letter I will be rejected by the Karnataka HC Registry.
2. **Notice to respondents:** copies of the petition, affidavit, and all annexures must be delivered to each respondent along with the notice.
3. **Vakalatnama:** standard Karnataka format; advocate's enrolment number must appear.
