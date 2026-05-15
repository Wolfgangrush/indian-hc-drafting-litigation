# USAGE — `indian-hc-drafting`

End-user guide for any advocate who wants to use this plugin to draft High Court pleadings before any Indian High Court.

---

## 1. What you need before you start

| Requirement | Why |
|---|---|
| **A Claude-compatible runtime** | This plugin runs inside any Anthropic-compatible runtime that parses the standard SKILL.md plugin format |
| **An active Anthropic API account** | The plugin invokes the Anthropic API through your chosen runtime; usage is billed to your account |
| **Microsoft Word or LibreOffice** | To open and review the `.docx` output |
| **`pandoc`** (recommended) | `brew install pandoc` on Mac, `sudo apt install pandoc` on Linux |
| **Your case folder** | A directory containing the case documents |
| **Your bench-config** | One-time setup: copy `bench-config/bench-config-template.md` to your case folder, rename to `bench-config.md`, fill in your specific HC bench's values |
| **Your State's Court-Fees Act PDF** (where applicable) | For matters requiring State Court-Fees citation |

---

## 2. Install the plugin

```bash
git clone https://github.com/wolfgang-rush/indian-hc-drafting \
  <your-anthropic-plugins-folder>/indian-hc-drafting
```

Verify the plugin loads in your runtime according to your runtime's standard plugin-listing mechanism.

---

## 3. One-time setup — bench-config + style references

### 3a. Bench-config

The plugin ships with a template at `bench-config/bench-config-template.md`. This is THE most important one-time setup step for non-Bombay HC users.

```bash
# Copy template to your case folder
cp <plugin-folder>/bench-config/bench-config-template.md \
   <your-case-folder>/bench-config.md
```

