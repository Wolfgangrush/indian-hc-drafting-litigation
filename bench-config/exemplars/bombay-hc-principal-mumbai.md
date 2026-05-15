# bench-config — Bombay High Court, Principal Bench (Mumbai)

**Validation depth:** Researched · awaiting Registry validation.
**Source authorities:** Bombay High Court (Appellate Side) Rules 1960; Bombay High Court (Original Side) Rules; Principal Bench Practice Notes.

---

## Section 1 — Court identification

```yaml
high_court: "Bombay High Court"
bench: "Principal Bench (Mumbai)"
state: "Maharashtra"
court_header_line: |
  IN THE HIGH COURT OF JUDICATURE AT BOMBAY.
```

The Principal Bench is at Bombay; no "BENCH AT" qualifier needed.

## Section 2 — Procedural Rules

```yaml
appellate_side_rules: |
  Bombay High Court (Appellate Side) Rules, 1960
original_side_rules: |
  Bombay High Court (Original Side) Rules                       # Applicable for OS matters at Principal Bench
pil_rules: |
  Bombay High Court Public Interest Litigation Rules, 2010
```

## Section 3-12 — As per Bombay HC Nagpur exemplar

Most values mirror `bombay-hc-nagpur.md` except:

```yaml
counsel_place: "MUMBAI"                     # Different from "NAGPUR"
```

The Principal Bench also handles Original Side jurisdiction (commercial matters, admiralty, testamentary/intestate, etc.), which the Nagpur Bench does not. For Original Side matters, refer to Bombay HC (Original Side) Rules; cause title may differ slightly (e.g., "ON THE ORIGINAL SIDE" sub-line for OS suits).

For Appellate Side matters at the Principal Bench, the rest of the conventions are the same as Nagpur.

**Pull from `bombay-hc-nagpur.md` for full content; override only the values noted above.**
