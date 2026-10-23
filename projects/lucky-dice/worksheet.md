# Lucky Dice — Worksheet

Print this. Fill it in with a pencil at the bench, not from the internet.

Rule for every table: **1 means the wire is connected to +. 0 means it's connected to −.**
"Light on" is 1. "Light off" is 0.

---

## 1. How fast is your clock, really?

Fit the **100 kΩ and the 10 µF**. Watch the clock lamp on CD4093 pin 3 and count blinks for
a full 20 seconds. Do it three times — you will not get the same answer twice, and that's
the point.

| Try | Blinks in 20 s | Blinks per second (÷ 20) |
|:-:|:-:|:-:|
| 1 | | |
| 2 | | |
| 3 | | |

**Average blinks per second:** ______________

The prediction from the formula, `f = 1.23 ÷ (R × C)`, is **1.2 per second**.

**How close were you?** ______________

**Name two reasons your answer isn't exactly 1.2:**

1. _________________________________________________

2. _________________________________________________

---

## 2. Predict before you measure

Work these out *before* you plug anything in. `R × C` first, then `f = 1.23 ÷ (R × C)`.

| R | C | R × C | Predicted f | Measured f | Right? |
|---|---|:-:|:-:|:-:|:-:|
| 100 kΩ | 10 µF | 1 s | 1.2 | | |
| 100 kΩ | 0.1 µF | | | | |
| 1 MΩ | 10 µF | | | | |

The last one is slow. How long would you have to watch to count 20 blinks?
______________

The second one is too fast to count by eye. Write "too fast to count" and say roughly what
speed a human eye gives up at:

**My eye stops seeing separate blinks somewhere around ______ per second.**

---

## 3. The register: no feedback

Stage 2. D1 (A pin 5) is wired to +. Press RESET, then hold ROLL for one tick at a time
(use the slow clock). Write down Q1, Q2 and Q3 after each tick.

| After tick | Q1 | Q2 | Q3 |
|:-:|:-:|:-:|:-:|
| 0 (RESET) | | | |
| 1 | | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |

**Finish the sentence:** on every tick, each flip-flop copies ________________________________

**How many ticks until the very first bit reaches Q3?** ______________

**Why does the pattern stop changing after that?**

_________________________________________________

---

## 4. The register: with feedback

Stage 3. The CD4077 (XNOR) is fitted. Press RESET and tick through the cycle. Before each
tick, work out what XNOR(Q2, Q3) will be, then check.

| Tick | Q1 | Q2 | Q3 | XNOR(Q2, Q3) — predicted | Next Q1 — observed |
|:-:|:-:|:-:|:-:|:-:|:-:|
| 0 | 0 | 0 | 0 | | |
| 1 | | | | | |
| 2 | | | | | |
| 3 | | | | | |
| 4 | | | | | |
| 5 | | | | | |
| 6 | | | | | |
| 7 | | | | | |

**Is tick 7 the same as tick 0?** ______________

**How many different states did you pass through before it repeated?** ______________

**Three bits have 8 states. Which one did you never visit?** ______ ______ ______

---

## 5. The trap

Fill in your *prediction* first. Then do the Stage 3 experiment and fill in what happened.

| Gate fitted | Start at | Q2, Q3 are | Gate gives | Next state — predicted | Next state — observed |
|---|:-:|:-:|:-:|:-:|:-:|
| CD4077 (XNOR) | 111 | 1, 1 | | | |
| CD4077 (XNOR) | 000 | 0, 0 | | | |
| CD4070 (XOR) | 000 | 0, 0 | | | |
| CD4070 (XOR) | 111 | 1, 1 | | | |

**Which of those rows is a trap — a state that leads back to itself?**

_________________________________________________

**RESET puts the register at 000. Why does that make XOR a bad choice for this project, and
XNOR a good one?**

_________________________________________________

_________________________________________________

**Power on, without pressing RESET, with the XNOR fitted. Do it 8 times. How many times did
the pips come on all lit?** ______ out of 8

**What should the answer be if each of the 8 states is equally likely?** ______

---

## 6. From three bits to seven lamps

