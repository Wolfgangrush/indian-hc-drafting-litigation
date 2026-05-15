# bench-config — High Court for the State of Telangana

**Validation depth:** Researched · awaiting Registry validation.
**Source authorities:** Andhra Pradesh Writ Proceedings Rules 1977 (continues in Telangana post-2019 bifurcation); Andhra Pradesh Civil Rules of Practice and Circular Orders 1990; Telangana HC Practice Directions.

---

## Section 1 — Court identification

```yaml
high_court: "High Court for the State of Telangana"
bench: "Principal Seat (Hyderabad)"
state: "Telangana"
court_header_line: |
  IN THE HIGH COURT FOR THE STATE OF TELANGANA AT HYDERABAD.
```

(Pre-2019 cases that originated at the unified High Court of Judicature at Hyderabad before the AP/Telangana separation may retain the older header in continuing proceedings.)

## Section 2 — Procedural Rules

```yaml
writ_proceedings_rules: |
  Andhra Pradesh Writ Proceedings Rules, 1977 (continues in Telangana)
civil_rules_of_practice: |
  Andhra Pradesh Civil Rules of Practice and Circular Orders, 1990 (continues in Telangana)
```

## Section 3-7 — As per typical HC convention with title-case section heads + standard advocate block

```yaml
parties_separator: "...Versus..."
section_headers_style: title-case
annexure_prefix: "Annexure-"
counsel_place: "HYDERABAD"
counsel_block_template: |
  HYDERABAD                                  ([NAME], Advocate)
  DATE: <DD.MM.YYYY>                         Bar Council Enrolment No. [____]
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
  Schedule I of the Andhra Pradesh Court-Fees and Suits Valuation Act, 1956 (continues in Telangana)
```
