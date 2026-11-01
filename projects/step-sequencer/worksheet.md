# Step Sequencer — Worksheet

Print this. Fill it in with a pencil at the bench, not from the internet.

Rule for every measurement: listen with your ears, watch the LEDs, and write down what the circuit
actually does.

---

## 1. Tempo & Beats Per Minute (BPM) — Stage 1

Fit the **1 µF capacitor** and the **100 kΩ tempo pot** on CD40106 pins 1 and 2.
Turn the pot to three different positions (minimum resistance, halfway, maximum resistance).
Count the LED flashes for a full 15 seconds, then calculate Beats Per Minute ($\text{BPM} = \text{flashes} \times 4$).

| Potentiometer setting | Flashes in 15 seconds | Beats per second (÷ 15) | Beats per Minute (BPM) | Musical feel (Slow / Dance / Frenzy) |
|---|:---:|:---:|:---:|---|
| Turned all the way right (Max R) | | | | |
| Centered (Halfway) | | | | |
| Turned all the way left (Min R) | | | | |

The Schmitt-trigger formula is:
$$f \approx \frac{1.23}{R \times C}$$

**a.** If $R = 100\text{ k}\Omega$ and $C = 1\text{ \mu F}$, what is the predicted frequency? _____________ Hz

**b.** Multiply that frequency by 60 to find predicted BPM: _____________ BPM

**c.** How close was your measured center BPM to the prediction? _____________

---

## 2. Modulo Looping with the CD4017 — Stage 2

The CD4017 is a decade counter — it naturally counts from 0 up to 9 (ten steps).
To make an 8-step sequencer, we connect output Q8 (pin 9) directly to RESET (pin 15).
The instant count 8 is reached, the chip zeroes itself back to count 0.

Fill in which pin connects to RESET for different musical loop lengths:

| Desired loop length | Musical time signature | Which step resets the count? | Which CD4017 pin goes to pin 15 (RESET)? |
|---|---|:---:|:---:|
| 8 steps (your build) | 4/4 standard dance | Q8 | **Pin 9** |
| 4 steps (short riff) | 4/4 short loop | Q4 | |
| 6 steps (triplet groove) | 6/8 shuffle | Q6 | |
| 3 steps (waltz) | 3/4 waltz | Q3 | |

**Why can't you see the reset step light up?**
When the counter reaches the reset output, how long does the chip take to reset? (Hint: CMOS gate delay is ~100 nanoseconds).

____________________________________________________________________________________

---

## 3. Musical Pitch vs. Resistance — Stages 3 & 4

The audio oscillator (CD40106 pins 3 & 4) produces a pitch based on the resistance connected
to the timing capacitor ($C = 0.1\text{ \mu F}$).

Smaller resistance = faster vibration = **higher pitch**.
Larger resistance = slower vibration = **lower pitch**.

| Musical note | Target frequency | Required resistance ($R \approx \frac{1.23}{f \times C} - 1\text{ k}\Omega$) |
|:---:|:---:|:---:|
| C3 (Deep Bass) | 131 Hz | $\approx 93\text{ k}\Omega$ |
| A3 (Bass) | 220 Hz | $\approx 55\text{ k}\Omega$ |
| C4 (Middle C) | 262 Hz | $\approx 46\text{ k}\Omega$ |
| E4 | 330 Hz | $\approx 36\text{ k}\Omega$ |
| G4 | 392 Hz | $\approx 30\text{ k}\Omega$ |
| A4 (Concert Pitch) | 440 Hz | $\approx 27\text{ k}\Omega$ |
| C5 (High C) | 523 Hz | $\approx 22\text{ k}\Omega$ |

Tune your 8 trim pots to play an 8-note melody. Write down what notes you picked:

| Step 1 | Step 2 | Step 3 | Step 4 | Step 5 | Step 6 | Step 7 | Step 8 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| | | | | | | | |

---

## 4. The Bilateral Switch (CD4066) — Stage 5

**a. Note Gating:**
Disconnect the clock wire from CD4066 pin 13 and tie pin 13 straight to +5 V.
Describe the sound:

____________________________________________________________________________________

Now plug pin 13 back into clock pin 2. Describe what changed about the rhythm:

____________________________________________________________________________________

**b. Analog Portamento (Slide):**
When the SLIDE switch connects a capacitor across the pitch bus, what happens when the note jumps
from a low pitch to a high pitch?

____________________________________________________________________________________

---

## 5. Extension Challenges

**Challenge A — The 4-Step / 8-Step Selector Switch:**
Fit a small toggle switch (or single jumper wire) between CD4017 pin 15 (RESET) and either
pin 10 (Q4) or pin 9 (Q8). Switch between 4-step techno loops and 8-step melodies while
the sequencer is running!

**Challenge B — The Light-Controlled Step:**
Replace one of the 8 trim pots with a photoresistor (LDR).
Wave your hand over the board as the sequencer plays. Which step changes pitch, and what does it sound like?

____________________________________________________________________________________

---

## 6. Engineer's Notebook

Real engineers document problems and solutions.

**Something that didn't work at first, and what fixed it:**

____________________________________________________________________________________

____________________________________________________________________________________

**The coolest musical melody or bassline I made with this circuit:**

____________________________________________________________________________________

____________________________________________________________________________________
