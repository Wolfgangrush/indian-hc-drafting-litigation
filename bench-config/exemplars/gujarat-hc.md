# bench-config — Gujarat High Court

**Validation depth:** Researched · awaiting Registry validation.
**Source authorities:** Gujarat High Court Rules, 1993 (amended 2019); Gujarat HC PIL Rules.

---

## Section 1 — Court identification

```yaml
high_court: "High Court of Gujarat"
bench: "Principal Seat (Ahmedabad)"
state: "Gujarat"
court_header_line: |
  IN THE HIGH COURT OF GUJARAT AT AHMEDABAD.
```

## Section 2 — Procedural Rules

```yaml
high_court_rules: |
  Gujarat High Court Rules, 1993 (amended 2019)
pil_rules: |
  Gujarat High Court PIL Rules
```

## Section 3-6

```yaml
parties_separator: "...Versus..."
section_headers_style: title-case
annexure_prefix: "Annexure-"
annexure_letter_omissions: []
respondent_annexure_prefix: ""
```

## Section 7 — Counsel block

```yaml
counsel_place: "AHMEDABAD"
counsel_block_template: |
  AHMEDABAD                                  ([NAME], Advocate)
  DATE: <DD.MM.YYYY>                         Bar Council of Gujarat Enrolment No. [____]
                                             COUNSEL FOR THE [PETITIONER/RESPONDENT]
```

## Section 9 — Paper size and Registry formatting (CRITICAL — Gujarat-specific)

```yaml
paper_size: "foolscap"                       # Gujarat HC Rules 1993 — durable foolscap paper
paper_alternative: "A4 (if foolscap unavailable; verify Registry acceptance)"
font_family: "Times New Roman"
font_size_body: 14
line_spacing: 1.5
left_margin_inches: 2                        # Gujarat HC Rules 1993 — 2-inch margin
```

**LOAD-BEARING:** Gujarat HC Rules 1993 — "All memoranda of appeals and applications, affidavits, copies and notes supplied by advocates or parties shall be neatly typed on durable **foolscap paper leaving a margin of 2 inches**."

## Section 12 — Court-Fees Act citation

```yaml
state_court_fees_act_citation: |
  Schedule I of the Bombay Court-Fees Act, 1959, as extended to Gujarat
```

(Note: Gujarat State retains the Bombay Court-Fees Act 1959 as the applicable Court-Fees Act, since Gujarat was bifurcated from Bombay State in 1960.)
