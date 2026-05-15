# bench-config — Madras High Court

**Validation depth:** Researched · awaiting Registry validation.
**Source authorities:** Madras High Court Original Side Rules 1956; Madras High Court Appellate Side Rules; Madras HC Practice Directions; Madras HC Party-in-Person Rules 2019.

---

## Section 1 — Court identification

```yaml
high_court: "High Court of Judicature at Madras"
bench: "Principal Seat (Chennai)"           # Also has a Madurai Bench
state: "Tamil Nadu, Puducherry"
court_header_line: |
  IN THE HIGH COURT OF JUDICATURE AT MADRAS.
```

For Madurai Bench: `IN THE HIGH COURT OF JUDICATURE AT MADRAS, MADURAI BENCH AT MADURAI.`

## Section 2 — Procedural Rules

```yaml
original_side_rules: |
  Madras High Court Original Side Rules, 1956
appellate_side_rules: |
  Madras High Court Appellate Side Rules
practice_directions: |
  Madras HC Practice Directions; Madras HC Party-in-Person Rules, 2019
```

Madras HC has a strong Original Side / Appellate Side divide. OS matters (commercial / admiralty / testamentary / certain writs) follow OS Rules 1956. AS matters follow AS Rules.

## Section 3-5 — Cause Title, separator, salutation

```yaml
parties_separator: "...Vs..."
section_headers_style: title-case
salutation_opener: |
  The humble petition of the Petitioner above-named most respectfully submits as follows:
```

## Section 6 — Annexure marker convention

```yaml
annexure_prefix: "Document No. "             # Madras OS practice often uses "Document No. 1, 2, 3" instead of letters
annexure_prefix_alternative: "Annexure-"     # Annexure-A/B/C also accepted on the Appellate Side
annexure_letter_omissions: []
respondent_annexure_prefix: ""
inline_marker_template: |
  ...a copy whereof is filed herewith and marked as Document No. [1/2/3] (or Annexure-[A/B/C] on Appellate Side)
annexure_column_label: "Annexure / Document No."
```

## Section 7 — Counsel block

```yaml
counsel_place: "CHENNAI"                     # or "MADURAI" for Madurai Bench
counsel_block_template: |
  CHENNAI                                    ([NAME], Advocate)
  DATE: <DD.MM.YYYY>                         Bar Council of Tamil Nadu & Puducherry Enrolment No. [____]
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

## Section 12 — Court-Fees Act citation

```yaml
state_court_fees_act_citation: |
  Schedule I of the Tamil Nadu Court-Fees and Suits Valuation Act, 1955
```

---

## Special Madras HC notes

1. **Original Side / Appellate Side divide is significant.** For OS commercial matters: OS Rules 1956 + AOR concept on OS. For AS matters: AS Rules + standard advocate appearance.
2. **For matters from Puducherry:** same Madras HC jurisdiction; cause title remains.
3. **For matters from Pondicherry State Courts on appeal:** filed at Madras HC.
4. **Tamil Nadu Court-Fees Act 1955:** load-bearing for all civil suit valuations.
