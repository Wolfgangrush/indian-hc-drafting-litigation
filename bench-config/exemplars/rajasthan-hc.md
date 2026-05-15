# bench-config — High Court of Judicature for Rajasthan

**Validation depth:** Researched · awaiting Registry validation.
**Source authorities:** Rules of the High Court of Judicature for Rajasthan, 1952; Rajasthan HC Handbook 2015.

---

## Section 1 — Court identification

```yaml
high_court: "High Court of Judicature for Rajasthan"
bench: "Principal Seat (Jodhpur)"             # Also has Jaipur Bench
state: "Rajasthan"
court_header_line: |
  IN THE HIGH COURT OF JUDICATURE FOR RAJASTHAN, JODHPUR.
```

For Jaipur Bench: `IN THE HIGH COURT OF JUDICATURE FOR RAJASTHAN, JAIPUR BENCH, JAIPUR.`

## Section 2 — Procedural Rules

```yaml
high_court_rules: |
  Rules of the High Court of Judicature for Rajasthan, 1952
```

## Section 3-6

```yaml
parties_separator: "...Versus..."
section_headers_style: title-case
annexure_prefix: "Annexure P-"                # "Annexure P-1, P-2, P-3"
respondent_annexure_prefix: "Annexure R-"     # "Annexure R-1, R-2"
annexure_letter_omissions: []
inline_marker_template: |
  ...a true copy whereof is annexed hereto and marked as Annexure P-[N]
```

## Section 7 — Counsel block

```yaml
counsel_place: "JODHPUR"                      # or "JAIPUR" for Jaipur Bench
counsel_block_template: |
  JODHPUR                                    ([NAME], Advocate)
  DATE: <DD.MM.YYYY>                         Bar Council of Rajasthan Enrolment No. [____]
                                             COUNSEL FOR THE [PETITIONER/RESPONDENT]
```

## Section 9 — Paper size and Registry formatting

```yaml
paper_size: A4
font_family: "Times New Roman"
font_size_body: 14
line_spacing: 1.5
```

## Section 12 — Court-Fees Act citation

```yaml
state_court_fees_act_citation: |
  Schedule I of the Rajasthan Court-Fees and Suits Valuation Act, 1961
```
