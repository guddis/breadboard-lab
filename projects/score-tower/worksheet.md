# The Score Tower — Worksheet

Print this. Fill it in with a pencil at the bench, not from the internet.

Rule for every table: **1 means the wire is connected to +. 0 means it's connected to −.**
"Bar lit" is 1 in the font tables, but watch out — on your common-anode display it takes a
**0** to light a bar. That difference is the whole project.

---

## 1. Find your display's pins

Do this before you wire anything. Probe wire: + rail → 1 kΩ → the pin you're testing.
− wire: straight from the − rail.

Put the **probe on pin 3**, then touch the − wire to each other pin in turn and write down
which bar lights.

| Display pin | Bar that lit | Matches the guide? |
|:-:|:-:|:-:|
| 1 | | (guide says e) |
| 2 | | (guide says d) |
| 3 | — common — | |
| 4 | | (guide says c) |
| 5 | | (guide says decimal point) |
| 6 | | (guide says b) |
| 7 | | (guide says a) |
| 8 | — common — | |
| 9 | | (guide says f) |
| 10 | | (guide says g) |

**If yours disagrees with the guide**, yours is right and the guide is a guess. Cross out the
display pin numbers in the README's segment table and write yours in.

---

## 2. The font, from your own display

Build Stage 2, then press COUNT ten times, stopping at each digit. Mark which bars are lit.

| Digit | a | b | c | d | e | f | g | how many bars |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0 | | | | | | | | |
| 1 | | | | | | | | |
| 2 | | | | | | | | |
| 3 | | | | | | | | |
| 4 | | | | | | | | |
| 5 | | | | | | | | |
| 6 | | | | | | | | |
| 7 | | | | | | | | |
| 8 | | | | | | | | |
| 9 | | | | | | | | |

**a.** Which bar is lit for the most digits? ______________

**b.** Which is lit for the fewest? ______________

**c.** Add up your "how many bars" column. That's how many segment-lightings it takes to count
0 to 9: ______________

**d.** Which two digits differ by only one bar? ______________ and ______________

---

## 3. Predict before you look

Write the prediction **first**, then test it. Score yourself honestly.

| What you do | Your prediction | What happened | Right? |
|---|---|---|:-:|
| Pull the **a** segment's wire out of its inverter and leave the input dangling | | | |
| Wire the **a** segment straight from CD4026 pin 10 to the resistor, no inverter | | | |
| Hold BLANK down and press COUNT four times, then let go | | | |
| Hold HOLD down and press COUNT four times, then let go | | | |
| Hold RESET down and press COUNT | | | |
| Wire CD4026 pin 3 to − instead of + | | | |

---

## 4. Counting

**a.** One digit shows how many different numbers? ______________

**b.** Two digits? ______________  Show your working: ________________________________

**c.** Three digits, if you added a third CD4026? ______________

**d.** How many chips would a five-digit counter need, counting inverters too?

Show your working: ________________________________

**e.** A CD4017 (Reaction Machine) needs one wire per count. A CD4026 needs seven wires for
*any* count 0–9. At what number of counts does the CD4026's way start using fewer wires?

______________

---

## 5. The bounce, with numbers

The debounce is a 100 kΩ resistor charging a 0.1 µF capacitor. That pair takes about
**10 milliseconds** to charge.

**a.** How many times a second could you press the button before the capacitor can't keep up?

______________ presses per second

**b.** A button's contacts bounce for something like half a millisecond. How many times longer
than that is the capacitor's 10 ms? ______________

**c.** Swap the 100 kΩ for 10 kΩ. The charging time drops to about 1 ms. Predict what happens,
then try it:

Prediction: ________________________________

What happened: ________________________________

**d.** The CD4026 can accept a clock up to 2.5 MHz — 2,500,000 counts a second. Your finger
manages about 5. Write the ratio: ______________

---

## 6. Carry and overflow

**a.** CARRY OUT is high for counts 0–4 and low for 5–9. Draw its shape over two full cycles
of the units digit:

```
count   0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9
carry
```

**b.** Mark every place on your drawing where the carry goes from low to **high**. How many? ____

**c.** The tens digit counts on a low-to-high edge. Which count does it move on? ____________

**d.** If the carry had been built the other way up, the scoreboard would count
0, 1, 2, 3, 4, then ______________ instead of 5.

**e.** Press COUNT a hundred times from 00. What is on the display? ______________

---

## 7. Challenges

**Challenge A — the one-resistor experiment.**
Pull the seven segment resistors out and replace them with a *single* 220 Ω between the
display's common pin and the + rail. Count from 0 to 9 and watch the brightness.
Which digit is brightest? ____________  Dimmest? ____________  Why?
*Then put the seven back.*

**Challenge B — count seconds instead of presses.**
Borrow the CD40106 oscillator from the Siren Box, slow it right down with a 1 MΩ and a 10 µF,
and feed it to CD4026 pin 1 in place of the button. Now it is a clock.
*Hint: you no longer need the debounce capacitor. Why not?*

**Challenge C — a stopwatch.**
Add Challenge B, then put HOLD on a button and RESET on another. What order do you have to
press them in to time something twice in a row?

**Challenge D — wire it to the Quiz Buzzer.**
Player 1's lamp signal can drive the count input, so buzzing in scores a point.
*Hint: the scoreboard counts on a rising edge. Which of the buzzer's signals rises exactly
once per buzz?*

**Challenge E — think, don't build.**
You want to count *down*. The CD4026 cannot. Find out what a chip that can is called, and
write down one thing it needs that the CD4026 doesn't have:

________________________________

---

## 8. Notebook

Real engineers write down what went wrong. It's how you stop making the same mistake twice.

**Something that didn't work, and what fixed it:**

_________________________________________________

_________________________________________________

**The thing that surprised me most:**

_________________________________________________

**Something I want to build next:**

_________________________________________________
