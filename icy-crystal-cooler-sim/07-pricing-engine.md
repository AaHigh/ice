# 07 — Pricing Engine

Pricing is deliberately transparent and physics-derived.

## Variable Cost

\[
\text{Energy Cost} = E_{\text{wh}} \times \text{electricity_rate_per_kwh}
\]

\( E_{\text{wh}} \) comes from the physics model conditioned on the chosen operating point and current ambient.

## Fixed Margin

Two supported modes (chosen in SimulationConfig):

1. Absolute dollars — add a constant amount per cycle.
2. Percentage — multiply energy cost by (1 + margin_fraction).

The margin itself is a fixed policy; it does not change with ambient or drink. Only the energy cost moves.

## Final Price

\[
\text{Final Price} = \text{Energy Cost} + \text{Fixed Margin}
\]

(or the percentage equivalent)

If the machine also dispenses the liquid, the liquid cost is added as a separate transparent line item. Cooling physics and margin remain independent.

## Educational Display

Every menu option and every completed cycle should be able to show:

- Calculated \( Q_{\min} \)
- Assumed or measured COP
- Ancillary energy
- Effect of current ambient temperature on the result
- Why the price is higher or lower than on a cooler day

This satisfies the transparency and education goals.

## Implementation Requirements

- Pure function: inputs → price breakdown.
- No hidden fees.
- All intermediate values available for logging and OR analysis.
- Support for both interactive display and batch economic simulation.
