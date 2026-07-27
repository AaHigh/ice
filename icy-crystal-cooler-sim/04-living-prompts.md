# 04 — Living Prompts

The living prompt is the only place methodology lives for a given barcode.

## Purpose

Each barcode (or liquid class) owns one evolving prompt. The prompt contains the current best known way to take that liquid to the ice-crystal-on-open state under different risk preferences and ambient conditions. After every cycle the prompt is updated with real (or simulated) outcome data.

## Required Contents

- Target temperature window for clean surface nucleation
- Bath temperature set-point
- Spin profile (RPM, reversal schedule, duration)
- Hold / equilibration time
- Nucleation method and timing
- Expected energy and time under reference conditions
- History of past cycles and observed failure modes
- Free-form notes explaining recent changes

## Evolution Rules

1. A cycle completes and produces a CycleOutcome.
2. The Prompt Updater appends the outcome to performance_history.
3. Statistics (success rate by risk band, mean energy, mean time) are recomputed.
4. If the outcome reveals a better operating region or a previously unknown failure mode, the methodology section is revised.
5. Version number is incremented and last_updated is set.
6. The new prompt becomes the source of truth for the next cycle of that barcode.

## Conditioning on Customer Risk

When generating a menu, the current prompt is conditioned on the customer’s risk_tolerance:

- conservative → safer (warmer) side of the target window, longer hold, lower spin aggression
- balanced → current best median parameters
- aggressive → colder side of the window, faster spin, higher nucleation confidence, accepting elevated hard-freeze probability

The prompt may store separate parameter sets per risk band or a continuous parameterization; either is acceptable as long as the menu generator can produce coherent options.

## Default / Bootstrap Prompt

When a barcode is seen for the first time, a conservative default prompt is created from generic liquid-class knowledge (soda, water, spirit, etc.). Subsequent cycles refine it.

## Transparency Requirement

Any prompt version can be inspected. The simulation should be able to show the current methodology text and the history that produced it. This supports the educational and auditability goals.

The living prompt mechanism is the concrete realization of emergence inside the system.
