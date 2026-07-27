# 01 — Goals and Constraints

These are the only fixed elements. Everything else is allowed to emerge.

## Primary Qualitative Goal

Deliver a drink that, when opened, forms visible and tasteable ice crystals at the surface on the first sip, without bulk freezing of the contents and without can/bottle explosion or rupture.

This is a controlled supercooling + on-demand nucleation target, not “make the drink cold.”

## Performance Goals (ordered)

1. Minimize time from start of cooling process to the ice-crystal-ready state.
2. Minimize electrical energy consumed per successful cycle.
3. Maximize probability of clean surface crystallization under the customer-chosen risk tolerance.

## Economic Goals

- Variable cost of cooling is calculated from real (or simulated) thermodynamic work.
- A fixed margin (constant dollars or constant percentage — to be chosen) is applied on top of the calculated energy cost.
- Final price is therefore transparent and educational: it moves with ambient temperature, starting temperature of the drink, and the chosen risk/time operating point.
- The system must support different liquids (water, sugary sodas, high-alcohol) under the same transparent model.

## Customer Agency Goals

- Customer inserts the drink first so actual starting temperature can be measured.
- Customer expresses risk tolerance (higher risk of hard-freeze/explosion in exchange for colder/faster/more certain crystallization, or lower risk in exchange for more conservative process).
- Customer sees a menu of options with estimated time, energy cost, risk level, and final price before committing.
- Customer thereby shoulders the risk and optimizes for their own preference and budget.

## HRLF-Style / Preference Constraints

- Safety first: uncontrolled hard freezes or explosions are failures.
- Transparency is mandatory: every cycle can display the calculated Q, measured/estimated energy, ambient effect, and resulting price.
- Preference for emergence: methodology lives only in living prompts; no permanent hardcoded control tables beyond what the current prompt directs.
- Local reality matters: ambient temperature distributions, electricity rates, and typical drink starting temperatures should reflect realistic operating environments (including hot climates).
- Education is a feature: the price and displayed numbers teach the customer about thermodynamic work under current conditions.

## Success Criteria for a Single Cycle

A cycle is considered successful when:

- Surface ice crystals form and are detectable/tasteable on first sip after opening.
- No bulk solid freeze of the majority of the liquid.
- No rupture, explosion, or dangerous pressure release.
- The process completed under the risk tolerance the customer selected.
- Energy and time were recorded for prompt update.

## Out of Scope (for the virtual system)

- Physical hardware design, materials, or fabrication.
- Payment hardware (coin, card, etc.) — only the economic model.
- Legal/regulatory classification of the device.
- Branding or physical industrial design.

These constraints remain fixed. All methodology, control parameters, and operating points are free to evolve inside the living prompts and the simulation loop.
