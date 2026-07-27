# 08 — Simulation Runtime & Operations Research

The virtual system must support both interactive single-cycle sessions and large-scale batch analysis.

## Interactive Mode

- User (or test harness) supplies drink + starting temperature + risk preference.
- Full flow from insertion to outcome executes once.
- Prompt is updated.
- Full transparency data is returned.

## Batch / Monte Carlo Mode

- Sample ambient temperature distributions (realistic for target climate).
- Sample starting temperatures of drinks.
- Sample barcodes / liquid classes.
- Sample customer risk preferences (or fix them).
- Run thousands of cycles.
- Collect statistics on:
  - Success rates by risk band and ambient
  - Energy and time distributions
  - Price distributions
  - Margin stability
  - Utilization under different arrival patterns

## Operations Research Capabilities

The simulation must make it possible to answer, before any hardware is built:

- How does fixed margin size affect total revenue and customer acceptance under realistic weather?
- Which risk bands are most profitable / most used?
- How sensitive is energy cost to ambient temperature extremes?
- What is the value of better COP or better heat transfer (i.e., where should physical improvement effort go later)?
- What is the break-even utilization rate under different electricity prices?
- How does the educational transparency affect simulated willingness-to-pay? (can be modeled as a simple function of displayed information)

## Required Outputs for OR

- Full cycle logs (every CycleOutcome)
- Aggregated statistics by barcode, risk, ambient bin
- Sensitivity tables
- Monetization surface (price vs. volume vs. margin vs. ambient)

All of the above must be producible from the data models and physics/pricing engines already defined. No additional conceptual machinery is required.
