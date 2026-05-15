---
name: contempt-petition-draft
description: Draft a Contempt Petition before any Indian High Court (civil or criminal contempt under the Contempt of Courts Act, 1971; bench-specific values sourced from `<case-folder>/bench-config.md`). Most-validated bench at v0.1.0-alpha is Bombay HC Nagpur. Produces .docx with Main Petition + Index + Synopsis + List of Annexures, rendered in the user's bench's idiom. Auto-fires on "draft contempt" or "draft contempt petition".
allowed-tools: Read, Write, Edit, Bash, Glob
---

# Contempt Petition Draft Skill

Extends: `${CLAUDE_PLUGIN_ROOT}/skills/_hc_pleading_base/SKILL.md`
Common rules: `${CLAUDE_PLUGIN_ROOT}/skills/_drafting_common/SKILL.md`

## Case-type metadata

```yaml
case_type_line: CONTEMPT PETITION
case_short_code: CONP
hc_taxonomy_match: CONP / CP
statutory_opening: |
  CONTEMPT PETITION UNDER SECTIONS 11, 12, 14, 15 OF THE CONTEMPT OF
  COURTS ACT, 1971 READ WITH RULES OF THE HON'BLE HIGH COURT OF
  JUDICATURE AT BOMBAY (NAGPUR BENCH)
  (For [civil / criminal] contempt — fill per case)
accompanying_applications: []
typical_annexure_order:
  - A: Copy of order alleged to have been disobeyed (the order founding contempt)
  - B: Service / receipt evidence (proving knowledge of order)
  - C: Communications evidencing disobedience
  - D: Notice to respondent (where pre-action notice given)
```

## Format reference

🟡 **Place case-type-specific format text in the file referenced below.**

`${CLAUDE_PLUGIN_ROOT}/skills/contempt-petition-draft/format-from-user.md`

## Hard rules

All rules from `_drafting_common/SKILL.md` apply. Additionally:
- ❌ NEVER draft contempt without confirmed wilful disobedience or knowledge of order. Halt if facts don't support that limb.
