# 03 — Data Models

All core entities required by the simulation.

## 1. AmbientConditions

```yaml
ambient:
  temperature_c: float          # outdoor / room temperature
  pressure_kpa: float           # atmospheric pressure (default 101.3)
  humidity_pct: float           # optional, for future refinement
  electricity_rate_per_kwh: float
  timestamp: datetime
```

## 2. Drink

```yaml
drink:
  barcode: string               # primary key
  name: string                  # human readable
  volume_ml: float
  density_g_per_ml: float       # default ~1.04 for cola-type
  mass_g: float                 # computed or measured
  specific_heat_j_per_g_c: float  # ~4.18 for water-based, lower for high alcohol/sugar
  estimated_freezing_point_c: float  # initial estimate; refined over time
  sugar_brix_approx: float      # optional helper for freezing-point depression
  alcohol_abv: float            # 0 for soda, higher for spirits
  category: string              # "soda", "water", "beer", "spirit", etc.
```

## 3. LivingPrompt

```yaml
prompt:
  barcode: string
  version: int
  last_updated: datetime
  methodology:
    target_temp_window_c: [float, float]   # e.g. [-2.5, -1.0]
    bath_setpoint_c: float
    spin_profile:
      rpm: int
      reversal_interval_s: float
      total_spin_time_s: float
    hold_time_s: float
    nucleation_method: string              # "open", "impact", "ultrasonic", "none"
    nucleation_delay_s: float
  performance_history:
    - cycle_id: string
      ambient_temp_c: float
      start_temp_c: float
      chosen_risk: string
      time_s: float
      energy_wh: float
      success: bool
      notes: string
  statistics:
    success_rate_by_risk: map
    mean_energy_wh: float
    mean_time_s: float
  notes: string                            # free-form evolution commentary
```

## 4. CustomerPreference

```yaml
preference:
  risk_tolerance: string        # "conservative" | "balanced" | "aggressive"
  # optional future axes: max_time_s, max_price, etc.
```

## 5. OperatingPoint (menu option)

```yaml
option:
  id: string
  risk_label: string
  estimated_time_s: float
  estimated_energy_wh: float
  estimated_success_prob: float
  estimated_hard_freeze_prob: float
  calculated_energy_cost: float
  fixed_margin: float
  final_price: float
  prompt_parameters_snapshot: map   # the exact settings that will be used
```

## 6. CycleOutcome

```yaml
outcome:
  cycle_id: string
  barcode: string
  ambient: AmbientConditions
  start_temp_c: float
  preference: CustomerPreference
  chosen_option: OperatingPoint
  actual_time_s: float
  actual_energy_wh: float
  success: bool                 # clean surface crystals, no bulk freeze, no explosion
  quality_score: float          # 0–1, how good the crystals were
  failure_mode: string | null   # "hard_freeze", "explosion", "no_crystals", etc.
  notes: string
```

## 7. SimulationConfig

```yaml
config:
  fixed_margin_type: string     # "absolute_dollars" | "percentage"
  fixed_margin_value: float
  default_electricity_rate: float
  max_menu_options: int         # typically 3–5
  monte_carlo_runs: int
  random_seed: int | null
```

These models are sufficient to implement persistence, the recursive loop, and all analyses.
