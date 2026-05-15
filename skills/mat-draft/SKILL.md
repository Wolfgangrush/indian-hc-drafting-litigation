---
name: mat-draft
description: Draft a State Administrative Tribunal Original Application (e.g., Maharashtra Administrative Tribunal "MAT", Karnataka Administrative Tribunal "KAT", Gujarat Administrative Tribunal "GAT", etc., as established under the Administrative Tribunals Act 1985) or a Writ Petition before any Indian High Court challenging an Administrative Tribunal order (bench-specific values sourced from `<case-folder>/bench-config.md`). Most-validated configuration at v0.1.0-alpha is Bombay HC Nagpur + Maharashtra Administrative Tribunal. Produces a .docx with Main Petition + Index + Synopsis + List of Annexures, rendered in the user's bench's idiom. Auto-fires on "draft MAT OA", "draft administrative tribunal", "draft KAT OA", or similar State-tribunal trigger phrases.
allowed-tools: Read, Write, Edit, Bash, Glob
---

# MAT Draft Skill

Extends: `${CLAUDE_PLUGIN_ROOT}/skills/_hc_pleading_base/SKILL.md`
Common rules: `${CLAUDE_PLUGIN_ROOT}/skills/_drafting_common/SKILL.md`

## Case-type metadata

```yaml
case_type_line: WRIT PETITION   # when challenging a MAT order
case_short_code: MAT-WP
hc_taxonomy_match: WP
statutory_opening: |
  PETITION UNDER ARTICLE 226 / 227 OF THE CONSTITUTION OF INDIA
  CHALLENGING THE JUDGMENT AND ORDER PASSED BY THE LEARNED
  MAHARASHTRA ADMINISTRATIVE TRIBUNAL UNDER THE ADMINISTRATIVE
  TRIBUNALS ACT, 1985.
accompanying_applications:
  - stay_application        # often filed alongside
typical_annexure_order:
  - A: Certified copy of the impugned MAT Judgment and Order
  - B: Copy of the Original Application filed before MAT
  - C: Copy of the impugned departmental order (charge sheet / promotion / transfer / disciplinary order, as applicable)
  - D: Copy of the service-rule / GR / circular relied upon
  - E (Colly): Representations / departmental correspondence
  - F: Copy of the appointment order / service record summary
```

## When this skill fires

- Auto-trigger on phrases: "draft MAT OA", "draft MAT writ", "MAT WP", "administrative tribunal writ", "MAT challenge"
- The pipeline produces the standard 6-agent file chain

## Grounds structure (typical heads — to be populated from case facts)

A MAT-challenging WP typically argues one or more of:

1. **Jurisdictional error** — MAT exceeded jurisdiction conferred under S.14/15 of the Administrative Tribunals Act, 1985, or wrongly declined jurisdiction
2. **Error of law on the face of the record** — misinterpretation of service rules / GR / departmental circular
3. **Violation of principles of natural justice** before MAT (denial of oral hearing, denial of documents, denial of cross-examination)
4. **Perversity** — MAT's findings unsupported by evidence on record
5. **Failure to consider relevant material** / consideration of irrelevant material
6. **Wrong application of seniority / promotion / reservation / inter-se merit principles**
7. **Wrong application of disciplinary-inquiry standards** (proportionality of punishment; charge-sheet vagueness; presiding-officer bias)
8. **Limitation** — wrongly entertained beyond the period prescribed under S.21 AT Act / wrongly rejected on limitation
9. **Alternative-remedy disclaimer** — review under AT Act exhausted / Article 227 supervisory jurisdiction invoked

The Drafter agent draws the actual grounds from `case-facts.md`. Do not assume facts.

## Prayer template (typical)

```
a.  Quash and set aside the Judgment and Order dated <date>
    passed by the learned Maharashtra Administrative Tribunal,
    <Bench>, in O.A. No. ___/____;

b.  Allow the Original Application filed before MAT and grant
    [the consequential service benefits prayed for in O.A.];

c.  Direct the Respondents to [restore promotion / pay arrears /
    set aside the impugned departmental order / etc. — relief
    specific to facts];

d.  Stay the operation of the impugned Judgment and Order
    pending the hearing and final disposal of the present
    petition;

e.  Grant any other relief deems fit just and proper in the
    facts and circumstances of the case in favour of the
    Petitioner.
```

## Hard rules

All rules from `${CLAUDE_PLUGIN_ROOT}/skills/_drafting_common/SKILL.md` apply.

Additional MAT-specific rules:

- ❌ NEVER cite a service-jurisprudence precedent (e.g. L. Chandra Kumar, S.P. Sampath Kumar, Union of India v. R. Gandhi) without the user-supplied PDF in `<case-folder>/laws/`.
- ❌ NEVER assume the GR / circular / service rule contents from training data — the user MUST supply the rule PDF.
- ❌ NEVER assume the chronology of departmental representations / orders without case-folder support.
- ✅ The Synopsis Dates–Events table for MAT matters typically runs: date of appointment → date of impugned departmental action → date of representation → date of OA filing → date of MAT order → date of present petition.
- ✅ Always check whether the impugned departmental order itself can be challenged in a direct writ (some categories) — flag to the user if MAT route was unnecessary.

## Format reference

The exact statutory opening, prayer phrasing, and counsel block follow the format reference at `${CLAUDE_PLUGIN_ROOT}/skills/mat-draft/format-from-user.md` (user-supplied).
