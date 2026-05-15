# bench-config — Allahabad High Court

**Validation depth:** Researched · awaiting Registry validation.
**Source authorities:** Allahabad High Court Rules (Rules of the Court, 1952); Allahabad HC Schedule III Forms 1-100.

---

## Section 1 — Court identification

```yaml
high_court: "High Court of Judicature at Allahabad"
bench: "Principal Seat (Allahabad/Prayagraj)"  # Also Lucknow Bench
state: "Uttar Pradesh"
court_header_line: |
  IN THE HIGH COURT OF JUDICATURE AT ALLAHABAD.
```

For Lucknow Bench: `IN THE HIGH COURT OF JUDICATURE AT ALLAHABAD, LUCKNOW BENCH AT LUCKNOW.`

## Section 2 — Procedural Rules

```yaml
high_court_rules: |
  Allahabad High Court Rules (Rules of the Court, 1952)
schedule_forms: |
  Volume II of the High Court Rules — Schedule III Forms 1-100 (case-type proformas)
```

## Section 3-6 — Cause Title, separator, annexure

```yaml
parties_separator: "...Versus..."
section_headers_style: title-case
annexure_prefix: "Annexure-"
annexure_letter_omissions: []
respondent_annexure_prefix: ""
```

## Section 7 — Counsel block

```yaml
counsel_place: "ALLAHABAD"                    # or "LUCKNOW" for Lucknow Bench
counsel_block_template: |
  ALLAHABAD                                  ([NAME], Advocate)
  DATE: <DD.MM.YYYY>                         Bar Council of UP Enrolment No. [____]
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
  Schedule I of the Uttar Pradesh Court-Fees Act, 1870 (as amended by UP)
```

---

## Special Allahabad HC notes

1. **Schedule III Forms 1-100 are load-bearing for specific case types.** Many case types have a prescribed Form (Form 47 for affidavit verification, etc.). Verify case-type-specific Form before drafting.
2. **Largest HC by case volume in India** — Registry is particular about Form-compliance.
3. The Allahabad HC Rules 1952 also apply (with adaptations) at the **Uttarakhand HC** until Uttarakhand publishes its own Rules.
