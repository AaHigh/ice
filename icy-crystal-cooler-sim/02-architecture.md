# 02 — Virtual System Architecture

The simulation is a closed software system that models the complete user experience, physics, pricing, and recursive improvement loop.

## High-Level Components

```
┌─────────────────────────────────────────────────────────────┐
│                     Simulation Runtime                       │
│                                                             │
│  ┌─────────────┐    ┌──────────────┐    ┌────────────────┐ │
│  │ Ambient     │    │ Drink        │    │ Living Prompt  │ │
│  │ Conditions  │───▶│ Instance     │───▶│ (per barcode)  │ │
│  └─────────────┘    └──────────────┘    └────────────────┘ │
│         │                   │                     │         │
│         ▼                   ▼                     ▼         │
│  ┌─────────────────────────────────────────────────────┐   │
│  │              Physics & Energy Model                  │   │
│  └─────────────────────────────────────────────────────┘   │
│         │                                                   │
│         ▼                                                   │
│  ┌─────────────┐    ┌──────────────┐    ┌────────────────┐ │
│  │ Risk Menu   │───▶│ Customer     │───▶│ Outcome        │ │
│  │ Generator   │    │ Choice       │    │ Recorder       │ │
│  └─────────────┘    └──────────────┘    └────────────────┘ │
│                                                   │         │
│                                                   ▼         │
│                                          ┌────────────────┐ │
│                                          │ Prompt Updater │ │
│                                          │ (RSI loop)     │ │
│                                          └────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

## Data Flow Summary

1. Ambient conditions and a Drink instance (barcode + starting temperature) are provided.
2. The current Living Prompt for that barcode is retrieved (or a default is created).
3. Physics model computes Q_min, expected energy, and feasible operating points conditioned on customer risk preference.
4. Risk Menu Generator produces 2–5 concrete options (time, energy, risk band, price).
5. Customer (or simulated agent) selects an option.
6. Process is simulated under the selected policy.
7. Outcome is recorded (success quality, actual energy, time, any failure).
8. Prompt Updater revises the living prompt with the new data.
9. Statistics and OR analyses can be run over many such cycles.

## Key Design Principles

- The Living Prompt is the sole repository of methodology for a given drink.
- All numerical estimates are derived from the physics model + current prompt parameters.
- Customer risk preference is an explicit input that conditions which operating points are offered.
- The simulation can run single interactive sessions or large Monte Carlo batches for operations research.
- No component hard-codes “the best” method; it only executes or updates what the current prompt contains.

## Extensibility Points

- New ambient variables (pressure, humidity) can be added to the physics model without changing the overall flow.
- New risk dimensions or preference axes can be added to the menu generator.
- Prompt update logic can itself be improved recursively.

This architecture is sufficient to implement the entire virtual system to completion.
