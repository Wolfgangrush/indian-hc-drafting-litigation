---
name: pil-draft
description: Draft a Public Interest Litigation before any Indian High Court (bench-specific values sourced from `<case-folder>/bench-config.md` — each HC has its own PIL Rules: Bombay HC PIL Rules 2010, Delhi HC PIL Rules 2010, Gauhati HC PIL Rules 2011, Gujarat HC PIL Rules, etc.) under Article 226 of the Constitution. Most-validated bench at v0.1.0-alpha is Bombay HC Nagpur. Produces .docx with Main Petition + Index + Synopsis + List of Annexures + (optional) Stay/Interim Relief Application, rendered in the user's bench's idiom. Auto-fires on "draft PIL" or "draft public interest litigation".
allowed-tools: Read, Write, Edit, Bash, Glob
---

# Public Interest Litigation Draft Skill

Extends: `${CLAUDE_PLUGIN_ROOT}/skills/_hc_pleading_base/SKILL.md`
Common rules: `${CLAUDE_PLUGIN_ROOT}/skills/_drafting_common/SKILL.md`

## Case-type metadata

```yaml
case_type_line: PUBLIC INTEREST LITIGATION
case_short_code: PIL
hc_taxonomy_match: PIL / CRPIL (criminal PIL)
statutory_opening: |
  PUBLIC INTEREST LITIGATION UNDER ARTICLE 226 OF THE CONSTITUTION
  OF INDIA READ WITH RULES OF THE HON'BLE HIGH COURT OF JUDICATURE
  AT BOMBAY (NAGPUR BENCH)
accompanying_applications:
  - stay_application          # where interim relief sought
  - direction_application     # where mandamus-style direction sought during pendency
locus_standi_required: TRUE   # PIL maintainability requires bona fide public interest, not personal grievance
typical_annexure_order:
  - A: Documents establishing the public-interest fact pattern (RTI replies, news reports, official records)
  - B: Representations made to authorities (exhausted alternative remedy)
  - C: Replies received / inaction evidence
  - Subsequent: documentary support for grounds, expert reports, statistics
```

## Format reference

🟡 **Place case-type-specific format text in the file referenced below.**

`${CLAUDE_PLUGIN_ROOT}/skills/pil-draft/format-from-user.md`

## Hard rules

All rules from `_drafting_common/SKILL.md` apply. Additionally:
- ❌ NEVER draft a PIL without locus established. Halt if petitioner's interest looks private rather than public.
- ❌ NEVER draft a PIL where alternative remedy is available and unexhausted, unless the user confirms exception (constitutional violation, fundamental rights, etc.).
- ✅ Always include "Petitioner is filing this PIL bonafide and in public interest" with grounds for that bonafides in Facts.
