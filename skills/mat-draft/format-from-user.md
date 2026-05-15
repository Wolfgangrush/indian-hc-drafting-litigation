# MAT Writ Petition — Format reference

🟡 **Place case-type-specific format text in this file.**

The user should paste their canonical MAT-WP master template into this file. The Drafter agent reads it as the authoritative source for statutory openings, prayer phrasing, counsel block layout, and other format-level conventions.

Until this file is filled, the Drafter falls back to the universal skeleton in `${CLAUDE_PLUGIN_ROOT}/skills/_hc_pleading_base/SKILL.md` plus the case-type metadata in `SKILL.md`. That fallback is sufficient for a first draft but the user should review carefully before filing.

## What this file should contain

1. The exact court header line as used in your chambers
2. The exact cause-title line wording (with `WRIT PETITION NO._______/<YEAR>` and the ACT-code line below)
3. The statutory opening clause (Article 226/227 + AT Act invocation)
4. The party-block format (Petitioner = aggrieved official; Respondents = State + Department + immediate superior + private respondents impleaded as necessary parties)
5. The salutation opener
6. The grounds opener and the closing grounds (limitation, alternative remedy disclaimer, rights-reserved)
7. The prayer opener and the catchall prayer
8. The counsel block exact layout
9. The Index table column ordering and headers
10. The Synopsis section ordering (Dates–Events → Points to be Considered → Acts & Rules → Citations)
11. The Stay Application format (as a standalone block with its own cause title + facts + prayer + counsel)
