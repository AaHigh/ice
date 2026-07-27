# 05 — Physics Model

All energy and time estimates derive from this model. Approximations are explicit so they can be improved later with real data.

## Core Quantities

- Mass \( m \) (g) = volume_ml × density_g_per_ml
- Specific heat \( c \) ≈ 4.18 J/g·°C for water-rich drinks; lower for high sugar or high alcohol (prompt or drink record may override)
- Starting temperature \( T_{start} \) (°C) — measured after insertion
- Target temperature \( T_{target} \) (°C) — taken from the living prompt’s window, conditioned on risk preference
- Ambient temperature \( T_{amb} \) (°C)

## Minimum Heat Removal (Sensible)

\[
Q_{\min} = m \cdot c \cdot (T_{start} - T_{target}) \quad \text{(Joules)}
\]

This is the thermodynamic floor for the liquid only. Can wall, imperfect contact, and system losses are additional.

## Real Electrical Energy

\[
E_{\text{elec}} = \frac{Q_{\min}}{\text{COP}_{\text{real}}} + E_{\text{ancillary}}
\]

- \(\text{COP}_{\text{real}}\) is a function of \( T_{amb} \) and evaporator temperature. A simple model is sufficient for the virtual system (e.g., linear or lookup decline as ambient rises). Later replaced by measured values.
- \( E_{\text{ancillary}} \) covers spinner motor, pumps, controls, nucleation assist (Wh).

Convert to Wh: \( E_{\text{wh}} = E_{\text{elec}} / 3600 \).

## Freezing-Point Depression (Initial Approximation)

For sugary drinks a simple estimate can be used at bootstrap:

\[
\Delta T_f \approx K_f \cdot m_{\text{solute}}
\]

where \( K_f \approx 1.86 \) °C·kg/mol for water. More accurate values are expected to emerge inside the living prompts from observed nucleation behavior.

## Time Estimation

Time is dominated by heat-transfer rate, not by \( Q_{\min} \) alone. The living prompt stores empirical or model-based time expectations for given spin profiles and bath set-points. The physics model may supply a simple convective heat-transfer estimate as a starting point; the prompt overrides it with observed data.

## Atmospheric Pressure & Other Variables

Atmospheric pressure has second-order effects on boiling/nucleation but is included in AmbientConditions so the model can later incorporate it. Humidity and other factors are reserved for future refinement.

## Implementation Note

All formulas must be implemented as pure functions that take Drink + Ambient + Prompt parameters and return Q_min, expected energy, and any intermediate values needed by the menu generator and pricing engine. No hidden state.
