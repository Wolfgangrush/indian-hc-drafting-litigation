---
name: civil-wp-draft
description: Draft a Civil Writ Petition before any Indian High Court (bench-specific values sourced from `<case-folder>/bench-config.md`) under Articles 226 / 227 of the Constitution of India. Most-validated bench at v0.1.0-alpha is Bombay HC Nagpur; other Indian HCs supported via bench-config exemplars in `${CLAUDE_PLUGIN_ROOT}/bench-config/exemplars/`. Produces .docx containing Main Petition + Index + Synopsis + List of Annexures + (optional) Stay Application, rendered in the user's bench's idiom. Auto-fires on "draft civil wp" or "draft writ petition".
allowed-tools: Read, Write, Edit, Bash, Glob
---

# Civil Writ Petition Draft Skill

Extends: `${CLAUDE_PLUGIN_ROOT}/skills/_hc_pleading_base/SKILL.md`
Common rules: `${CLAUDE_PLUGIN_ROOT}/skills/_drafting_common/SKILL.md`

## Case-type metadata

```yaml
case_type_line: WRIT PETITION
case_short_code: WP
hc_taxonomy_match: WP / SPLCA
statutory_opening: |
  WRIT PETITION UNDER ARTICLE 226 / 227 OF THE CONSTITUTION OF INDIA
  (filled per case — 226 alone, 227 alone, or 226 read with 227)
accompanying_applications:
  - stay_application          # only if interim relief sought
typical_annexure_order:
  - A: Copy of impugned order/action being challenged
  - B: Representation/notice (where exhausted alternative remedy)
  - C: Replies received (where applicable)
  - Subsequent: documentary support for grounds
```

## Format reference

🟡 **Place case-type-specific format text in the file referenced below.**

The user pastes the canonical Civil WP format into:
`${CLAUDE_PLUGIN_ROOT}/skills/civil-wp-draft/format-from-user.md`

DO NOT assume language. Fail-stop until format-from-user.md exists.

## Hard rules

All rules from `_drafting_common/SKILL.md` apply.