Then open `bench-config.md` and fill in the values for your bench:
- **Court header line** (e.g., `IN THE HIGH COURT OF DELHI AT NEW DELHI.`)
- **Appellate-Side / Original-Side Rules** reference for your HC
- **Annexure-marker convention** (`ANNEXURE-A` / `EXHIBIT-A` / your bench's variant)
- **Paper size, font, spacing, margins** per your bench's Registry direction
- (Several other fields — see the template)

If you practise at Bombay HC Nagpur, the template's default values already match your bench. Minimal edits needed.

For other HCs, the template's default values are Bombay HC Nagpur — you'll need to replace each value with your bench's actual values. Pull from your bench's Practice Notes and Civil/Criminal Manual.

You only do bench-config setup ONCE per Anthropic installation, then save a master copy for re-use across cases. The plugin reads `bench-config.md` from each case folder at run-time.

### 3b. Style references

Each case-type skill has a `format-from-user.md` file under `skills/<case-type>-draft/`. These files request **your own preferred drafting style** for each section (Synopsis opener, Cause Title formatting, Grounds numbering, Prayer wording, Verification layout).

Open each file and paste your preferred style. The plugin uses these for connective-phrase alignment — it does NOT pull case-specific content from them.

You only do this once per Claude installation. Subsequent cases reuse your saved style.

```bash
cd <plugin-folder>/skills
$EDITOR pil-draft/format-from-user.md
$EDITOR civil-wp-draft/format-from-user.md
# ... and the remaining eleven case-type skills
```

If you skip this step, the Drafter will fail-stop on the first invocation and remind you.

---

## 4. Prepare your case folder

```
~/cases/<client-code-or-matter-name>/
├── CLAUDE.md                      # case context (case type, parties, key dates, advocate)
├── bench-config.md                # YOUR bench-config (filled in)
├── citations.md                   # YOUR confirmed list of case citations
├── laws/                          # PDFs of statutes not in training data
│   ├── HMA-1955.pdf
│   ├── MVA-1988.pdf
│   └── (etc.)
├── 01-impugned-order.pdf
├── 02-FIR.pdf                     # for criminal matters
├── 03-lower-court-pleadings.pdf
└── (other case-specific documents)
```

### What goes in `CLAUDE.md`

```markdown
# Case Context

## Case type
pil-draft                         # or civil-wp-draft / criminal-wp-draft / bail-draft / etc.

## Bench
Bombay High Court, Nagpur Bench   # or per your bench-config

## Parties
Petitioner: [Petitioner Name], [Age], [Occupation], R/o [Address]
Respondent: [Respondent Name]

## Impugned order
Date of order: <DD.MM.YYYY>
Court of origin: [Lower Court Designation]
Case number: [Case Type & Number]

## Limitation
Cause of action / date of impugned order: <DD.MM.YYYY>

## Advocate engaged
Name: [Advocate Name]
Bar Council enrolment number: [Enrolment No.]
```

### What goes in `citations.md`

Same shape as the sibling `supreme-court-drafting` plugin — `citations.md` is YOUR confirmed citation list. The Drafter never generates a citation from training memory; every citation in the output traces to this file.

---

## 5. Run the pipeline

Open your Claude-compatible session inside your case folder. Invoke the case-type skill:

```
draft pil
```

or:

```
/pil-draft
```

Other invocation phrases:

| Skill | Trigger phrases |
|---|---|
| `pil-draft` | "draft pil" · "draft public interest litigation" |
| `civil-wp-draft` | "draft civil wp" · "draft writ petition" |
| `criminal-wp-draft` | "draft criminal wp" · "draft criminal writ" |
| `criminal-appeal-draft` | "draft criminal appeal" · "appeal against conviction" |
| `application-482-draft` | "draft 482 application" · "draft 528 bnss application" · "inherent powers application" |
| `anticipatory-bail-draft` | "draft anticipatory bail" · "draft section 438 bail" · "draft section 482 bnss bail" |
| `bail-draft` | "draft bail application" · "draft regular bail" |
| `contempt-petition-draft` | "draft contempt petition" |
| `first-appeal-draft` | "draft first appeal" |
| `second-appeal-draft` | "draft second appeal" |
| `criminal-revision-draft` | "draft criminal revision" |
| `mact-draft` | "draft mact claim" · "draft motor accident claim" |
| `mat-draft` | "draft matrimonial petition" · "draft hma petition" |

The six-agent pipeline runs (Reader → Format → Drafter → Verifier → Refiner → Overseer) and produces:

```
case-folder/
├── case-facts.md
├── format-shell.md
├── draft-v1.md           draft-v1.docx
├── verification-report.md
├── draft-v2.md           draft-v2.docx
├── opposing-notes.md
└── final-draft.docx      ← OPEN THIS IN WORD
```

---

## 6. Review and finalise

Open `final-draft.docx` in Microsoft Word. Apply tracked-changes review.

Read carefully:
- **Cause Title** — Court header from your bench-config rendered correctly
- **Statement of Facts** — every paragraph matches your case folder
- **Annexure markers** — convention matches your bench-config
- **Verification** — your name, place, date filled in
- **Prayer** — relief sought is specific and tied to facts
- **Dual-citation pattern** (criminal cases) — every BNSS reference paired with CrPC

`opposing-notes.md` contains the Overseer's anticipation of preliminary objections — read this before filing.

You remain the responsible advocate. Sign only after full review.

---

## 7. Bench-specific notes

This plugin is designed to work across Indian HCs via bench-config. State-specific elements the plugin DOES NOT assume:
- Court header text (varies — Bombay vs Delhi vs Madras vs etc.)
- Appellate-Side / Original-Side Rules reference (each HC has its own)
- Annexure marker convention (varies by HC + Original Side vs Appellate Side)
- Paper size / font / margins (most converge on A4 + TNR + 14pt + 1.5 spacing, but verify)
- Pecuniary jurisdiction limits (set by each HC's notification)

Supply these via your `bench-config.md` per case folder, AND check your bench's Practice Notes before relying on the rendered output.

---

## 8. The plugin in one sentence

**This plugin converts your case folder into a High-Court-Registry-compliant `.docx` pleading at any Indian High Court — with bench-specific formatting from your supplied bench-config, every fact traceable to your case folder, every citation traceable to your confirmed list, and you remain the responsible advocate at every stage.**

---

## 9. Help and contact

- Bug reports / feature requests / bench-config contributions: open a GitHub Issue at https://github.com/wolfgang-rush/indian-hc-drafting/issues
- This project does not have an email contact channel and does not accept private legal-services inquiries.
- The plugin is released under the MIT licence — see `LICENSE`.
- For provenance and Bar Council Rule 36 compliance details, see `NOTICE.md`.

---

## 10. Quick troubleshooting

| Problem | Fix |
|---|---|
| Drafter halts with `STYLE.FAIL_STOP` | You haven't pasted style references into `format-from-user.md`. Open each file and paste your preferred style. |
| Output Court header is "Bombay HC Nagpur" but I practise at a different HC | Your case folder's `bench-config.md` is either missing or contains the default Bombay values. Copy the template, fill in your bench's values, save in the case folder. |
| Reader halts with `Need PDF` | You've referenced a statute (e.g., HMA, MVA) whose PDF is not in your case folder's `laws/` subfolder. Add the PDF. |
| Annexure markers come out as `ANNEXURE-A` but my HC uses different convention | Update `bench-config.md` Section 6 (annexure-prefix) to your bench's convention. |
| Many `[CITATION NEEDED]` placeholders in the output | The plugin won't generate citations from memory. Add the citations you intend to rely on to `citations.md`, then re-run; OR accept the placeholders and fill them manually post-draft. |
| `.docx` output looks unformatted | Pandoc may not be installed. Install: `brew install pandoc` (Mac) or `sudo apt install pandoc` (Linux). |
