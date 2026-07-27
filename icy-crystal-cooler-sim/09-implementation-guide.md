# 09 — Implementation Guide

This document is sufficient to take the virtual system to completion in software.

## Recommended Stack (example)

- Language: Python 3.11+
- Data: Pydantic or dataclasses for the models in `03-data-models.md`
- Persistence: JSON files or SQLite for prompts and cycle history (easy to inspect)
- Simulation: pure functions + a simple event loop or discrete-event style for batch runs
- Analysis: pandas + matplotlib/plotly for OR outputs
- Optional: FastAPI or Streamlit for an interactive front-end later

No external physics engines or heavy dependencies are required. The models are simple enough to implement directly.

## Implementation Order

1. Define all data classes / Pydantic models exactly as specified.
2. Implement the pure physics functions (`Q_min`, energy estimate, simple COP model).
3. Implement LivingPrompt load / save / update logic.
4. Implement menu generation (condition prompt on risk → produce OperatingPoints).
5. Implement the single-cycle flow (insertion → menu → choice → simulate outcome → update prompt).
6. Add a batch runner that samples ambient, start temps, preferences and records thousands of outcomes.
7. Add analysis scripts that produce the OR tables and monetization surfaces.
8. (Optional) Add a minimal interactive CLI or web UI that exercises the same flow.

## Bootstrap Data

- Create 5–10 example drinks (water, cola, diet cola, beer, high-ABV spirit) with reasonable defaults.
- Create a conservative default prompt template for each liquid class.
- Define a simple ambient temperature distribution (e.g., normal around 25 °C with a hot-climate tail).

## Testing the Recursive Loop

- Run the same barcode through many cycles with different ambients and risk preferences.
- Verify that the prompt version increments and that statistics and methodology parameters move in response to outcomes.
- Confirm that a drink that starts already cold produces a low energy cost and low price.

## Definition of Done for the Virtual System

- All nine design documents are reflected in working code.
- A single interactive cycle can be run end-to-end with full transparency output.
- A Monte Carlo batch of ≥ 1 000 cycles can be executed and produces usable OR statistics.
- Living prompts demonstrably evolve.
- Pricing remains strictly physics-derived + fixed margin.
- No physical hardware assumptions remain in the critical path.

Once the above is true, the virtual system is complete. Any later physical prototype simply replaces the approximate physics and outcome models with real sensors and measurements and continues the identical recursive loop.

## Final Note

The documents in this directory, taken together, constitute a complete specification. Implementation can proceed directly from them without further design invention.