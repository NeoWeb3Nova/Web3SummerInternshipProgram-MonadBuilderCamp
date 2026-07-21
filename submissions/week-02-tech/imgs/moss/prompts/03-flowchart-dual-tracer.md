---
illustration_id: 03
type: flowchart
style: blueprint
palette: graphite-cyan-red-yellow
---

Moss Dual Tracer Reconciliation — Process Flow

LAYOUT: symmetric top-to-bottom technical flowchart with two parallel tracer lanes that merge into one verification engine.

STEPS:
1. UNSIGNED TXS — a stack of transaction cards at top center.
2. Split into two equal lanes:
   - CALL TRACER — extracts CALL TREE, LOGS, MON VALUE.
   - PRESTATE TRACER — extracts STATE DIFF and feeds STATE OVERRIDES to the next transaction.
3. Both lanes merge into ACTUAL EFFECTS.
4. ACTUAL EFFECTS and DECLARED EXPECTS enter a large central reconciliation comparator.
5. MATCH flows in cyan to VERIFIED.
6. UNDECLARED DIFFERENCE flows in yellow then red to WARNING → HALT.

CONNECTIONS: thick directional arrows; a looping cyan arrow from STATE OVERRIDES back to the next UNSIGNED TXS to show multi-step simulation state inheritance.

LABELS: UNSIGNED TXS, CALL TRACER, CALL TREE, LOGS, MON VALUE, PRESTATE TRACER, STATE DIFF, STATE OVERRIDES, ACTUAL EFFECTS, DECLARED EXPECTS, MATCH, VERIFIED, UNDECLARED DIFFERENCE, WARNING, HALT. Spell exactly. No other visible text.

COLORS: graphite-black background; cyan for trace and verified paths; white for neutral nodes; yellow for detected difference; red for HALT. Color names are rendering guidance only—do not display palette labels.

STYLE: precise system-design blueprint, neon circuit traces with restrained glow, large readable labels, clean cards, no people, no logos, no fake terminal text, no clutter.

Clean composition with generous margins and strong visual hierarchy.

ASPECT: 16:9 landscape, medium-high complexity.
