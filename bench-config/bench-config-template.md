# bench-config-template.md

This is a **template**. Copy this file into your case folder, rename to `bench-config.md`, and fill in the values for your specific High Court bench. The plugin's Format and Drafter agents read this file at run-time to render the pleading in your bench's idiom.

**Do not edit this template in the plugin folder.** Always work on a copy inside your case folder.

---

## Section 1 — Court identification

```yaml
high_court: "Bombay High Court"          # or "Madras High Court" / "Calcutta High Court" / etc.
bench: "Nagpur Bench"                    # or "Principal Bench (Mumbai)" / "Aurangabad Bench" / "Goa Bench" / N/A
state: "Maharashtra"
court_header_line: |
  IN THE HIGH COURT OF JUDICATURE AT BOMBAY BENCH AT NAGPUR.
                                          # Exact line as accepted by your Registry.
                                          # For Bombay Principal Bench: "IN THE HIGH COURT OF JUDICATURE AT BOMBAY."
                                          # For Madras HC: "IN THE HIGH COURT OF JUDICATURE AT MADRAS."
                                          # For Calcutta HC: "IN THE HIGH COURT AT CALCUTTA."
                                          # For Delhi HC: "IN THE HIGH COURT OF DELHI AT NEW DELHI."
                                          # For Karnataka HC: "IN THE HIGH COURT OF KARNATAKA AT BANGALORE."
                                          # Pull from your bench's Practice Notes if uncertain.
```

## Section 2 — Procedural Rules

```yaml
appellate_side_rules: |
  Bombay High Court (Appellate Side) Rules, 1960
                                          # Each HC has its own AS / OS Rules.
                                          # Examples:
                                          # · Delhi HC Rules (Original Side) 2018
                                          # · Madras HC Original Side Rules 1956
                                          # · Calcutta HC Original Side Rules 1914
                                          # · Karnataka HC Rules 1959
original_side_rules: |
  Bombay High Court (Original Side) Rules
                                          # Where applicable (Bombay Principal Bench + a few other HCs maintain Original Side jurisdiction).
                                          # For HCs without Original Side jurisdiction, leave blank.
pil_rules: |
  Bombay High Court PIL Rules, 2010       # If your bench has specific PIL Rules, cite them.
                                          # Examples:
                                          # · Delhi HC (Public Interest Litigation) Rules, 2010
                                          # · High Court of Madras Public Interest Litigation Rules, 2014
```

## Section 3 — Cause Title and Parties

```yaml
case_number_format: |
  [CASE TYPE] NO._______/[YEAR]
                                          # Some HCs use [Year]/[Sequence] format instead.
                                          # Some use Roman numerals for case types (e.g., "W.P. (C)").
act_code_line: yes                        # Most HCs require an "ACT CODE-" line after the case number.
                                          # Set to "no" if your bench omits this.
parties_separator: "///VERSUS///"         # Variations: "...VERSUS...", "///VERSUS///", "vs.", "...vs..."
                                          # Bombay HC: prefer "///VERSUS///" for appeals; "...VERSUS..." for applications.
```

## Section 4 — Section headers

```yaml
section_headers_style: spaced             # Bombay HC convention: spaced ("F A C T S", "G R O U N D S").
                                          # Many other HCs use Title Case bold: "Facts", "Grounds".
                                          # Set "spaced" for Bombay-style, "title-case" for other.
```

## Section 5 — Salutation and connective phrases

```yaml
salutation_opener: |
  The [Applicant/Petitioner/Appellant] named above most humbly and respectfully begs to submit as under: -
                                          # Variations across HCs are slight; supply yours if it differs.
prayer_opener: |
  It is, therefore, prayed that this Hon'ble Court may kindly be pleased to:
                                          # Variations are slight.
prayer_catchall_last_clause: |
  Grant any other relief deems fit just and proper in the facts and circumstances of the case in favour of the [petitioner/appellant].
```

## Section 6 — Annexure marker convention

```yaml
annexure_prefix: "ANNEXURE-"              # Bombay HC convention. Variations:
                                          # · Delhi HC: "ANNEXURE A-1" (often)
                                          # · Madras HC: "Document No. 1" sometimes, or "Annexure-A"
                                          # · Calcutta HC: "Annexure-A"
                                          # · Supreme Court (separate plugin): "P-1" / "R-1"
collective_annexure_suffix: " (Colly)"    # for grouped depositions / documents
inline_marker_template: |
  ...is annexed herewith and marked as **ANNEXURE-[A/B/C]**
```

