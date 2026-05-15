# `reference.docx` — Customisation Guide

The `reference.docx` is the **pandoc template** the Drafter agent uses when converting markdown drafts to `.docx`. Customise once per bench-config.

---

## Why customise

Each High Court's Registry rejects pleadings on minor formatting deviations. Pandoc's default `.docx` styles are office-document-generic. Customising `reference.docx` once aligns every future Drafter output with your specific HC bench's formatting.

---

## Typical HC formatting (varies by bench — verify against your bench-config)

| Element | Common specification |
|---|---|
| Paper size | A4 (most HCs); some Original Side practices use Legal |
| Print | One-side |
| Font (body) | Times New Roman, 14 point (most HCs) |
| Line spacing | 1.5 (most HCs) |
| Left margin (binding side) | 4 cm |
| Top / bottom / right margin | 2.5 cm |
| Section headers | Bombay HC convention: spaced (`F A C T S`); other HCs: Title Case bold |
| Page numbers | Centred at bottom |

Pull the exact values from your `bench-config.md` Section 9.

---

## How to customise (one-time, ~10 minutes)

1. **Generate a default reference.docx** if not already present:
   ```bash
   cd <plugin-folder>/skills/_hc_pleading_base
   pandoc --print-default-data-file reference.docx > reference.docx
   ```

2. **Open in Word or LibreOffice:**
   ```bash
   open reference.docx
   ```

3. **Set page size and margins** per your bench-config Section 9.

4. **Set body style** (Home / Styles / Normal):
   - Font: Times New Roman (or per bench-config)
   - Point size: 14 (or per bench-config)
   - Line spacing: 1.5 lines

5. **Set heading styles** (Heading 1, 2, 3) — bold, same point size as body.

6. **Add page numbers** (Insert / Page Number / Bottom centred).

7. **Save** (Cmd-S / Ctrl-S). Keep filename `reference.docx`.

---

## What NOT to customise

- No header / footer text content. The reference is a STYLE template only.
- Do not move the file or change the filename.
- Do not commit a `reference.docx` with case-specific content.

---

## How the Drafter uses it

```bash
pandoc draft-v1.md -o draft-v1.docx \
  --reference-doc="${CLAUDE_PLUGIN_ROOT}/skills/_hc_pleading_base/reference.docx"
```

Pandoc reads the styles from your customised `reference.docx` and applies them to every section of the draft.

---

## Bench-specific reference.docx (advanced)

If you practise at MULTIPLE benches with different formatting (e.g., you appear at Bombay HC Nagpur sometimes and Bombay HC Principal Bench other times — different paper size / different annexure style), you can maintain separate reference.docx files in your personal templates folder and point the Drafter at the right one via the case folder's `bench-config.md`. Future versions of the plugin will support per-case-folder reference.docx override.

---

## Fallback if pandoc is unavailable

The Drafter falls back to `python-docx` (which uses simpler default styles). Install pandoc for best results:

```bash
brew install pandoc       # macOS
sudo apt install pandoc   # Debian / Ubuntu
```
