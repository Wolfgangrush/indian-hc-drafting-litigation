# bench-config — Bombay High Court, Goa Bench

**Validation depth:** Researched · awaiting Registry validation.
**Source authorities:** Bombay High Court (Appellate Side) Rules 1960; Goa Bench Practice Notes; Goa Civil Manual.

---

## Section 1 — Court identification

```yaml
high_court: "Bombay High Court"
bench: "Goa Bench"
state: "Goa"
court_header_line: |
  IN THE HIGH COURT OF BOMBAY AT GOA.
```

Note the format differs slightly from the Nagpur / Aurangabad Benches — Goa uses `AT GOA`, not `BENCH AT GOA`.

## Section 3-12 — Mirror Bombay HC Nagpur exemplar with overrides

```yaml
counsel_place: "PANAJI"                    # Counsel block uses Panaji (the seat of the Goa Bench)
state: "Goa"                                # Different State for Court-Fees Act
state_court_fees_act_citation: |
  Schedule I, Article [N] of the Goa Court-Fees Act, 2002, as amended.
```

All other values per `bombay-hc-nagpur.md`.
