# bench-config — Patna High Court

**Validation depth:** Researched · awaiting Registry validation.
**Source authorities:** Patna High Court Rules (Chapter IIIA); Patna HC Appendix A(i) — civil proforma / A(ii) — criminal proforma.

---

## Section 1 — Court identification

```yaml
high_court: "Patna High Court"
bench: "Principal Seat (Patna)"
state: "Bihar"
court_header_line: |
  IN THE HIGH COURT OF JUDICATURE AT PATNA.
```

## Section 2 — Procedural Rules

```yaml
high_court_rules: |
  Patna High Court Rules (Chapter IIIA — Writ procedure)
appendix_proforma:
  civil: "Appendix A(i)"
  criminal: "Appendix A(ii)"
```

## Section 3-6

```yaml
parties_separator: "...Versus..."
section_headers_style: title-case
annexure_prefix: "Annexure P"                 # "Annexure P1, P2, P3" (no slash; seriatim numbering)
respondent_annexure_prefix: "Annexure R"      # "Annexure R1, R2"
annexure_letter_omissions: []
inline_marker_template: |
  ...a true copy whereof is annexed hereto and marked as Annexure P[N]
```

## Section 7 — Counsel block

```yaml
counsel_place: "PATNA"
counsel_block_template: |
  PATNA                                      ([NAME], Advocate)
  DATE: <DD.MM.YYYY>                         Bar Council of Bihar Enrolment No. [____]
                                             COUNSEL FOR THE [PETITIONER/RESPONDENT]
```

## Section 12 — Court-Fees Act citation

```yaml
state_court_fees_act_citation: |
  Schedule I of the Court-Fees Act, 1870 (as extended to Bihar and amended)
```

---

## Special Patna HC notes

1. **Presentation proforma:** civil matters require Appendix A(i) proforma; criminal matters require Appendix A(ii). Both ensure case-title, parties, and reliefs are captured systematically.
2. **Index + Synopsis required** for every writ petition.
3. **Synopsis** = concise summary of facts, grounds, relief sought, in chronological order.
