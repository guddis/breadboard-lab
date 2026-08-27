# The Reaction Machine — Worksheet

Print this. Fill it in with a pencil at the bench, not from the internet.

Rule for every table: **1 means the wire is connected to +. 0 means it's connected to −.**
"Light on" is 1. "Light off" is 0.

---

## 1. How fast is your clock, really?

Put the clock in **slow mode**: 100 kΩ and the 10 µF capacitor. Watch the LED on CD40106
pin 2 and count blinks for a full 20 seconds. Do it three times — you will not get the same
answer twice, and that's the point.

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

Now work out these *before* you plug anything in. `R × C` first, then
`f = 1.23 ÷ (R × C)`.

| R | C | R × C | Predicted f | Measured f | Right? |
|---|---|:-:|:-:|:-:|:-:|
| 100 kΩ | 10 µF | 1 s | 1.2 | | |
| 1 MΩ | 10 µF | | | | |
| 100 kΩ | 0.1 µF | | | | |
| 1 MΩ | 0.1 µF | | | | |

Two of those are too fast to count by eye. Write "too fast to count" and say roughly what
speed a human eye gives up at:

**My eye stops seeing separate blinks somewhere around ______ per second.**

---

## 3. Resistors side by side

Plug a second 1 MΩ in beside the first, in the same two holes.

**Before you switch on — will the game get faster or slower?** ______________

**Why?** _________________________________________________

| 1 MΩ resistors in parallel | Behaves like | Predicted f |
|:-:|:-:|:-:|
| 1 | 1 MΩ | 12 |
| 2 | | |
| 3 | | |
| 4 | | |

**The rule for resistors in parallel, in your own words:**

_________________________________________________

---

## 4. Read the counter's pinout

Fill this in from the pinout drawing in the guide — *not* from the wiring table. This is
the skill: getting a fact out of a datasheet without anyone translating it for you.

| Count | CD4017 output pin |
|:-:|:-:|
| 0 | |
| 1 | |
| 2 | |
| 3 | |
| 4 | |
| 5 | |
| 6 | |
| 7 | |
| 8 | |
| 9 | |

**Is there any pattern to it?** _________________________________________________

**Which pin is +, and which is −, on this chip?** + = ______  − = ______

**And on the other three chips?** + = ______  − = ______

---

## 5. The freeze pin

CD4017 pin 13 is called CLOCK INHIBIT. Try it both ways with a jumper before you wire the
flip-flop to it.

| Pin 13 connected to | What the ring does |
|:-:|---|
| − | |
| + | |

**When the ring is frozen, does the counter lose its place?** ______________

**How can you tell?** _________________________________________________

---

## 6. The flip-flop

Wire the two buttons, then poke the CD4013 by hand and watch pin 1.

| What you do | Pin 1 (FROZEN) after |
|---|:-:|
| Switch the power on, touch nothing | |
| Press STOP, let go | |
| Wait ten seconds | |
| Press STOP again | |
| Press RESET, let go | |
| Press RESET again | |

**What is different about this circuit compared with every circuit in Projects 01 and 02?**

_________________________________________________

_________________________________________________

**Why do you have to press RESET after switching the power on?**

_________________________________________________

---

## 7. The two verdict gates

Fill this in by thinking, then check it by playing.

| FROZEN | GOLD | WIN (pin 3) | MISS (pin 4) |
|:-:|:-:|:-:|:-:|
| 0 | 0 | | |
| 0 | 1 | | |
| 1 | 0 | | |
| 1 | 1 | | |

**Row 2 is the important one.** The dot is sitting on the gold light, but you haven't
pressed STOP. Why must WIN be 0?

_________________________________________________

**Can WIN and MISS ever both be 1 at the same time? Explain.**

_________________________________________________

---

## 8. Score sheet

One press per round. Ten rounds each. The machine tells you how far off you were — count
lamps from the gold one, the short way round, so the worst you can be is 5.

**Clock setting:** ______ × 1 MΩ  ·  **Beats per second:** ______

| Round | Player A: hit? | A: lamps off | Player B: hit? | B: lamps off |
|:-:|:-:|:-:|:-:|:-:|
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |
| 4 | | | | |
| 5 | | | | |
| 6 | | | | |
| 7 | | | | |
| 8 | | | | |
| 9 | | | | |
| 10 | | | | |
| **Total** | ___ / 10 | avg ___ | ___ / 10 | avg ___ |

---

## 9. Are you actually any good, or just lucky?

There are ten lamps. Someone pressing at a completely random moment would hit the gold one
about **1 time in 10**.

**My hit rate:** ______ out of 10

**Is that better than random?** ______________

**How many rounds would you need to play before you'd be confident it wasn't luck?**

_________________________________________________

---

## 10. Measure your own reaction time

This is the best thing in this project. You can measure something about your own body using
ten LEDs and a bit of arithmetic.

Each step of the ring lasts a fixed amount of time:

| Beats per second | One step lasts |
|:-:|:-:|
| 12 | 83 ms |
| 25 | 40 ms |
| 37 | 27 ms |
| 49 | 20 ms |

Your average "lamps off" from table 8 tells you how *spread out* your timing is.

**a.** Average lamps off: ______

**b.** One step lasts: ______ ms

**c.** a × b = ______ ms — that's roughly how much your timing wanders from press to press.

**d.** Play ten more rounds at double the speed. Does your answer to (c) come out about the
same, or double?

_________________________________________________

**e.** If it comes out about the same at both speeds, what does that tell you about where
the wandering comes from — the machine, or you?

_________________________________________________

---

## 11. Challenges

**A. Move the target.** Put the gold light at position 3 instead of 6. Which two wires do
you have to change, and to which pins?

_________________________________________________

**B. Two gold lights.** Could you make *two* of the lamps count as a win, so the game is
easier for a younger sibling? Which chip would you need a spare gate on, and what kind of
gate?

_________________________________________________

**C. A miss that isn't silent.** How would you make MISS produce a short buzz instead of
just a red light? What's the problem with wiring the buzzer straight to MISS?

_________________________________________________

**D. Nine lamps instead of ten.** The CD4017 has a RESET pin that jumps the count back to
zero. If you connected RESET to the count-9 output, what would happen? Try it. What does
that do to the odds of winning?

_________________________________________________

**E. Cheating.** There is a way to make the machine say you won every single time, by
moving one wire. Find it, then explain why the machine can't tell the difference.

(Careful: the answer involves *replacing* a wire, not adding one. Wiring a chip output to a
rail is rule 5, and it's a short circuit.)

_________________________________________________
