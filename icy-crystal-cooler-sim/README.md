# Icy Crystal Cooler — Virtual System Design

**Project Intent**  
This is a pure software simulation of a coin-operated single-drink cooler whose sole qualitative goal is to deliver surface ice crystals that form and can be tasted on the first sip when the can is opened, without bulk freezing or explosion.

The system is deliberately constructed as an example of Recursive Self-Improvement (RSI) driven by emergence. Only the high-level goals and constraints are fixed. Everything about methodology for each drink lives inside evolving per-barcode prompts. Customer risk preference, ambient conditions, and measured starting temperature further condition those prompts. No physical hardware is required to complete the virtual system.

The simulation exists so that operations-research analysis, monetization mapping, risk surfaces, and pricing sensitivity can be fully explored before any physical prototype is considered.

## Document Map

| File | Purpose |
|------|---------|
| `01-goals-and-constraints.md` | Immutable goals, HRLF-style constraints, success criteria |
| `02-architecture.md` | Overall virtual system components and data flow |
| `03-data-models.md` | All core entities (Drink, Prompt, Ambient, Choice, Outcome, etc.) |
| `04-living-prompts.md` | Format, contents, and evolution rules for per-barcode prompts |
| `05-physics-model.md` | Thermodynamic calculations, approximations, energy floors |
| `06-user-experience-flow.md` | Complete simulated customer journey |
| `07-pricing-engine.md` | Transparent variable-cost pricing + fixed margin |
| `08-simulation-and-or.md` | Monte Carlo, sensitivity, monetization mapping, OR techniques |
| `09-implementation-guide.md` | Concrete guidance for building the simulator to completion |

## Core Philosophy

- Goals and constraints are fixed.
- Methodology is emergent and lives only inside living prompts.
- Customer agency (risk tolerance) is a first-class input.
- Pricing is physics-derived and educational.
- The simulation itself is the first instantiation of the recursive loop.
- Physical implementation, if ever pursued, simply replaces approximate models with real measurements and continues the same loop.

Start with `01-goals-and-constraints.md`.
