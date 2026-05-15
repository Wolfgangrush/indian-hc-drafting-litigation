---
name: criminal-wp-draft
description: Draft a Criminal Writ Petition before any Indian High Court (bench-specific values sourced from `<case-folder>/bench-config.md`) under Articles 226 / 227 of the Constitution. Most-validated bench at v0.1.0-alpha is Bombay HC Nagpur. Produces .docx containing Main Petition + Index + Synopsis + List of Annexures + (optional) Stay Application, rendered in the user's bench's idiom. Auto-fires on "draft criminal wp" or "draft cri writ".
allowed-tools: Read, Write, Edit, Bash, Glob
---

# Criminal Writ Petition Draft Skill

Extends: `${CLAUDE_PLUGIN_ROOT}/skills/_hc_pleading_base/SKILL.md`
Common rules: `${CLAUDE_PLUGIN_ROOT}/skills/_drafting_common/SKILL.md`

## Case-type metadata

```yaml
case_type_line: CRIMINAL WRIT PETITION
case_short_code: WPC
hc_taxonomy_match: WPC / Criminal Writ Petition
statutory_opening: |
  CRIMINAL WRIT PETITION UNDER ARTICLE 226 / 227 OF THE CONSTITUTION OF INDIA
  READ WITH SECTION 482 / 528 BNSS, 2023 (where applicable)
accompanying_applications:
  - stay_application          # where interim relief sought
typical_annexure_order:
  - A: Copy of FIR / impugned order
  - B: Charge sheet (where applicable)
  - Subsequent: documentary support
```

## Format reference

🟡 **Place case-type-specific format text in the file referenced below.**

The user pastes the canonical Criminal WP format into:
`${CLAUDE_PLUGIN_ROOT}/skills/criminal-wp-draft/format-from-user.md`

DO NOT assume language.

## Hard rules

All rules from `_drafting_common/SKILL.md` apply.
