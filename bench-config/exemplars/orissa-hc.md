# bench-config — Orissa High Court

**Validation depth:** Researched · awaiting Registry validation.
**Source authorities:** Orissa High Court Rules; Orissa HC Appendix I (sample form).

---

## Section 1 — Court identification

```yaml
high_court: "High Court of Orissa"
bench: "Principal Seat (Cuttack)"
state: "Odisha"
court_header_line: |
  IN THE HIGH COURT OF ORISSA AT CUTTACK.
```

## Section 2 — Procedural Rules

```yaml
high_court_rules: |
  Orissa High Court Rules (Chapter XV)
sample_proforma: |
  Orissa HC Appendix I, Rule 3 (sample form for writ petition)
```

## Section 3-6

```yaml
parties_separator: "-Versus-"
section_headers_style: title-case
annexure_prefix: "Annexure P/"                # "Annexure P/1, P/2, P/3"
respondent_annexure_prefix: "Annexure R/"
annexure_letter_omissions: []
inline_marker_template: |
  ...as stated in the letter dated <DD.MM.YYYY> (Annexure P/[N])
```

## Section 7 — Counsel block

```yaml
counsel_place: "CUTTACK"
counsel_block_template: |
  CUTTACK                                    ([NAME], Advocate)
  DATE: <DD.MM.YYYY>                         Bar Council of Odisha Enrolment No. [____]
                                             COUNSEL FOR THE [PETITIONER/RESPONDENT]
```

## Section 12 — Court-Fees Act citation

```yaml
state_court_fees_act_citation: |
  Schedule I of the Odisha Court-Fees Act
```

---

## Special Orissa HC notes

1. **Cause of action statement:** Orissa HC Rules require stating cause of action and reasons for any delayed filing.
2. **Description of parties:** age, father/husband's name, residential address with contact details, and details of each opposite party in chronological order.
3. **Annexure marking:** strictly P/N (petitioner) and R/N (respondent) — distinct marking system to avoid filing defects.
