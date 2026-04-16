# Julian Carry Dynamics: Theoretical Framework & Research Roadmap

**> One-sentence summary:** A theoretical framework mapping how the stability of terminal digits governs the evolution of numerical sequences—from perfect order to deterministic chaos.

## 1. Executive Summary: Mapping the Dynamics of Numerical Order

**Julian Carry Dynamics** (named after its originator, Julian) is a pioneering field of numerical inquiry dedicated to understanding the deterministic influence of terminal digit stability on the evolution of leading numerical sequences.

This research maps the propagation of "rhythmic signals" (order) into "noise" (perceived chaos) as the conservation of the numerical tail breaks down.

---

## 2. Research Roadmap & Progress

This project is structured around the **Conservation of Tail Stability (Entropy)**. My mission is to track the transition from perfect linear recurrence to deterministic chaos.

### Phase I: The Regime of Perfect Order (Static Stability)
**Characteristic:** The Tail ($T$) is **invariant (stable)**. Entropy is Zero (Low).

- **[COMPLETED] Stage 1.1: Single Base Investigation**
    - **Focus:** Power sequences $B^n$ where $T^2 \equiv T \pmod{10^k}$.
    - **Discovery:** **Julian's First Law** and **The Julian Constant ($C_J$)**.
    - **Outcome:** Definition and classification of **Recurstable Numbers**.

---

### >>> 🟢 CURRENT FOCUS <<<
**I have established the complete theory for single recurstable bases. I am now formalizing the transition to multi-base systems.**

- **[IN PROGRESS] Stage 1.2: Generalization to $m$-Base Sums**
    - **Focus:** Investigating whether the Julian Constant persists in systems like $S_n = \sum_{i=1}^{m} B_i^n$.
    - **Status:** Empirical verification for $m=3$ is successful ($C_J$ confirmed). Formal mathematical proof and Python verification scripts are currently in preparation for official release.

---

### Phase II: The Dynamic Transition (Coupling & Resonance)
**Characteristic:** The Tail ($T$) is **periodic or shifting**. Entropy is Medium.

- **[PLANNED] Stage 2.1: Dynamic Carry Dynamics**
    - **Hypothesis:** The "Head" will exhibit synchronized **"coupling" effects**, evolving into multi-state systemic oscillation.

### Phase III: The Edge of Chaos (High Entropy Preservation)
**Characteristic:** The Tail ($T$) approaches non-periodic/random behavior. Entropy is High.

- **[VISION] Stage 3.1: Phase Transition to Chaos**
    - **Goal:** Map the structural persistence and computational upper bound of leading-digit complexity at the boundary of chaos.