## Section 7 — Counsel block

```yaml
counsel_block_template: |
  [Place]                      ([NAME], Adv.)
  DATE:   .__.YYYY             COUNSEL FOR [APPELLANT/PETITIONER]
                                          # The exact layout varies per bench's Practice Note.
                                          # Bombay HC Nagpur: as above.
                                          # Delhi HC: typically includes the advocate's enrolment number.
                                          # Madras HC: similar.
counsel_for_designation_options:
  - "COUNSEL FOR THE PETITIONER"
  - "COUNSEL FOR THE APPLICANT"
  - "COUNSEL FOR THE APPELLANT"
  - "PARTY-IN-PERSON"             # where appearing without counsel
```

## Section 8 — Affidavit dispensation

```yaml
affidavit_dispensation_note: |
  Note: The [Appellant] is in jail therefore his affidavit may kindly be dispensed with.
                                          # Used in criminal appeals where the appellant is in custody.
                                          # Phrasing varies slightly per bench's Practice Note.
```

## Section 9 — Paper size and Registry formatting

```yaml
paper_size: A4                            # Most HCs: A4. Some Original Side practices: Legal.
font_family: "Times New Roman"
font_size_body: 14                        # Most HCs: 14pt. Some: 12pt.
line_spacing: 1.5
left_margin_cm: 4                         # Binding side.
right_margin_cm: 2.5
top_margin_cm: 2.5
bottom_margin_cm: 2.5
```

## Section 10 — Accompanying-application requirements

```yaml
accompanying_applications_per_case_type:
  pil_draft:
    - stay_application                    # if interim relief sought
  civil_wp_draft:
    - stay_application                    # sometimes
  criminal_appeal_draft:
    - suspension_of_sentence              # mandatory if appellant is in custody
    - condonation_of_delay                # if filed late
  bail_draft: []                          # typically standalone
  anticipatory_bail_draft: []
  application_482_draft: []
                                          # Your bench may require additional applications per case type.
                                          # Add them here.
```

## Section 11 — Limitation references

```yaml
limitation_act_schedule_article: |
  Limitation Act 1963, Schedule, Article [N]
                                          # Specific Article depends on the case type.
                                          # Drafter computes per case-facts and case-type.
```

## Section 12 — State Court-Fees Act citation

```yaml
state_court_fees_act_citation: |
  Schedule [N], Article [N] of the [State] Court-Fees Act, [Year]
                                          # Maharashtra: "Schedule I, Article 1 of the Bombay Court-Fees Act, 1959, as amended"
                                          # Karnataka: "Schedule I of the Karnataka Court-Fees and Suits Valuation Act, 1958"
                                          # Tamil Nadu: "Schedule I of the Tamil Nadu Court-Fees and Suits Valuation Act, 1955"
                                          # Delhi: "Schedule I of the Court-Fees Act, 1870 (as extended to Delhi)"
                                          # etc.
```

---

## How to use this file

1. **Copy this template to your case folder:**
   ```bash
   cp <plugin-folder>/bench-config/bench-config-template.md <your-case-folder>/bench-config.md
   ```

2. **Open `bench-config.md` in your editor** and replace every example value with your bench's actual values.

3. **Verify each value against your bench's Practice Notes / Registry directions / Civil Manual.** If unsure, leave the default (which is the Bombay HC Nagpur value) and ask the Registry at filing.

4. **Save the file inside your case folder.** The plugin's Format agent reads `<case-folder>/bench-config.md` at run-time.

5. **For repeat-use:** save your filled-in bench-config to a personal templates folder so you can reuse it across cases. The plugin does not store your bench-config; it expects to find one in each case folder.

---

## Contributing bench-config templates

If you practise regularly before a non-Bombay High Court bench, please contribute your filled-in bench-config back to the plugin via a GitHub Issue. Over time, this folder will contain validated templates for every Indian HC bench, lowering the setup burden for advocates joining the plugin's community.

When contributing, do NOT include any case-specific information — only the bench's standard procedural conventions.
