---
layout: project
title: Nutcracker Design
description: Designed the optimal nutcracker based off publicly available data
image: /assets/images/nut-cracker.jpeg

---

As part of a class project, I designed a specialized lever-action nutcracker optimized specifically for the high forces required to crack macadamia nuts.

---

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

<img src="{{ site.baseurl }}/assets/images/diagram.png" alt="Class 2 lever diagram" width="600">

The diagram above illustrates the manual design, highlighting the pivot point (A), the dual-sized crushing seats (8 mm and 12 mm), and the 164 mm handle extension.

## Usability

The final design prioritizes the average female grip strength as the baseline, ensuring most adults can crack a macadamia nut with minimal effort. The two distinct crushing zones prevent slipping — a common issue under high-force conditions — while the extended handle achieves a mechanical advantage that maximizes cracking power with minimal physical exertion.