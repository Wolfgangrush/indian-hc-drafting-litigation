---
name: anticipatory-bail-draft
description: Draft an Anticipatory Bail Application before any Indian High Court (bench-specific values sourced from `<case-folder>/bench-config.md`) under Section 438 CrPC / Section 482 BNSS. Most-validated bench at v0.1.0-alpha is Bombay HC Nagpur; other Indian HCs supported via bench-config exemplars (see `${CLAUDE_PLUGIN_ROOT}/bench-config/exemplars/`). Produces .docx with Main Application + Index + Synopsis + List of Annexures, rendered in the user's bench's idiom. Auto-fires on "draft anticipatory bail" or "draft ABA" or "draft pre-arrest bail".
allowed-tools: Read, Write, Edit, Bash, Glob
---

# Anticipatory Bail Application Draft Skill

Extends: `${CLAUDE_PLUGIN_ROOT}/skills/_hc_pleading_base/SKILL.md`
Common rules: `${CLAUDE_PLUGIN_ROOT}/skills/_drafting_common/SKILL.md`

## Case-type metadata

```yaml
case_type_line: CRIMINAL ANTICIPATORY BAIL APPLICATION
case_short_code: ABA
hc_taxonomy_match: ABA
statutory_opening: |
  APPLICATION UNDER SECTION 438 OF CODE OF CRIMINAL PROCEDURE, 1973
  READ WITH SECTION 482 OF BHARATIYA NAGARIK SURAKSHA SANHITA, 2023
  FOR ANTICIPATORY BAIL
accompanying_applications: []   # standalone
typical_annexure_order:
  - A: Copy of FIR
  - B: Notice u/s 41A CrPC / 35 BNSS (where served)
  - Subsequent: documentary support for grounds (medical, employment, etc.)
```

## Format reference

🟡 **Place case-type-specific format text in the file referenced below.**

`${CLAUDE_PLUGIN_ROOT}/skills/anticipatory-bail-draft/format-from-user.md`

## Hard rules

All rules from `_drafting_common/SKILL.md` apply.
