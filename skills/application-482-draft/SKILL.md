---
name: application-482-draft
description: Draft an Application under Section 482 CrPC / Section 528 BNSS (inherent jurisdiction of any Indian High Court — typically used for quashing FIR / proceedings; bench-specific values sourced from `<case-folder>/bench-config.md`). Most-validated bench at v0.1.0-alpha is Bombay HC Nagpur. Produces .docx with Main Application + Index + Synopsis + List of Annexures, rendered in the user's bench's idiom. Auto-fires on "draft 482" or "draft quashing" or "draft 528 BNSS".
allowed-tools: Read, Write, Edit, Bash, Glob
---

# Application u/s 482 CrPC / 528 BNSS Draft Skill

Extends: `${CLAUDE_PLUGIN_ROOT}/skills/_hc_pleading_base/SKILL.md`
Common rules: `${CLAUDE_PLUGIN_ROOT}/skills/_drafting_common/SKILL.md`

## Case-type metadata

```yaml
case_type_line: CRIMINAL APPLICATION UNDER SECTION 482 CrPC
case_short_code: APPL_482
hc_taxonomy_match: APPL / APPW / APPLN
statutory_opening: |
  APPLICATION UNDER SECTION 482 OF CODE OF CRIMINAL PROCEDURE, 1973
  READ WITH SECTION 528 OF BHARATIYA NAGARIK SURAKSHA SANHITA, 2023
  (For [quashing of FIR / proceedings / impugned order — fill per case])
accompanying_applications:
  - stay_application          # where stay of proceedings sought
typical_annexure_order:
  - A: Copy of FIR / impugned order being challenged
  - B: Charge sheet (if filed)
  - Subsequent: settlement deeds, compromise affidavits, documentary support
```

## Format reference

🟡 **Place case-type-specific format text in the file referenced below.**

`${CLAUDE_PLUGIN_ROOT}/skills/application-482-draft/format-from-user.md`

## Hard rules

All rules from `_drafting_common/SKILL.md` apply.
