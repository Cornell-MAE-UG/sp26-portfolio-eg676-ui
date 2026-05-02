---
layout: project
title: Nutcracker Design
description: Designed the optimal nutcracker based off publicly available data
image: /assets/images/nut-cracker.jpeg

---

<div style="clear:both;"></div>

As part of a class project, I designed a specialized lever-action nutcracker optimized specifically for the high forces required to crack macadamia nuts.

---
<div style="clear:both;"></div>


## Problem Statement & Objective

The goal of this project was to design a manual nutcracker that makes cracking a macadamia nut feasible for the average adult. Macadamia nuts are notoriously difficult to open, requiring significantly more force than common nuts. My objective was to determine the necessary handle length and mechanical advantage required to bridge the gap between human grip strength and the nut's failure point. Additionally, I explored an automated variant by selecting and integrating a linear actuator into the design to replace manual effort.

## Constraints and Input Parameters

To ensure the design was grounded in reality, I used the following parameters:

- **Average Load to Crack:** 222.18 lbf (approximately 225 lbf used for calculations)
- **Average Nut Size:** Approximately 15 mm
- **Human Grip Strength:** 30 lbf for females, 50 lbf for males
- **Design Target:** Minimum handle length required for a female with average grip strength (30 lbf)
- **Actuator Specs:** 12V DC Compact Micro Linear Actuator with a 25 lbf force capacity and 192 mm stroke

## Approach and Calculations

My approach utilized a **Class 2 Lever** model, where the pivot is at one end, the load (nut) is in the middle, and the effort (hand/actuator) is at the opposite end.

1. **Assumptions:** I assumed the nut is placed at a distance from the pivot to maximize leverage. I designed two internal "seats" for the nuts: a 12 mm space for average/large macadamias and an 8 mm space for smaller ones.
2. **Statics Analysis:** I performed a moment balance about the pivot ΣMₐ = 0 to find the required dimensions.
3. **Manual Design:** Using the formula {F}nut(24) = {F}handle(24 + x), I calculated that to crack a 225 lbf nut with 30 lbf of input force, the required additional handle length x is **164 mm**, providing a **7.5x force amplification**.
4. **Automation:** When redesigning for a linear actuator with a 25 lbf output, I recalculated the required length to be **192 mm** to accommodate the lower force capacity and the actuator's specific stroke.

## Design Diagram

<img src="{{ '/assets/images/finaldiagram.png' | relative_url }}" alt="Class 2 lever diagram" width="600">

The diagram above illustrates the manual design, highlighting the pivot point (A), the dual-sized crushing seats (8 mm and 12 mm), and the 164 mm handle extension.

## Usability

The final design prioritizes the average female grip strength as the baseline, ensuring most adults can crack a macadamia nut with minimal effort. The two distinct crushing zones prevent slipping — a common issue under high-force conditions — while the extended handle achieves a mechanical advantage that maximizes cracking power with minimal physical exertion.

---

## Beam Bending Analysis

The initial design treated the handles as rigid. In reality they are slender beams that deflect under the combined action of the nut reaction and the actuator force. The goal here is to (a) find the location of maximum elastic deflection, (b) size a cross-section that keeps the vertical deflection below 2% of the handle length while minimizing mass, and (c) present the final design.

### Assumptions

- Handle modeled as a **cantilever beam fixed at the pivot A** — the bracket region is much stiffer than the slender handle, so this is a reasonable upper-bound on bending.
- Only the **transverse** components of the forces are considered, per the problem statement.
- Forces treated as approximately perpendicular to the handle since the handle angle is small at the moment of cracking.
- Actuator force applied at the tip (x = L = 192 mm); nut reaction acts at x = 14 mm from the pivot (center of the 12 mm crushing seat, offset 8 mm from the pivot).
- Static loading, small deflections, linear-elastic Euler–Bernoulli beam theory.
- Material: 6061-T6 aluminum (justified below).

### Loading

By Newton's third law, when the nutcracker delivers the F_crush = 225 lbf ≈ 1000 N crushing force to the nut, the nut pushes back on the handle with the same 1000 N, applied at x = 14 mm. Moment balance about the pivot then sets the actuator force:

```
F_nut × 14 = F_act × 192
F_act = 1000 × (14 / 192) ≈ 73 N
```

