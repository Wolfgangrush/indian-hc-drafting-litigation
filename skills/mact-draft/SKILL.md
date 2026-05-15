---
name: mact-draft
description: Draft a Motor Accidents Claims Tribunal (MACT) claim petition or a Writ Petition before any Indian High Court challenging a MACT award (under the Motor Vehicles Act 1988; bench-specific values sourced from `<case-folder>/bench-config.md`). Most-validated bench at v0.1.0-alpha is Bombay HC Nagpur. Produces a .docx with Main Petition + Index + Synopsis + List of Annexures, rendered in the user's bench's idiom. Auto-fires on "draft MACT", "draft motor accident claim", or "draft MACT writ petition".
allowed-tools: Read, Write, Edit, Bash, Glob
---

# MACT Draft Skill

Extends: `${CLAUDE_PLUGIN_ROOT}/skills/_hc_pleading_base/SKILL.md`
Common rules: `${CLAUDE_PLUGIN_ROOT}/skills/_drafting_common/SKILL.md`

## Case-type metadata

```yaml
case_type_line: WRIT PETITION   # when challenging a MACT award; for original claim use the appropriate Claim Petition heading
case_short_code: MACT-WP
hc_taxonomy_match: WP
statutory_opening: |
  PETITION UNDER ARTICLE 226 / 227 OF THE CONSTITUTION OF INDIA
  CHALLENGING THE JUDGMENT AND AWARD PASSED BY THE LEARNED
  MOTOR ACCIDENT CLAIMS TRIBUNAL (MACT) UNDER THE MOTOR
  VEHICLES ACT, 1988.
accompanying_applications:
  - stay_application        # often filed alongside to stay recovery
typical_annexure_order:
  - A: Certified copy of the impugned MACT Judgment and Award
  - B: Copy of the FIR / accident report
  - C: Copy of the post-mortem report (where claim arises from death)
  - D: Copy of the medical records / disability certificate (where claim arises from injury)
  - E: Copy of the insurance policy / cover note
  - F (Colly): Witness depositions before MACT
  - G: Income / dependency proof (salary slips, ITRs, etc.)
```

## When this skill fires

- Auto-trigger on phrases: "draft MACT", "draft MACT writ", "MACT WP", "motor accident claim draft", "MACT award challenge"
- The pipeline produces the standard 6-agent file chain (Reader → Format → Drafter → Verifier → Refiner → Overseer)

## Grounds structure (typical heads — to be populated from case facts)

A MACT-challenging WP typically argues one or more of:

1. **Erroneous application of the multiplier method** (Sarla Verma v. DTC, Pranay Sethi)
2. **Wrongful application of the contributory-negligence reduction** (percentage attribution unsupported by evidence)
3. **Wrongful determination of dependency** (income, deductions, future prospects)
4. **Wrongful determination of just compensation** under heads of: loss of dependency, loss of consortium, loss of estate, conventional heads, funeral expenses, medical expenses, attendant charges, pain and suffering
5. **Insurer-liability exclusion wrongly upheld** (driving licence, fake licence, pay-and-recover)
6. **Interest rate inadequately awarded** or running-from-date wrongly fixed
7. **Limitation / delay** (where applicable — S.166(3) MV Act)

The Drafter agent draws the actual grounds from `case-facts.md` produced by Reader. Do not assume facts.

## Prayer template (typical)

```
a.  Quash and set aside the Judgment and Award dated <date>
    passed by the learned MACT, <place>, in MACP No. ___/____
    insofar as it [denies / reduces / wrongly determines] the
    compensation payable to the [Claimant/Appellant];

b.  Enhance the compensation awarded under all admissible heads
    in accordance with law;

c.  Direct that interest be payable at __% per annum from the
    date of filing of the claim petition till realisation;

d.  Stay the operation of the impugned Judgment and Award
    pending the hearing and final disposal of the present
    petition;

e.  Grant any other relief deems fit just and proper in the
    facts and circumstances of the case in favour of the
    Petitioner.
```

## Hard rules

All rules from `${CLAUDE_PLUGIN_ROOT}/skills/_drafting_common/SKILL.md` apply.

Additional MACT-specific rules:

- ❌ NEVER cite a multiplier table, dependency formula, or any quantum citation (Sarla Verma, Pranay Sethi, etc.) without the user-supplied PDF in `<case-folder>/laws/`. Reader STOPS if absent.
- ❌ NEVER assume the age of the deceased / claimant / dependents from anything other than documents in the case folder.
- ❌ NEVER assume the insurance position (admitted / contested / pay-and-recover) without explicit case-folder support.
- ✅ The Synopsis Dates–Events table for MACT matters typically runs: date of accident → date of FIR → date of charge sheet → date of filing claim petition → date of award → date of present petition.

## Format reference

The exact statutory opening, prayer phrasing, and counsel block follow the format reference at `${CLAUDE_PLUGIN_ROOT}/skills/mact-draft/format-from-user.md` (user-supplied).
