# The Digit Factory — Worksheet

Print this. Fill it in with a pencil at the bench, not from the internet.

Rule for every table: **1 means the wire is at +. 0 means it is at −.** And the thing that
makes this project odd: on your common-anode display a **0 lights a bar** and a **1 leaves it
dark**. The gates here are built to answer the *dark* question, so a 1 out of a gate is a bar
you cannot see.

---

## 1. Your display's pins

If you built the Score Tower you already did this — copy the map across and skip to part 2.

Probe wire: + rail → 1 kΩ → the pin you are testing. − wire: straight from the − rail. Put the
**probe on pin 3** and touch the − wire to each other pin in turn.

| Display pin | Bar that lit | Guide says |
|:-:|:-:|:-:|
| 1 | | e |
| 2 | | d |
| 3 | — common — | |
| 4 | | c |
| 5 | | decimal point |
| 6 | | b |
| 7 | | a |
| 8 | — common — | |
| 9 | | f |
| 10 | | g |

**If yours disagrees, yours is right.** Cross out the display pin numbers in the README and
write yours in before you wire anything.

---

## 2. Three switches, eight numbers

Fill this in from the lamps, with the gates not yet built. C is 4, B is 2, A is 1.

| Number | C | B | A | Lamps you can see |
|:-:|:-:|:-:|:-:|---|
| 0 | | | | |
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |
| 4 | | | | |
| 5 | | | | |
| 6 | | | | |
| 7 | | | | |

**a.** Three switches give how many different numbers? ____________

**b.** Four switches? ____________  Ten switches? ____________

**c.** Pull the A jumper out completely. What does the A lamp do, and why?

_________________________________________________

---

## 3. The font, from your own display

Build to the end of Stage 4, then set all eight numbers and mark which bars are lit.

| Number | a | b | c | d | e | f | g | bars lit | bars dark |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0 | | | | | | | | | |
| 1 | | | | | | | | | |
| 2 | | | | | | | | | |
| 3 | | | | | | | | | |
| 4 | | | | | | | | | |
| 5 | | | | | | | | | |
| 6 | | | | | | | | | |
| 7 | | | | | | | | | |

**a.** Add up the "bars lit" column: ____________  And the "bars dark" column: ____________

**b.** Which of those two numbers is smaller? ____________

**c.** So which question is cheaper to build a circuit for — "which bars light?" or "which bars
stay dark?" ____________________

**d.** Which segment is dark for the fewest numbers? ____________ How many gates does its
equation need? ____________

---

## 4. Derive three equations yourself

The guide works out segment **a** in full. Do these three the same way: write the dark numbers
in binary, then find what is true of all of those rows and of no other row.

### Segment b — dark for 5 and 6

| dark for | C | B | A |
|:-:|:-:|:-:|:-:|
| 5 | | | |
| 6 | | | |

What is the same about both rows? _________________________________________

What is *different* between C, B and A in both rows? _________________________________________

**b dark = _______________________________**  Gates needed: ________

### Segment e — dark for 1, 3, 4, 5, 7

| dark for | C | B | A |
|:-:|:-:|:-:|:-:|
| 1 | | | |
| 3 | | | |
| 4 | | | |
| 5 | | | |
| 7 | | | |

Four of those five rows have one thing in common. Which? _______________

Which row is the odd one out? _______  What is true of it? _______________

**e dark = _______________________________**  Gates needed: ________

### Segment g — dark for 0, 1 and 7

| dark for | C | B | A |
|:-:|:-:|:-:|:-:|
| 0 | | | |
| 1 | | | |
| 7 | | | |

**g dark = _______________________________**  Gates needed: ________

*Check all three against the guide's equation cards. If yours is different but still gives the
right answer for all eight numbers, yours is also correct — write down which one uses fewer
gates.*

---

## 5. Counting the cost

**a.** Count the gates in the wire list: ____________

**b.** Add up "gates needed" for all seven segments as if nothing were shared. The guide says
twenty-nine; check it: ____________

**c.** How many gates does sharing save? ____________ How many chips is that? ____________

**d.** Which signal is shared by the most segments? ____________  By how many? ____________

**e.** A CD4511 does this whole job in one chip. Yours takes six. Write down one thing your
version can do that the CD4511 cannot:

_________________________________________________

**f.** Add a fourth switch, D, worth 8. The font table goes from eight rows to sixteen. Work
out segment **a**'s new dark list (it is dark for 1 and 4, and now also for 11, 12, 14 and 15 if
you use the usual hex font). How many gates now? ____________

---

## 6. Predict before you look

Write the prediction **first**, then try it.

| What you do | Your prediction | What happened | Right? |
|---|---|---|:-:|
| Move the wire on CD4081 #1 pin 1 from B̅ to plain B | | | |
| Pull the wire out of CD4081 #1 pin 2 and leave it dangling | | | |
| Wire segment a's resistor straight to − instead of to the gate | | | |
| Move the display's common pin from + to − | | | |
| Pull the CD4070 out of the board altogether | | | |
| Swap the two inputs of the A⊕C gate over | | | |

The last one is the interesting one. **Why does it make no difference?** And name one gate on
your board where swapping the inputs *would* matter:

_________________________________________________

---

## 7. Why it is dim, with numbers

A CD4081 output pulls down about **1 mA** at 5 V. A red segment wants about 10 mA to look
bright.

**a.** So your segments run at roughly what fraction of bright? ____________

**b.** The 220 Ω resistor: if the chip could push as hard as it liked, 5 V minus the LED's
1.8 V across 220 Ω would give how many mA? ____________

**c.** So which one is actually limiting the current — your resistor, or the chip? ____________

**d.** Run the board at 9 V. The chip can then pull about 2.6 mA. Is the digit brighter?
____________  Did you change any resistor? ____________

**e.** One gate takes about **125 ns** to answer at 5 V. Segment c is the deepest: inverter,
OR, OR, inverter — four gates in a row. How long after you flip a switch is that bar right?

____________ ns. And segment b, which is only two gates deep? ____________ ns

**f.** How many times a second could you change the number and still have the display keep up?

____________ times a second. Show your working: ________________________________

---

## 8. Challenges

**Challenge A — make it count by itself.**
Borrow the two CD4013s from the Quiz Buzzer. Wire each flip-flop as a toggle (D to its own Q̅),
clock the first from a button, and clock each later one from the previous stage's Q̅. Feed the
three Q outputs into your A, B and C rows.
*You have now built a CD4026 out of parts. Write down which half you built today:* ____________

**Challenge B — hexadecimal.**
Add the fourth switch and show A, b, C, d, E, F for 10 to 15 — the way a memory dump looks.
Sketch all six of those shapes on seven segments first. Two of them have to be lower case.
*Why?* _________________________________________

**Challenge C — race the Score Tower.**
Feed the same three bits into both boards. Is there a moment, right after a switch flips, when
the two displays disagree? *What would you need to see it?* ____________

**Challenge D — think, don't build.**
You want a decimal point that lights only for odd numbers. Which single wire does that, and
which gate do you need? ____________________

**Challenge E — the lazy version.**
Work out how many gates you would need if you asked "which bars light?" instead, and add the
seven inverters. Chips: ____________ against six. *This is the decision Section 3 is about.*

---

## 9. Notebook

Real engineers write down what went wrong. It is how you stop making the same mistake twice.

**A gate I wired wrong, and how I found it:**

_________________________________________________

_________________________________________________

**The equation that took longest to see:**

_________________________________________________

**The thing that surprised me most:**

_________________________________________________

**Something I want to build next:**

_________________________________________________
