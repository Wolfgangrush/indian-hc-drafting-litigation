# bench-config — High Court of Kerala

**Validation depth:** Researched · awaiting Registry validation.
**Source authorities:** Rules of the High Court of Kerala, 1971; Kerala Judicial Academy Compendium on High Court Procedure.

---

## Section 1 — Court identification

```yaml
high_court: "High Court of Kerala"
bench: "Principal Seat (Ernakulam)"
state: "Kerala, Lakshadweep"
court_header_line: |
  IN THE HIGH COURT OF KERALA AT ERNAKULAM.
```

## Section 2 — Procedural Rules

```yaml
high_court_rules: |
  Rules of the High Court of Kerala, 1971
```

## Section 3-6

```yaml
parties_separator: "...Versus..."
section_headers_style: title-case
annexure_prefix: "Exhibit "                  # Kerala default — "Exhibit P1, Exhibit P2"
annexure_prefix_alternative: "Annexure-"      # Annexure-A/B/C also accepted
respondent_annexure_prefix: "Exhibit R"
annexure_letter_omissions: []
```

## Section 7 — Counsel block

```yaml
counsel_place: "ERNAKULAM"
counsel_block_template: |
  ERNAKULAM                                  ([NAME], Advocate)
  DATE: <DD.MM.YYYY>                         Bar Council of Kerala Enrolment No. [____]
                                             COUNSEL FOR THE [PETITIONER/RESPONDENT]
```

## Section 9 — Paper size and Registry formatting (CRITICAL — Kerala-specific)

```yaml
paper_size: "foolscap"                        # Kerala HC Rules 1971 — foolscap folio paper
paper_alternative: "A4 (if foolscap unavailable; verify Registry acceptance)"
font_family: "Times New Roman"
font_size_body: 14
line_spacing: 1.5
left_margin_cm: 4                             # outer margin ~4cm
right_margin_cm: 1.5                          # inner margin ~1.5cm
binding: "book-stitched"                      # Kerala HC Rules — sheets stitched together bookwise
ink_color: "blue-black"                       # Kerala HC Rules — blue-black ink or typed
```

**LOAD-BEARING:** Kerala HC Rules 1971 — "All petitions, affidavits, memoranda of appeal and other proceedings presented to the Court shall be written in blue-black ink, or type-written or printed, fairly and legibly on stamp paper or on substantial transparent foolscap folio paper, with an **outer-margin of about 4 cm and an inner margin of about 1.5 cm and separate sheets be stitched together bookwise.**"

## Section 12 — Court-Fees Act citation

```yaml
state_court_fees_act_citation: |
  Schedule I of the Kerala Court-Fees and Suits Valuation Act, 1959
```

---

## Special Kerala HC notes

1. **Foolscap paper + book-stitching are non-negotiable** in strict Registry application. Verify with the user's Registry counter before final filing.
2. **Exhibit convention preferred over Annexure** — Kerala HC default.
3. **For matters from Lakshadweep:** same Kerala HC jurisdiction; cause title remains.