So each handle sees a 1000 N upward load near the pivot and a 73 N downward load at the tip.

### (a) Location of maximum deflection

Using cantilever superposition with the pivot as the fixed end:

- Deflection from the tip load (downward, from F_act): δ₁(x) = F_act · x²(3L − x) / (6EI), monotonically increasing in x.
- Deflection from the interior load (upward, from F_nut at x = a): δ₂(x) = F_nut · a²(3x − a) / (6EI) for x ≥ a, also monotonically increasing in x.

Both contributions grow with x, and the actuator term dominates (the nut sits so close to the pivot that its long-distance bending influence is small). The **maximum elastic deflection therefore occurs at the tip, x = L**.

Net tip deflection:

```
δ_tip = F_act · L³ / (3EI) − F_nut · a² · (3L − a) / (6EI)
```

Plugging in numbers (SI units):

- Actuator term: 73 × (0.192)³ / 3 = 0.1722 N·m³
- Nut term: 1000 × (0.014)² × (0.562) / 6 = 0.0184 N·m³
- Net: δ_tip · EI = 0.1539 N·m³

### (b) Cross-section and material

**Deflection target**: δ_max ≤ 0.02 × L = 3.84 mm.

Required stiffness: EI ≥ 0.1539 / 0.00384 = **40.1 N·m²**.

**Material — 6061-T6 aluminum** (E = 69 GPa, ρ = 2700 kg/m³). For deflection-limited bending, the relevant material index is √E/ρ. Comparing options:

| Material   | E (GPa) | ρ (kg/m³) | √E / ρ (×10⁻³) |
|------------|---------|-----------|----------------|
| A36 steel  | 200     | 7850      | 1.80           |
| 6061-T6 Al | 69      | 2700      | 3.08           |
| Ti-6Al-4V  | 114     | 4430      | 2.41           |
| CFRP       | 70      | 1600      | 5.23           |

Aluminum nearly matches CFRP-class efficiency for stiffness-limited bending while remaining cheap, machinable, and well-suited to a hand tool.

Required second moment: I ≥ 40.1 / (69 × 10⁹) = 5.81 × 10⁻¹⁰ m⁴ = **581 mm⁴**.

**Cross-section — I-beam**, oriented with the web in the bending plane. For a given area, the I-beam places material as far as possible from the neutral axis, maximizing I/A. Selected dimensions (matching the 12 mm handle thickness from the original drawing):

- Height h = 12 mm
- Flange width b = 8 mm
- Flange thickness t_f = 1.5 mm
- Web thickness t_w = 1.5 mm

```
I = b·h³/12 − (b − t_w)(h − 2t_f)³/12
  = 8(12)³/12 − (6.5)(9)³/12
  = 1152 − 395 = 757 mm⁴
```

This exceeds the 581 mm⁴ requirement by ~30%, leaving margin for manufacturing tolerance.

Cross-sectional area:

```
A = 2(b · t_f) + (h − 2 t_f) · t_w = 2(8)(1.5) + (9)(1.5) = 37.5 mm²
```

Mass per handle:

```
m = ρ · A · L = 2700 × 37.5×10⁻⁶ × 0.192 = 19.4 g
```

### Verification

```
EI    = 69 × 10⁹ × 757 × 10⁻¹² = 52.2 N·m²
δ_tip = 0.1539 / 52.2          = 2.95 × 10⁻³ m = 2.95 mm
δ_tip / L                      = 1.54%   ✓  (below the 2% limit)
```

### (c) Final design

<img src="{{ '/assets/images/handle-beam-design.svg' | relative_url }}" alt="Handle beam model and I-beam cross-section" width="700">

### Summary

The handle is modeled as a cantilever beam fixed at the pivot, loaded by a 1000 N nut reaction at x = 14 mm and a 73 N actuator force at the tip. Although the actuator force is much smaller, its long moment arm makes it the dominant deflection driver — required EI = 40.1 N·m², or I ≥ 581 mm⁴.

A 6061-T6 aluminum I-beam with h = 12 mm, b = 8 mm, and 1.5 mm flanges/web provides I = 757 mm⁴ at 19.4 g per handle, with tip deflection of 2.95 mm (1.54% of L) — comfortably below the 2% target.
