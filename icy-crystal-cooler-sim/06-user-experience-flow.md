# 06 — User Experience Flow (Virtual)

This is the complete simulated customer journey. Every step must be representable in software.

## 1. Insertion

Customer inserts the drink.  
System records barcode (or assigns a temporary ID) and measures / accepts starting temperature \( T_{start} \).

## 2. Context Gathering

- Load current AmbientConditions.
- Load or create the LivingPrompt for the barcode.
- Accept CustomerPreference (risk_tolerance). If none supplied, default to “balanced”.

## 3. Menu Generation

Physics model + current prompt + risk preference produce 2–5 OperatingPoints.  
Each option shows:

- Risk label
- Estimated time
- Estimated energy (Wh)
- Estimated probability of clean surface crystals
- Estimated probability of hard-freeze / explosion
- Calculated energy cost
- Fixed margin
- Final price

## 4. Choice

Customer (or simulated agent) selects one option.  
The exact prompt parameters that will be used are locked for this cycle.

## 5. Process Execution (Simulated)

The selected methodology is applied:

- Bath at the prompt’s set-point
- Spin profile executed
- Hold time
- Nucleation trigger

The simulation produces actual_time_s, actual_energy_wh, and a success / failure outcome according to the probabilistic models currently encoded in the prompt and physics layer.

## 6. Outcome & Feedback

- CycleOutcome is recorded.
- Living prompt is updated (version++, history appended, statistics refreshed, methodology revised if warranted).
- Customer is shown the result (success quality, actual energy, actual time, educational note about ambient effect if desired).

## 7. Loop Continuity

The next insertion of the same barcode uses the newly updated prompt.  
Over many cycles the methodology for that drink improves.

This flow is the complete user experience that the virtual system must implement. Interactive single-user mode and batch Monte Carlo mode both exercise the same path.
