---
name: criminal-revision-draft
description: Draft a Criminal Revision Application before any Indian High Court (bench-specific values sourced from `<case-folder>/bench-config.md`) under Section 442 BNSS / Sections 397 + 401 CrPC. Used to challenge non-interlocutory orders of subordinate criminal courts. Most-validated bench at v0.1.0-alpha is Bombay HC Nagpur. Produces .docx with Main Application + Index + Synopsis + List of Annexures + (optional) Stay Application, rendered in the user's bench's idiom. Auto-fires on "draft revision" or "draft criminal revision" or "draft CRA".
allowed-tools: Read, Write, Edit, Bash, Glob
---

# Criminal Revision Application Draft Skill

Extends: `${CLAUDE_PLUGIN_ROOT}/skills/_hc_pleading_base/SKILL.md`
Common rules: `${CLAUDE_PLUGIN_ROOT}/skills/_drafting_common/SKILL.md`

This is the **11th case-type skill** added to the original 10 after the user provided a Criminal Revision Petition format.

## Case-type metadata

```yaml
case_type_line: Criminal Revision Application
case_short_code: CRA
hc_taxonomy_match: CRA / REVN
statutory_opening: |
  CRIMINAL REVISION APPLICATION UNDER SECTION 442 OF BHARATIYA NAGARIK SURAKSHA SANHITA, 2023.
  Note: the correct spelling is "BHARATIYA NAGARIK SURAKSHA SANHITA" (not "BHARTIYA NYAYA
  SANHITA" — that is a different statute, the BNS 2023 substantive penal code).
  S.442 BNSS = revisional jurisdiction, equivalent to S.397 / S.401 CrPC.
accompanying_applications:
  - stay_application          # where stay of trial proceedings sought
typical_annexure_order:
  - A: Copy of impugned order being challenged
  - B: Copy of related documents (chargesheet gist, depositions of relevant witnesses)
  - C-I: Subsequent documents establishing the chain of events leading to the impugned order
```

## Format reference

✅ **Encoded** at `${CLAUDE_PLUGIN_ROOT}/skills/criminal-revision-draft/format-from-user.md`

Master source: the user-supplied master Criminal Revision template (Drafts/ folder)

## Hard rules

All rules from `_drafting_common/SKILL.md` apply. Additionally:
- ❌ NEVER cite case law beyond what's verified (Bhajan Lal etc.) without user-supplied PDF.
- ✅ Revision is supervisory — grounds focus on jurisdictional errors, not factual reappreciation. Drafter should structure grounds accordingly.
