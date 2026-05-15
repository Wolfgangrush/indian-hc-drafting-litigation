---
name: first-appeal-draft
description: Draft a First Appeal (Civil) before any Indian High Court (bench-specific values sourced from `<case-folder>/bench-config.md`) under Section 96 CPC read with Order XLI CPC. Most-validated bench at v0.1.0-alpha is Bombay HC Nagpur. Produces .docx containing Main Appeal + Index + Synopsis + List of Annexures + (optional) Stay Application, rendered in the user's bench's idiom. Auto-fires on "draft first appeal" or "draft FA".
allowed-tools: Read, Write, Edit, Bash, Glob
---

# First Appeal Draft Skill

Extends: `${CLAUDE_PLUGIN_ROOT}/skills/_hc_pleading_base/SKILL.md`
Common rules: `${CLAUDE_PLUGIN_ROOT}/skills/_drafting_common/SKILL.md`

## Case-type metadata

```yaml
case_type_line: FIRST APPEAL
case_short_code: FA
hc_taxonomy_match: FA
statutory_opening: |
  FIRST APPEAL UNDER SECTION 96 READ WITH ORDER XLI OF CODE OF CIVIL PROCEDURE, 1908
accompanying_applications:
  - stay_application          # where interim relief sought
  - condonation_of_delay      # where late
typical_annexure_order:
  - A: Copy of impugned decree / judgment of trial court
  - B: Plaint / written statement (where contextually needed)
  - Subsequent: documentary support
```

## Format reference

🟡 **Place case-type-specific format text in the file referenced below.**

`${CLAUDE_PLUGIN_ROOT}/skills/first-appeal-draft/format-from-user.md`

## Hard rules

All rules from `_drafting_common/SKILL.md` apply.
