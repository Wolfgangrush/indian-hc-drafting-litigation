---
name: criminal-appeal-draft
description: Draft a Criminal Appeal before any Indian High Court (bench-specific values sourced from `<case-folder>/bench-config.md`) under Section 374(2) CrPC + Section 415(2) BNSS. Most-validated bench at v0.1.0-alpha is Bombay HC Nagpur. Produces .docx containing Main Appeal + Index + Synopsis + List of Annexures + Suspension of Sentence application + Condonation of Delay application (if late), rendered in the user's bench's idiom. Auto-fires on "draft criminal appeal" or "draft cri appeal".
allowed-tools: Read, Write, Edit, Bash, Glob
---

# Criminal Appeal Draft Skill

Extends: `${CLAUDE_PLUGIN_ROOT}/skills/_hc_pleading_base/SKILL.md`
Common rules: `${CLAUDE_PLUGIN_ROOT}/skills/_drafting_common/SKILL.md`

## Case-type metadata

```yaml
case_type_line: CRIMINAL APPEAL
case_short_code: APEAL
hc_taxonomy_match: APEAL
statutory_opening: |
  CRIMINAL APPEAL UNDER SECTION 374(2) OF CODE OF CRIMINAL PROCEDURE
  READ WITH SECTION 415 (2) OF THE BHARTIYA NAGARIK SURAKSHA SANHITA, 2023.
accompanying_applications:
  - suspension_of_sentence    # always
  - condonation_of_delay      # only if filed beyond 60-day limitation
typical_annexure_order:
  - A: Copy of Judgment and Order of conviction (impugned)
  - B (Colly): Copies of depositions of prosecution witnesses
  - C: FIR (where relevant to grounds)
  - D: Other documentary evidence as required
```

## Format reference

🟡 **Place case-type-specific format text in the file referenced below.**

The user pastes the canonical Criminal Appeal format text into:
`${CLAUDE_PLUGIN_ROOT}/skills/criminal-appeal-draft/format-from-user.md`

That file holds the EXACT language patterns the user uses for:
- The opening fact paragraph (impugned order recital)
- The "prosecution case in nutshell" paragraph (where applicable)
- The standard grounds opener: "The learned Special Court erred in law and facts of the case..."
- The reservation clause: "That the appellants reserve its rights to raise additional grounds..."
- The limitation declaration: "That, the appellants have filed instant criminal appeal within limitation..."
- The standard prayer: "Quash and set aside the Judgment and Order of conviction dated <date>..."
- The "in jail" affidavit dispensation note
- The "Notes on Limitation" block

DO NOT assume any of this language. Fail-stop until format-from-user.md exists.

## Accompanying applications (drafted in same .docx)

### Suspension of Sentence Application
Cause title: `CRIMINAL APPLICATION (APPA) NO. ______/<year> IN CRIMINAL APPEAL NO._______/<year>`
Statutory opening: "APPLICATION UNDER SECTION 389 (1) OF CODE OF CRIMINAL PROCEDURE AND 430 (1) OF THE BHARATIYA NAGARIK SURAKSHA SANHITA, 2023 FOR SUSPENSION OF SENTENCE AND FOR BAIL."
Format text from: `format-from-user.md` → `suspension_app:` section.

### Condonation of Delay Application (only if late)
Cause title: same APPA-in-APEAL pattern.
Statutory opening: "APPLICATION UNDER SECTION 5 OF LIMITATION ACT FOR CONDONATION OF DELAY OF ____ DAYS IN FILING APPEAL."
Format text from: `format-from-user.md` → `condonation_app:` section.

## Pipeline invocation

When the user says "draft criminal appeal" while in a case folder:
1. Reader runs first → produces `case-facts.md`
2. Format runs → loads this skill + base + format-from-user.md → produces `format-shell.md`
3. Drafter → produces `draft-v1.docx`
4. Verifier → produces `verification-report.md`
5. Refiner → produces `draft-v2.docx`
6. Overseer → produces `opposing-notes.md` + `final-draft.docx`

The user reviews `final-draft.docx` in Word with tracked changes.

## Hard rules

All rules from `_drafting_common/SKILL.md` apply. In particular:
- ❌ NEVER assume format language. Always read `format-from-user.md`.
- ❌ NEVER cite case law from training data. Use "Will be cited at the time of hearing."
- ❌ NEVER write to palace.
- ❌ NEVER delete/rename/overwrite anything in case folder. Only WRITE new files.
