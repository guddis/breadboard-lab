# The Siren Box — Worksheet

Print this. Fill it in with a pencil at the bench, not from the internet.

**How to measure a pitch without a meter.** Open `guide.html` on a phone or laptop next to
your board. Hold the same button on the page and on your box at the same time. If the two
pitches are close but not identical you will hear a slow wobble — that wobble is the
difference between them. When the wobble disappears, they match. Musicians call this
*beating*, and it is how a piano gets tuned.

---

## 1. Predict the four notes

Two formulas. The naive one, and the one that admits the chip has its own resistance.

> **naive:** f = 1.23 ÷ (R × C)
> **corrected:** f = 1.23 ÷ ((R + 1 000 Ω) × C)
>
> C is the 104 capacitor: 0.1 µF, which is 0.0000001 farads.

Each button's resistor is in parallel with the 1 MΩ, which changes it by about 1% — small
enough to ignore in your working, but write it down if you want to be exact.

| Button | R | Naive f | Corrected f |
|:-:|:-:|:-:|:-:|
| 1 | 10 kΩ | | |
| 2 | 5.1 kΩ | | |
| 3 | 2 kΩ | | |
| 4 | 1 kΩ | | |

**Which button do the two formulas disagree about most?** ______________

**Why that one and not the others?**

_________________________________________________

---

## 2. Measure them

| Button | Corrected prediction | What you measured | Difference |
|:-:|:-:|:-:|:-:|
| 1 | | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |

**Were the top notes closer to the naive or the corrected prediction?** ______________

---

## 3. Find the hidden resistance inside your chip

This is real reverse-engineering. You know the capacitor and you have measured the
frequency, so you can work backwards to the *total* resistance the oscillator actually saw —
then subtract the resistor you plugged in. Whatever is left over is inside the chip.

Because C is 0.1 µF, the arithmetic collapses to one division:

> **R total = 12 300 000 ÷ f**

| Button | Your f | R total = 12 300 000 ÷ f | R you plugged in | Hidden = total − yours |
|:-:|:-:|:-:|:-:|:-:|
| 1 | | | 10 000 Ω | |
| 2 | | | 5 100 Ω | |
| 3 | | | 2 000 Ω | |
| 4 | | | 1 000 Ω | |

**Average of your four "hidden" answers:** ______________ Ω

The datasheet figure works out at about **1 000 Ω**.

**a.** Are your four answers roughly the same as each other? ______________

**b.** If one is wildly different, which button is it, and why is that measurement the
least trustworthy?

_________________________________________________

**c.** You just measured something the datasheet never prints as a single number, using a
buzzer and some arithmetic. Write down, in one sentence, what you actually did:

_________________________________________________

---

## 4. Two buttons at once

**Before you press:** will two buttons together give a pitch that is higher than both,
lower than both, or in between? ______________

**Why?** _________________________________________________

| Buttons held | Combined R | Predicted f | Measured f |
|:-:|:-:|:-:|:-:|
| 1 alone | 10 kΩ | | |
| 1 + 2 | | | |
| 1 + 2 + 3 | | | |
| all four | | | |

> Two resistors in parallel: R = (a × b) ÷ (a + b)

**The rule for parallel resistors, in your own words:**

_________________________________________________

---

## 5. Which note is loudest?

Hold each button and rank them by loudness — not by pitch.

| Button | Frequency | Loudness rank (1 = loudest) |
|:-:|:-:|:-:|
| 1 | | |
| 2 | | |
| 3 | | |
| 4 | | |

**The loudest note is around ______ Hz.**

That is your buzzer's *resonant frequency* — the speed it likes best, the same way a bell or
a guitar string has one.

**Name two other objects that have a frequency they like best:**

_________________________________________________

---

## 6. The theremin

| What you do to the photoresistor | Pitch (high / middle / low / tick) |
|---|:-:|
| Phone torch shining on it | |
| Normal room light | |
| Hand hovering 5 cm above | |
| Hand pressed over it | |
| Board taken to a window in daylight | |

**Does more light mean more or less resistance?** ______________

**How do you know that from what you just heard?**

_________________________________________________

**Try to play a recognisable tune. How did that go?**

_________________________________________________

---

## 7. The two slow oscillators

These are slow enough to count with a clock — no app needed. Count for 20 seconds.

| Oscillator | R | C | Predicted rate | Counted in 20 s | ÷ 20 = rate |
|---|:-:|:-:|:-:|:-:|:-:|
| WAIL | 100 kΩ | 10 µF | 1.2 | | |
| CHOP | 10 kΩ | 10 µF | 11 | | |

**The CHOP oscillator uses a resistor ten times smaller than WAIL's. Is it ten times
faster? Should it be?** ______________

**Electrolytic capacitors are much less accurate than ceramic ones. Does that show up in
your answers?**

_________________________________________________

---

## 8. The siren's two notes

Hold button 1 with WAIL on. The pitch flips between two values.

**Low note:** ______ Hz  **High note:** ______ Hz

The switch puts a 10 kΩ in parallel with your button's 10 kΩ.

**a.** What is 10 kΩ in parallel with 10 kΩ? ______________

**b.** So what should the high note be? ______________

**c.** Which note happens when the switch is **closed** — the high one or the low one?

______________

**d.** Explain (c) in one sentence:

_________________________________________________

---

## 9. Hearing test

Frequencies you can hear fade as you get older. Hold each button and go round the house.

| Person | Age | 1 133 Hz | 2 040 Hz | 4 168 Hz | 6 295 Hz |
|---|:-:|:-:|:-:|:-:|:-:|
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |

**Was there any note you could hear that an adult could not?** ______________

**Careful:** loudness is not the same as pitch. Somebody might say "I can't hear it" when
they mean "it's very quiet". Ask them to tell you *when* you press, with their eyes shut,
and see if they get it right.

---

## 10. Challenges

**A. A third character.** WAIL and CHOP give four sounds. If you had a *fourth* oscillator,
how many sounds would there be? What if you had ten?

_________________________________________________

**B. Make the siren sweep instead of flip.** A real British siren slides smoothly up and
down instead of jumping between two notes. This box cannot do that. Explain why switching a
resistor can only ever give you jumps.

_________________________________________________

**C. Two switches.** The CD4066 has four switches and you used one. Wire a second one with
its own resistor, controlled by the CHOP oscillator instead of Q2. What do you predict? Try
it.

_________________________________________________

**D. The 22 pF.** Fit the 22 pF as the audio timing capacitor instead of the 104. Predict
the frequency first. Then explain why what actually happens is nothing like your prediction.

_________________________________________________

**E. Silence.** There is a way to make the box completely silent, using the CHOP jumper and
nothing else. Find it, and explain what Q2 is doing.

_________________________________________________
