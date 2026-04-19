# Julian Carry Dynamics: The Theory of Recurstable Numbers
### A Study on How Terminal Stability Determines Leading Behavior in Power Sequences

**Author:** Julian Wong  
**Current Grade:** Grade 3 (Age 9)  
**Primary Documenter:** Dong Cang  
**Research Date:** April 2026  
**Location:** Mississauga, Ontario, Canada  
**Version:** 1.0 (Phase I — Foundational)    
**Keywords:** Number Theory, Power Sequences, Linear Recurrence, Stable-Tail Integers

---

## Foreword 
>This article began with a conversation with my 9-year-old son, Julian. One afternoon, he was excited to share his "super cool secret" about what he noticed with the powers of 5 and how the front of the numbers followed a "hidden rule."
>
>To protect his discovery and provide a solid foundation should he choose to pursue this research in the future, 
>I have translated his spoken reasoning into formal written language and applied for a DOI.

---

## Abstract
This repository contains the my core research for **Julian Carry Dynamics**, which shifts the focus from inter-numerical relationships to the internal dynamics of a single value, exploring how digit carry-over effects move within its own structure.
The study defines **Recurstable Numbers**, and establishes **Julian's First Law**  — including the deterministic constant ($C_J$) that governs the leading digits of power sequences.
As the first paper in the Julian Carry Dynamics series, it lays the groundwork for future research that will map the transition from linear recurrence to deterministic chaos — revealing how numerical structure persists even at the edge of chaos.

---

## 1. What did I find?

1. For any integer exponent $n \ge 2$, the value of $5^n$ will always end in the digits **25**.
2. The hundreds digit always flips between $1$ and $6$ .
3. Let $A_n$ be the **leading digits** of $5^n$ (the number formed by removing the last two digits, $25$). 

The relationship between the current leading digits ($A_n$) and the previous leading digits ($A_{n-1}$) is defined by the formula:
$$A_n = 5A_{n-1} + 1$$

---

## 2. How did I find it? 

When you multiply the end part **25** by **5**, you get **125**. Because **$4  \times25$ = $100$**, every time you multiply by 5, it will go over 100. So:
- The **$25$** stays at the end.
- The **$1$** always **"carry over"** to the next place (the hundreds place).

That’s why you take the previous leading part, multiply it by 5, and then **always add 1**! 

This also explains the **1-6 Flip-Flop**:
- If the front ends in **1**: $1 \times 5 + 1 = \mathbf{6}$
- If the front ends in **6**: $6 \times 5 + 1 = 3\mathbf{1}$ (it goes back to 1!)

---

## 3. Let's see it in action:

| Power ($5^n$) | Result | leading Part ($A_n$) | Calculation ($5 \cdot A_{n-1} + 1$) | **Hundreds-Digit Pattern** |
| :--- | :--- |:---------------------| :--- |:---------------------------|
| $5^2$ | 25 | 0                    | (Base Case) | -                          |
| $5^3$ | 125 | **1**                | $5(0) + 1 = 1$ | **1**                      |
| $5^4$ | 625 | **6**                | $5(1) + 1 = 6$ | **6**                      |
| $5^5$ | 3125 | 3**1**               | $5(6) + 1 = 31$ | **1**                      |
| $5^6$ | 15625 | 15**6**              | $5(31) + 1 = 156$ | **6**                      |


---

## 4. The "Quinponent" Verification
* I originally named my first discovery the **"Quinponent"** pattern—a portmanteau of **Quin** (five) and **Ex-ponent**. 
* I wrote this script specifically to verify the leading digits for powers of 5.

```python
def verify_quinponent(n):
    front = 0  # Starting with 5^2
    for i in range(2, n + 1):
        result = 5**i
        print(f"5^{i} = {result} | Leading part is {front}")
        front = front * 5 + 1

if __name__ == "__main__":
    verify_quinponent(10)
```

## 5. Are there any similar numbers?
Through computer testing, I was able to identify a class of numbers that follow the same recursive patterns as base 5.

