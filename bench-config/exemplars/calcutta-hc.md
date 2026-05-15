# bench-config — Calcutta High Court

**Validation depth:** Researched · awaiting Registry validation.
**Source authorities:** Rules of the High Court at Calcutta (Original Side) 1914; Appellate Side Rules of the High Court at Calcutta; Calcutta HC Practice Directions.

---

## Section 1 — Court identification

```yaml
high_court: "High Court at Calcutta"
bench: "Principal Seat (Kolkata)"            # Also has a Circuit Bench at Port Blair (Andaman & Nicobar)
state: "West Bengal, Andaman and Nicobar Islands"
court_header_line: |
  IN THE HIGH COURT AT CALCUTTA.
```

For Port Blair Circuit Bench: `IN THE HIGH COURT AT CALCUTTA, CIRCUIT BENCH AT PORT BLAIR.`

## Section 2 — Procedural Rules

```yaml
original_side_rules: |
  Rules of the High Court at Calcutta (Original Side), 1914
appellate_side_rules: |
  Appellate Side Rules of the High Court at Calcutta
```

Calcutta HC has the oldest Original Side Rules in India (1914) and a strong OS/AS divide. The OS retains its own Advocate-on-Record concept similar to the Supreme Court.

## Section 3-5 — Cause Title, separator, salutation

```yaml
parties_separator: "-Versus-"
section_headers_style: title-case
salutation_opener: |
  The humble petition of the Petitioner above-named most respectfully showeth:
```

## Section 6 — Annexure marker convention

```yaml
annexure_prefix: "Annexure-"
annexure_letter_omissions: []
respondent_annexure_prefix: ""
inline_marker_template: |
  ...a true copy whereof is annexed hereto and marked as Annexure-[A/B/C]
annexure_column_label: "Annexure"
```

## Section 7 — Counsel block

```yaml
counsel_place: "KOLKATA"
counsel_block_template: |
  KOLKATA                                    ([NAME], Advocate)
  DATE: <DD.MM.YYYY>                         Bar Council of West Bengal Enrolment No. [____]
                                             COUNSEL FOR THE [PETITIONER/RESPONDENT]
```

For Original Side matters: counsel block includes the AOR designation.

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

## Section 12 — Court-Fees Act citation

```yaml
state_court_fees_act_citation: |
  Schedule I of the West Bengal Court-Fees Act, 1971
```

---

## Special Calcutta HC notes

1. **Original Side AOR system:** OS commercial / admiralty / testamentary matters require an Advocate-on-Record (similar to SC). AS matters do not.
2. **Income-Tax appendix:** OS Rules 1914 Appendix 14 governs income tax matters separately.
3. **Vakalatnama:** standard format with Bar Council enrolment.
4. **Letters Patent jurisdiction:** Calcutta HC retains certain Letters Patent appeals.