Fill in the four decoder signals for each state, then say which pips light.

| State | a = Q2 OR Q3 | b = Q3 | c = Q2 AND Q3 | C = Q1 | Pips lit | Face |
|:-:|:-:|:-:|:-:|:-:|---|:-:|
| 000 | | | | | | |
| 100 | | | | | | |
| 110 | | | | | | |
| 011 | | | | | | |
| 101 | | | | | | |
| 010 | | | | | | |
| 001 | | | | | | |

Pip names: **TL** top-left, **TR** top-right, **ML** middle-left, **MR** middle-right,
**C** centre, **BL** bottom-left, **BR** bottom-right.

Signal **a** lights TL and BR. Signal **b** lights TR and BL. Signal **c** lights ML and MR.
Signal **C** lights the centre.

**Which face is missing from the tick sequence?** ______________

**Which state is dark, and what do you do when the die shows it?**

_________________________________________________

---

## 7. Roll a six every time

You are about to cheat a machine that is supposed to be random.

Put the clock in **slow mode** (100 kΩ and 10 µF). Press RESET. Hold ROLL and watch the
pips. Let go the moment you see a six.

| Try | Press RESET first? | Face showing when you let go |
|:-:|:-:|:-:|
| 1 | yes | |
| 2 | yes | |
| 3 | yes | |
| 4 | yes | |
| 5 | yes | |

**How many ticks after RESET is the six?** ______________

**Now fit the 0.1 µF (fast clock) and try to do the same thing 5 times:**

| Try | Face showing when you let go |
|:-:|:-:|
| 1 | |
| 2 | |
| 3 | |
| 4 | |
| 5 | |

**How many sixes?** ______ out of 5

**One tick lasts about ______ ms at the fast clock, and your thumb wanders by about
______ ms. Why does that make the die random?**

_________________________________________________

**So is it random? Explain what "pseudo-random" means, using this circuit.**

_________________________________________________

_________________________________________________

---

## 8. Is it fair?

Roll the die 60 times on the fast clock. Press RESET only once, at the start. Put a tally
mark for each result.

| Result | Tally | Total |
|:-:|---|:-:|
| dark | | |
| 1 | | |
| 2 | | |
| 3 | | |
| 4 | | |
| 5 | | |
| 6 | | |
| **Total** | | **60** |

**If all seven results were equally likely, how many of each would you expect in 60 rolls?**
______________ (60 ÷ 7)

**Biggest total:** ______ for ______  **Smallest total:** ______ for ______

**Is the gap between biggest and smallest what you expected? Roll 60 more and see whether
the same result is biggest.**

_________________________________________________

**About what fraction of rolls came up dark?** ______ out of 60 → 1 in ______

**A real die never shows "dark". What would you do with a dark roll so the other six
faces stay equally likely?**

_________________________________________________

---

## 9. Challenges

**A. Count the ticks.** The fast clock runs at about 120 ticks a second. How long does one
lap of the seven states take? How many laps do you go round while your thumb is down for
half a second?

_________________________________________________

**B. Four bits.** Add the fourth flip-flop (see the Bonus in the guide). The cycle has 15
states. Tick through it, write the states down, and find the trap. Is it 1111 or 0000?

_________________________________________________

**C. A roll-again lamp.** Build the Bonus lamp that is lit for every state except dark.
Which gate computes it? Which two signals go into it?

_________________________________________________

**D. Move the faces.** There are 720 ways to hand six faces to six states, and only some
need two gates. Pick a different assignment from the table in Section 6 and work out what
the decoder would cost: how many gates, and which kinds?

_________________________________________________

**E. Two dice.** Think about it — you don't have to build it. How many more flip-flops would
a second die need? Could the two dice share one clock? What would be wrong with letting them
share one feedback gate?

_________________________________________________

---

## 10. Notebook

Real engineers write down what went wrong. It's how you stop making the same mistake twice.

**Something that didn't work, and what fixed it:**

_________________________________________________

_________________________________________________

**The thing that surprised me most:**

_________________________________________________

**Something I want to build next:**

_________________________________________________