| Tail Length ($k$) | Base ($B$) | Stable Tail ($T$) | Constant ($C$) | Recursive Formula          |
|:------------------|:-----------|:------------------|:---------------|:---------------------------|
| **1**             | 6          | 6                 | **3**          | $A_n = 6(A_{n-1}) + 3$     |
| **1**             | 36         | 6                 | **21**         | $A_n = 36(A_{n-1}) + 21$   |
| **1**             | 11         | 1                 | **1**          | $A_n = 11(A_{n-1}) + 1$    |
| **2**             | **5**      | **25**            | **1**          | $A_n = 5(A_{n-1}) + 1$     |
| **2**             | 26         | 76                | **19**         | $A_n = 26(A_{n-1}) + 19$   |
| **2**             | 45         | 25                | **11**         | $A_n = 45(A_{n-1}) + 11$   |
| **2**             | 76         | 76                | **57**         | $A_n = 76(A_{n-1}) + 57$   |
| **3**             | 25         | 625               | **15**         | $A_n = 25(A_{n-1}) + 15$   |
| **3**             | 376        | 376               | **141**        | $A_n = 376(A_{n-1}) + 141$ |
| **3**             | 425        | 625               | **265**        | $A_n = 425(A_{n-1}) + 265$ |

---

## 6. Julian's First Law of Recurstable Numbers
### 6.1 Theorem Statement:
For any base $B$ where the power $B^n$ results in a **Stable Tail ($T$)** of length $k$, the **Leading Part ($A_n$)** of the sequence can always be expressed as a linear recurrence:

$$A_n = B \cdot A_{n-1} + C_J $$

**Variable Definitions**
* **$A_n$**: The "Leading Part" of the number, calculated as the integer value remaining after removing the last $k$ digits (the stable tail).
* **$B$**: The base of the power being calculated.
* **$n$**: The exponent ($n \ge 2$).
* **$T$ :** The recurring ending value of $B^n$.
* **$k$ :** The number of digits in $T$.
* **$C_J$ (The Julian Constant)**: A fixed integer derived from the interaction between the base and the stable tail. 

**The Julian Constant Formula:**
Julian's logic dictates that the constant $C_J$ is determined by the "carry-over" from the tail's multiplication:
$$C_J = \frac{B \cdot T - T}{10^k}$$

### 6.2 Computational Verification
I wrote the following Python script to test Julian's First Law.

```python
def verify_julian_first_law(B, k, max_n):
    # Calculate the Stable Tail (T)
    T = (B ** 2) % (10 ** k)
    # Calculate the Julian Constant (C_J)
    C_J = (B * T - T) // (10 ** k)

    # Starting Leading Part (A_2)
    A = (B ** 2) // (10 ** k)

    for n in range(3, max_n+1):

        # Applying Julian's First Law: A_n = B * A_{n-1} + C_J
        predict_A = B * A + C_J

        # Calculating actual value for validation
        actual_A = (B ** n) // (10 ** k)

        # Iterating: The current prediction becomes the base for the next power
        A = predict_A

        # Verify if the Law holds true
        print(f"n={n}: {predict_A == actual_A}")



if __name__ == "__main__":
    verify_julian_first_law(B=5, k=2, max_n=10)
```

---

### 6.3 Mathematical Proof
This is my original handwritten manuscript, providing the  initial proof of Julian’s First Law and the calculation of the Julian Constant ($C_J$).

