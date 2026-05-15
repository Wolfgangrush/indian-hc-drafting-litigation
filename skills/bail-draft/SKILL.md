---
name: bail-draft
description: Draft a Regular Bail Application before any Indian High Court (bench-specific values sourced from `<case-folder>/bench-config.md`) under Section 439 CrPC / Section 483 BNSS. Most-validated bench at v0.1.0-alpha is Bombay HC Nagpur. Produces .docx with Main Application + Index + Synopsis + List of Annexures, rendered in the user's bench's idiom. Auto-fires on "draft bail" or "draft regular bail".
allowed-tools: Read, Write, Edit, Bash, Glob
---

# Bail Application Draft Skill

Extends: `${CLAUDE_PLUGIN_ROOT}/skills/_hc_pleading_base/SKILL.md`
Common rules: `${CLAUDE_PLUGIN_ROOT}/skills/_drafting_common/SKILL.md`

## Case-type metadata

```yaml
case_type_line: CRIMINAL BAIL APPLICATION
case_short_code: BA
hc_taxonomy_match: BA
statutory_opening: |
  APPLICATION UNDER SECTION 439 OF CODE OF CRIMINAL PROCEDURE, 1973
  READ WITH SECTION 483 OF BHARATIYA NAGARIK SURAKSHA SANHITA, 2023
  FOR REGULAR BAIL
accompanying_applications: []   # standalone
typical_annexure_order:
  - A: Copy of FIR
  - B: Copy of remand orders / earlier bail rejection orders
  - C: Charge sheet (if filed)
```

## Format reference

🟡 **Place case-type-specific format text in the file referenced below.**

`${CLAUDE_PLUGIN_ROOT}/skills/bail-draft/format-from-user.md`

## Hard rules

All rules from `_drafting_common/SKILL.md` apply.
