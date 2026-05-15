---
name: second-appeal-draft
description: Draft a Second Appeal (Civil) before any Indian High Court (bench-specific values sourced from `<case-folder>/bench-config.md`) under Section 100 CPC. Substantial question of law is the gateway requirement. Most-validated bench at v0.1.0-alpha is Bombay HC Nagpur. Produces .docx with Main Appeal + Index + Synopsis + List of Annexures + (optional) Stay Application, rendered in the user's bench's idiom. Auto-fires on "draft second appeal" or "draft SA".
allowed-tools: Read, Write, Edit, Bash, Glob
---

# Second Appeal Draft Skill

Extends: `${CLAUDE_PLUGIN_ROOT}/skills/_hc_pleading_base/SKILL.md`
Common rules: `${CLAUDE_PLUGIN_ROOT}/skills/_drafting_common/SKILL.md`

## Case-type metadata

```yaml
case_type_line: SECOND APPEAL
case_short_code: SA
hc_taxonomy_match: SA
statutory_opening: |
  SECOND APPEAL UNDER SECTION 100 OF CODE OF CIVIL PROCEDURE, 1908
accompanying_applications:
  - stay_application          # where interim relief sought
typical_annexure_order:
  - A: Copy of First Appeal Court judgment (impugned)
  - B: Copy of trial court judgment
  - Subsequent: documentary support for substantial questions of law
substantial_question_of_law: REQUIRED   # SA is not maintainable without substantial question of law u/s 100 CPC
```

## Format reference

🟡 **Place case-type-specific format text in the file referenced below.**

`${CLAUDE_PLUGIN_ROOT}/skills/second-appeal-draft/format-from-user.md`

## Hard rules

All rules from `_drafting_common/SKILL.md` apply. Additionally:
- ❌ NEVER draft a Second Appeal without a clearly articulated substantial question of law. If facts don't support one, halt and halt and ask the user.