![Manuscript-01: Algebraic Derivation of CJ and First Law](https://github.com/JulianWong310/Julian-Carry-Dynamics/blob/main/2026-04-15-julian-carry-dynamics/asset/01_algebraic_derivation.png)
*Caption: Original handwritten proof of Julian's First Law and The Julian Constant*

#### Step 1: Specific Observation (The Case of 5)

1. $5^2 = A_2 \cdot 100 + 25$
2. $5^3 = A_3 \cdot 100 + 25$
3. $\vdots$ (pattern continues...)
4. $5^{n-1} = A_{n-1} \cdot 100 + 25$
5. $5^n = A_n \cdot 100 + 25$

---

#### Step 2: Proving the Quinponent Pattern 
To find the relationship between $A_n$ and $A_{n-1}$, I used the fact that $5^n = 5^{n-1} \cdot 5$:

$$A_n \cdot 100 + 25 = (A_{n-1} \cdot 100 + 25) \cdot 5$$
$$A_n \cdot 100 + 25 = A_{n-1} \cdot 500 + 125$$
$$A_n \cdot 100 + 25 = A_{n-1} \cdot 500 + 100+25$$
$$A_n \cdot 100 + 25 = 100(A_{n-1} \cdot 5 + 1) + 25$$

By canceling the $25$ and dividing by $100$:
$$A_n = A_{n-1} \cdot 5 + 1$$

---

#### Step 3: Deriving the General Law
For any base $B$ with a stable tail $T$ of length $k$:

1. $B^n = 10^k \cdot A_n + T$
2. $B^{n-1} = 10^k \cdot A_{n-1} + T$

From (2), multiply by $B$:

$$B^n = 10^k \cdot B \cdot A_{n-1} + T \cdot B$$

Now, set the two expressions for $B^n$ equal:

$$10^k \cdot A_n + T = 10^k \cdot B \cdot A_{n-1} + T \cdot B$$

$$10^k \cdot A_n = 10^k \cdot B \cdot A_{n-1} + (T \cdot B - T)$$

Divide by $10^k$ to isolate $A_n$:

$$A_n = B \cdot A_{n-1} + \frac{T \cdot B - T}{10^k}$$

---

### Step 4: Final Conclusion (The Core Discovery)

#### 1. **The Julian Constant:**  

   $$C_J= \frac{T \cdot B - T}{10^k}$$ 

#### 2.  **The Julian's First Law Equation:**

   $$A_n = B \cdot A_{n-1} + C_J$$

Q.E.D

---

### 6.4 Explanation: The Geometry of Interference

Mathematically, without the carry‑over effect from the tail,one might expect the Leading Part ($A_n$) to grow purely as a power function ($B^n$). However, the Stable Tail ($T$) creates a persistent “interference”—the Julian Constant ($C_J$).

Picture a perfectly calm lake as a metaphor for the growth of a number. Multiplying by the base would produce a smooth, predictable wave across the surface. However, at each step, the stable tail acts like a small stone dropped into the water, making ripples that nudge the Leading Part away from its original path.

The beauty of Julian’s First Law lies in the realization that this shift isn't random; it is a deterministic offset. By pinpointing the Julian Constant, I have precisely mapped the “ripple effect” produced by the tail, demonstrating that what appears to be a deviation is, in fact, a perfectly regular and rhythmic law.

---

## 7. Julian's First Law Corollaries

### I. The Stability Requirement
According to the calculation of the Julian Constant, 
this linear recurrence exists only because the Tail (T) stays constant (stable).
If the tail were unstable, the constant ($C_J$) would become a variable, 
causing the linear structure of the Leading Part to collapse.

### II. The Integrality Guarantee
For the Linear Recurrence $A_n = B \cdot A_{n-1} + C_J$ to hold, the **Julian Constant ($C_J$)** must be an integer. We can verify this for all stable-tail bases ending in $T_1 \in \{0, 1, 5, 6\}$:

* **For 0 and 1:** The product $T_1(B-1)$ is always $0$, which is naturally divisible by $10$.
* **For 5:** Since the base $B$ ends in $5$, $(B-1)$ must be an even number. Any even number multiplied by $5$ results in a multiple of $10$.
* **For 6:** Since the base $B$ ends in $6$, $(B-1)$ must end in $5$. The product $6 \times 5 = 30$, which is also a multiple of $10$.
* **Note:** The verification above uses the case $k = 1$ (i.e., the last digit).
For k > 1, if $C_J$  is an integer then $10^k$ divides $T × (B−1)$, which implies $10$ also divides $T × (B−1)$. Hence the last‑digit condition must still hold. 

**Conclusion** — that $B$ must end in $0$, $1$, $5$, or $6$ — applies for any tail length $k$.

---

## 8. Definition & Properties of Recurstable Numbers

> *"A Recurstable Number is defined through the nature of its structure: the absolute stillness of its Tail and the consistent logic of its Head."*

### 8.1 Etymology 
The term **"Recurstable"** is an original portmanteau created by me, synergizing **Recurrence** (the deterministic evolution of terms) and **Stable** (the invariance of terminal digits).

I illustrated a knowledge map, visualizing where I applied my original ‘Recurstable Number’ within the landscape of Number Theory.

![Manuscript-02: Knowledge Tree of Recurstable Numbers](https://github.com/JulianWong310/Julian-Carry-Dynamics/blob/main/2026-04-15-julian-carry-dynamics/asset/02_knowledge_tree.png)
*Caption: Julian’s original knowledge map of Recurstable Numbers*


### 8.2 Definition
A **Recurstable Number** is a positive integer $B$ such that its power sequence $B^n$ (for $n \ge 2$) maintains an **invariant suffix** (a stable tail $T$) of length $k$. 


### 8.3 Core Properties
1. The Leading Part of a Recurstable Number follows $A_n = B \cdot A_{n-1} + C_J$.

2. A positive integer $B$ is a Recurstable Number **if and only if** its terminal digit $B \pmod{10} \in \{0, 1, 5, 6\}$. 

**Mathematical Intuition:**

* **Necessity (The DNA Test):** For a tail to be stable, the last digit must satisfy $T2≡T1(mod10)$. Testing all single digits confirms that only $0, 1, 5, 6$ possess this natural stability.
* **Sufficiency (The Julian Link):** As established in **Corollary II**, these four digits are the only ones that guarantee the **Julian Constant ($C_J$)** is an integer. 

---

## 9. Future Work: Julian Carry Dynamics
Julian Carry Dynamics is my approach to observing how the leading digits of a number evolve as the tail (the ending digits) becomes more complex.

I defined a research roadmap to guide my exploration and divided it into three phases, each corresponding to increasing levels of tail complexity.

![Manuscript-03:Research Roadmap of Julian Carry Dynamics](https://github.com/JulianWong310/Julian-Carry-Dynamics/blob/main/2026-04-15-julian-carry-dynamics/asset/03_research_roadmap.png)
*Caption: Three-phase research roadmap of Julian Carry Dynamics*

---

### Phase I: Static Stability (Low Entropy)
**Single base (like $5^n$)** — Completed  
- Julian's First Law  
- Julian Constant ($C_J$)  
- Recurstable Numbers

**Multiple bases (like $5^n + 6^n$)** — Working On It  
- The constant still shows up  
- Still writing the clean proof

---

### Phase II: Dynamic Transition (Medium Entropy)

At this stage, the tail is no longer constant, but it follows a repeating cycle instead.

**Example:** The $11^n$ Cycle   
I observed that the last two digits of $11^n$ follow a very predictable pattern:     
$11, 21, 31, 41, 51, 61, 71, 81, 91, 01, \dots$  (repeats every $10$ steps)

**Question:** when the tail exhibits a repeating pattern, does the leading part synchronize and vary in step with it?  

I refer to this as the **coupling effect**, and it is the next major question I want to explore.

---

### Phase III: Edge of Chaos (High Entropy)
I sketched this conceptual diagram to visualize the phase transition from low to high entropy.

![Manuscript-04: Phase Transition Concept](https://github.com/JulianWong310/Julian-Carry-Dynamics/blob/main/2026-04-15-julian-carry-dynamics/asset/04_phase_transition_concept.png)
*Caption: Julian's conceptual diagram mapping the Phase Transition of Julian Carry Dynamics*

At this stage, the tail reaches a level of complexity where it seems practically random.

**Example:** The $3^n$ "Wild" Cycle   
I tracked the last two digits of powers of 3, the sequence feels much more chaotic:  
$03, 09, 27, 81, 43, 29, 87, 61, 83, 49, 47, 41, 23, 69, 07, 21, 63, 89, 67, 01, \dots$
It takes exactly 20 steps to return to the start, which looks rather wild.

This is not fixed (like $5^n$) and not super simple (like $11^n$).  
They live near the **Edge of Chaos**.

**Questions:**
- When the tail gets this messy, does the Leading Part still follow any rule?  
- And if so, what is the upper bound on its complexity?

Even at the edge of chaos, I believe some rules still survive.

---

### The Big Goal
Even when numbers appear random, there is often a deeper logic hidden beneath the surface.
If this holds true for numbers, perhaps it also applies to other things—seemingly random phenomena like weather patterns, heartbeats, or traffic flow.

That is why I keep exploring.

---

## 10. Acknowledgments & Research Methodology

1. **Intellectual Property & Naming Rights Assertion:**
The core theoretical framework and mathematical insights presented in this study are the independent discoveries of **Julian Wong**. As the primary investigator, Julian Wong claims full naming rights and intellectual priority over the following established terminology:

      * **Recurstable Numbers:** The overarching classification for integers with stable-tail power sequences.
      * **Julian’s First Law:** The linear recurrence relation $A_n = B \cdot A_{n-1} + C_J$.
      * **The Julian Constant ($C_J$):** The deterministic integer representing carry-over dynamics.
      * **The "Quinponent" Pattern:** The foundational discovery for powers of $5$.
      * **Julian Carry Dynamics:** The prospective field investigating terminal stability as a driver for the evolution of leading numerical sequences.


2. **Mathematical Guidance:** I would like to thank my mother, Dong Cang. She introduced and taught me algebra, guided me to use variables (such as $A_n$) and powers of ten ($10^k$) to convert my thoughts into a framework.

---

**License:** This mathematical manuscript is released under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).
You are free to share and adapt this material for any purpose, provided you give appropriate credit to the original author: **Julian Wong**. 

*Copyright © 2026 Julian Wong. All rights reserved for original mathematical concepts and handwritten manuscripts.*
