## Network Structure Diagram

```
┌────────────────┐      ┌─────────────────┐
│                │      │                 │
│  Pancreatic    │      │     Plasma      │
│  Insulin       ├─────►│     Insulin     │
│  Secretion     │      │                 │
│                │      └────────┬────────┘
└───────┬────────┘               │
        │                        │
        │                        ▼
        │               ┌─────────────────┐
        │               │                 │
        │               │   Interstitial  │
        │               │     Insulin     │
        │               │                 │
        │               └────────┬────────┘
        │                        │
        │                        │
┌───────▼────────┐      ┌────────▼────────┐
│                │      │                 │
│                │◄─────┤   Delayed       │
│    Plasma      │      │   Insulin       │
│    Glucose     │      │   Action        │
│                │      │                 │
└────────────────┘      └─────────────────┘
```

## System of Equations

Based on the Sturis model (1991), the system of differential equations is:

1. Glucose dynamics:
    
    $dG/dt = G_in - f₂(G) - f₃(G)f₄(I_d) + f₁(I_d)$
    
2. Plasma insulin dynamics:

    $dI_p/dt = f₅(G) - E(I_p - I_i)/V_p$

    
3. Interstitial insulin dynamics:
    
    $dI_i/dt = E(I_p - I_i)/V_i - f₆(I_i)$
    

4-6. Delay chain for insulin action (three compartments):

$dI_1/dt = (I_i - I_1)/τ₁$
$dI_2/dt = (I_1 - I_2)/τ₂$
$dI_3/dt = (I_2 - I_3)/τ₃$

Where:

- G is plasma glucose concentration (mg/dl)
- I_p is plasma insulin concentration (μU/ml)
- I_i is interstitial insulin concentration
- I_1, I_2, I_3 represent delayed insulin action
- G_in is glucose input rate (mg/min)
- E is exchange rate between plasma and interstitial insulin
- V_p and V_i are distribution volumes
- τ₁, τ₂, τ₃ are time constants for the delay chain

The nonlinear functions f₁ through f₆ represent:

- f₁: insulin-dependent glucose production by liver
- f₂: insulin-independent glucose utilization
- f₃, f₄: insulin-dependent glucose utilization
- f₅: glucose-stimulated insulin production
- f₆: insulin degradation

## Levels of Complexity

### 1D Model

The simplest 1D model would focus solely on glucose concentration with insulin treated as a parameter:

$dG/dt = G_{in} - k₁G - k₂GI + k₃$

Where I is treated as a fixed parameter, and k₁, k₂, and k₃ are constants.
G_in -- rate of glucose 

Sturis Paper:
- k₁ ≈ 0.01 min⁻¹
    
- k₂ ≈ 0.0001 ml/μU·min
    
- k₃ ≈ 1.0 mg/min

**Note: generate oscillations but provides a starting point for understanding basic glucose regulation.**



Personal Notes:

### Different Physiological Situations

### Baseline Parameters (Healthy Individual, Fasting State)

- **G_in**: 1.8 mg/dL/min (baseline glucose input rate)
- **k₁**: 0.015 min⁻¹ (insulin-independent glucose utilization)
- **k₂**: 0.0002 mL/μU/min (insulin-dependent glucose utilization)
- **k₃**: 1.0 mg/dL/min (basal hepatic glucose production)
- **I**: 12 μU/mL (fixed insulin concentration)
- **G(0)**: 90 mg/dL (initial glucose concentration)
- 
1. **Fasting State (Baseline)**
    - Parameters as above
    - Equilibrium glucose level: ~87 mg/dL
    - No significant changes in glucose level over time
2. **After Meal Consumption**
    - **G_in**: Increases to 5.0 mg/dL/min
    - Other parameters unchanged
    - Result: Glucose rises initially, then gradually returns to baseline
    - Equilibrium would shift temporarily, then return to normal
3. **Moderate Insulin Resistance**
    - **k₂**: Reduced to 0.0001 mL/μU/min (reduced insulin sensitivity)
    - Other parameters unchanged
    - Result: Higher equilibrium glucose level (~97 mg/dL)
    - Rate of glucose clearance after meals would be slower
4. **Severe Insulin Resistance**
    - **k₂**: Further reduced to 0.00005 mL/μU/min
    - **k₃**: Increased to 1.3 mg/dL/min (increased hepatic glucose output)
    - Result: Significantly elevated glucose (~120 mg/dL)
    - Very slow return to baseline after meals
5. **Type 1 Diabetes (Insulin Deficiency)**
    - **I**: Reduced to 3 μU/mL (low insulin level)
    - Other parameters unchanged
    - Result: Severely elevated glucose (~147 mg/dL)
    - Minimal ability to clear glucose after meals
6. **During Exercise**
    - **k₁**: Increased to 0.025 min⁻¹ (increased insulin-independent glucose uptake)
    - **k₂**: Increased to 0.0003 mL/μU/min (enhanced insulin sensitivity)
    - Result: Lower equilibrium glucose (~72 mg/dL)
    - Faster glucose clearance
7. **Continuous Feeding (IV Glucose)**
    - **G_in**: Constant elevated value of 3.5 mg/dL/min
    - Other parameters unchanged
    - Result: New higher equilibrium glucose (~117 mg/dL)

To find the equilibrium glucose concentration for each scenario, set dG/dt = 0 and solve for G:


$0 = G_{in} - k₁G - k₂GI + k₃$
$G = (G_{in} + k₃)/(k₁ + k₂I)$
