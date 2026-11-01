# Pocket Adder — Worksheet

Print this. Fill it in with a pencil at the bench, not from the internet.

Rule for every table: **1 means the wire is connected to +5 V (HIGH). 0 means it's connected to − (LOW).**
"Lamp lit" is 1. "Lamp dark" is 0.

---

## 1. The Half Adder — Stage 1

Inputs $A_0$ and $B_0$. Gates: CD4070 (XOR gate 1, pins 1, 2 $\rightarrow$ 3) and CD4081 (AND gate 1, pins 1, 2 $\rightarrow$ 3).

| $A_0$ | $B_0$ | Sum $S_0$ (XOR) | Carry $C_0$ (AND) | Binary ($C_0 S_0$) | Decimal Total |
|:---:|:---:|:---:|:---:|:---:|:---:|
| 0 | 0 | | | | 0 |
| 0 | 1 | | | | 1 |
| 1 | 0 | | | | 1 |
| 1 | 1 | | | | 2 |

**Finish the sentence:** Sum $S_0$ is 1 when the two inputs are ________________________________.

**Finish the sentence:** Carry $C_0$ is 1 when ________________________________.

**Why is XOR called "addition without carry"?**

____________________________________________________________________________________

---

## 2. The Full Adder Column — Predict before you test

A Full Adder takes three inputs: $A_1$, $B_1$, and the Carry-In $C_0$ from the column next door.
Fill in your predictions **first**, then test them on the breadboard or simulator.

| $A_1$ | $B_1$ | $C_0$ | Intermediate Sum ($A_1 \oplus B_1$) | First Carry ($A_1 \cdot B_1$) | Second Carry (Int $\cdot C_0$) | Final Sum $S_1$ | Final Carry $S_2$ | Decimal Total |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 0 | 0 | 0 | | | | | | 0 |
| 0 | 0 | 1 | | | | | | 1 |
| 0 | 1 | 0 | | | | | | 1 |
| 0 | 1 | 1 | | | | | | 2 |
| 1 | 0 | 0 | | | | | | 1 |
| 1 | 0 | 1 | | | | | | 2 |
| 1 | 1 | 0 | | | | | | 2 |
| 1 | 1 | 1 | | | | | | 3 |

**The crucial question:** Can *First Carry* and *Second Carry* ever both be 1 at the same time?
(Circle one): **YES / NO**

**Explain why:** ____________________________________________________________________

____________________________________________________________________________________

*(Hint: If First Carry is 1, what must $A_1$ and $B_1$ be? What does that make the Intermediate Sum?)*

---

## 3. The Whole Two-Bit Calculator — Stage 2

Test your finished circuit with these additions. Record what your LEDs show.

| Math problem | $A$ ($A_1 A_0$) | $B$ ($B_1 B_0$) | LED $S_2$ (4s) | LED $S_1$ (2s) | LED $S_0$ (1s) | Binary Result | Decimal Checked |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| $0 + 0$ | 00 | 00 | | | | | ☐ |
| $1 + 0$ | 01 | 00 | | | | | ☐ |
| $1 + 1$ | 01 | 01 | | | | | ☐ |
| $2 + 1$ | 10 | 01 | | | | | ☐ |
| $2 + 2$ | 10 | 10 | | | | | ☐ |
| $2 + 3$ | 10 | 11 | | | | | ☐ |
| $3 + 1$ | 11 | 01 | | | | | ☐ |
| $3 + 3$ | 11 | 11 | | | | | ☐ |

**Maximum calculation:** What is the largest number this circuit can produce? ________

**Why doesn't it reach 7?** __________________________________________________________

---

## 4. The Speed of Math (Ripple Delay)

Electricity travels fast, but logic gates take time to switch. At 5 V, a CD4000-series gate takes
about **125 nanoseconds (ns)** to flip its output after the inputs change.

**a. Trace the longest path:**
Suppose $A_0 = 1$ and $B_0 = 1$. The carry $C_0$ is born in Bit 0's AND gate.
Count how many gates the signal must travel through to reach the final $S_2$ lamp:

1. CD4081 Gate 1 (AND in Bit 0): 125 ns
2. CD4081 Gate 3 (AND in Bit 1): 125 ns
3. CD4071 Gate 1 (OR in Bit 1): 125 ns

**Total delay for Bit 2 to settle:** _____________ ns

**b. Scaling up:**
In an old 8-bit computer (like a Commodore 64 or Apple II), a simple ripple adder chained 8 full adders.
If each full adder column adds 250 ns of carry delay:

- Total carry delay across 8 bits: _____________ ns
- How many additions could it perform per second? _____________ additions/sec

**c. Modern 64-bit CPUs:**
If an Intel Core or Apple M-series processor used a simple ripple adder across 64 bits, how many
nanoseconds would one addition take?

_____________ ns

Why couldn't a 4 GHz computer work if it had to wait that long?

____________________________________________________________________________________

---

## 5. Extension Challenges

**Challenge A — The Half Subtractor:**
Can you build a circuit that calculates $A - B$?
For 1-bit numbers, the difference $D = A \oplus B$ (the exact same XOR gate!).
The *Borrow* signal $B_{out}$ is 1 only when $A = 0$ and $B = 1$.
*Hint:* What single gate do you need to add before the AND gate to make $B_{out} = \text{NOT}(A) \text{ AND } B$?

Sketch the gates:

<br><br><br>

**Challenge B — Detecting Overflow:**
In a 2-bit system where numbers can only be 0 to 3, any result of 4 or higher is an "overflow".
Which single lamp in your circuit already tells you that an overflow happened?

Answer: _____________

---

## 6. Engineer's Notebook

Real engineers write down what went wrong. It's how you stop making the same mistake twice.

**Something that didn't work at first, and what fixed it:**

____________________________________________________________________________________

____________________________________________________________________________________

**The thing that surprised me most about this circuit:**

____________________________________________________________________________________

____________________________________________________________________________________
