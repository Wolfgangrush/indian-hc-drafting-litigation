# Public Interest Litigation — Format reference

🟢 **Format = Civil WP format.** the user confirmed: PIL format is identical to Civil Writ Petition.

This file is a **pointer** to the canonical Civil WP format-from-user.md.

---

## Authoritative source

→ See: `${CLAUDE_PLUGIN_ROOT}/skills/civil-wp-draft/format-from-user.md`

Drafter agent for `pil-draft` should load that file as the format authority and apply it with the PIL-specific overrides below.

---

## PIL-specific overrides (delta from Civil WP)

These are the ONLY differences in language/structure:

### Cause title

```
WRIT PETITION (PIL) No.                 /<YEAR>
   OR
PUBLIC INTEREST LITIGATION No.                 /<YEAR>
   OR (HC Nagpur taxonomy match)
PIL No.                 /<YEAR>
```

ACT CODE matches PIL/CRPIL per HC taxonomy.

### Statutory opening

```
PUBLIC INTEREST LITIGATION UNDER ARTICLE 226 OF THE CONSTITUTION OF INDIA
READ WITH RULES OF THE HON'BLE HIGH COURT OF JUDICATURE AT BOMBAY (NAGPUR BENCH)
```

### Parties terminology

- **PETITIONER:** the public-interest applicant (individual, NGO, or association)
- **RESPONDENT:** State of Maharashtra + relevant authorities + any private respondents whose interest is in question

### Mandatory bona fides paragraph

In FACTS, immediately after parties block, PIL must include a paragraph establishing locus standi:

```
That the Petitioner is filing this Public Interest Litigation bonafide and in
public interest. <Petitioner's standing — e.g., "as a concerned citizen of India",
"as a registered NGO working in the field of <area>", "as a member of the affected
community having no personal interest in the litigation other than redressal of
the public wrong">. The Petitioner has no personal grievance and is moved solely
by the public interest at stake.
```

### Mandatory exhausted-remedy paragraph

PIL maintainability requires exhaustion of alternative remedies (or a constitutional violation justifying direct approach). Include:

```
That the Petitioner has previously approached <authority> via representation dated
<date> seeking redressal of the grievance. The copy of representation dated <date>
is annexed herewith as ANNEXURE-<X>. Despite the representation, no action has
been taken by the authority concerned. The Petitioner is therefore left with no
other equally effective remedy than to approach this Hon'ble Court.
```

### Standard PIL grounds patterns

- Public-interest substantiation (what wrong, whose harmed, why public)
- Statutory or constitutional violation by the respondent
- Failure of authorities to act despite representation
- Reference to Article 21 / 14 / 19 fundamental rights where applicable
- Distinguishing PIL from personal grievance

### Prayer

Standard Civil WP prayer pattern works. Common PIL-specific reliefs:

- Mandamus directing authority to act
- Declaration that respondent's action/inaction is unconstitutional/illegal
- Constitution of an inquiry / SIT
- Direction for compensation to affected class
- Stay of impugned policy / scheme
- Grant of any other relief in public interest (catchall)

### Annexure pattern

- A: The act/omission being challenged (policy / order / inaction evidence)
- B: Representations made to authorities (proving exhaustion)
- C: Replies received OR no-action evidence
- D onward: Documents establishing the public-interest fact pattern (RTI replies, news reports, official records, expert reports)

## Section order in final .docx

Same as Civil WP:
1. Main Petition
2. List of Annexures
3. Synopsis
4. Index

## NOTES FOR DRAFTER

- **Use Civil WP format-from-user.md as base. Apply PIL overrides above.**
- **Bona fides + exhausted remedy paragraphs are MANDATORY in PIL** — without them, maintainability is at risk.
- **NEVER draft a PIL without explicit the user confirmation that the Petitioner has standing** (locus). PIL maintainability is heavily scrutinised.
- **NEVER draft a PIL where alternative remedy is available and unexhausted** unless the user confirms an exception applies (constitutional violation / fundamental rights / class action).
- **Parties separator:** `///VERSUS///` (per Civil WP).
- **Court header:** same as Civil WP (no period at end).
- **All other formatting:** identical to Civil WP — refer to `civil-wp-draft/format-from-user.md`.
