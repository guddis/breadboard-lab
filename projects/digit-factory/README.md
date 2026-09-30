# The Digit Factory

Three switches, nineteen logic gates, and a digit you can read.

The Score Tower had a chip that turned a number into seven segment signals and never showed
its working. This project is the working: you derive all seven equations from the font,
minimise them with a pencil, and wire them out of the same six gate chips the Gate Bench
introduced. No counter, no decoder, no code.

**Open [`guide.html`](https://guddis.github.io/breadboard-lab/projects/digit-factory/guide.html) in a browser** — that's the real guide, with diagrams
and a working simulator. This file is the bench reference: parts, wire lists, troubleshooting.

Build [the Score Tower](../score-tower/) first if you haven't. This one is the sequel, and it
assumes you have met a seven-segment display before.

---

## What it teaches

| Idea | Where it shows up |
|---|---|
| **A truth table is a specification** — and you can build straight from it | Section 4 |
| **Decoding, done by hand** — seven independent yes/no questions about one number | The whole project |
| **Active-low signals** — asking "which bars stay dark?" to save seven inverters | Section 3 |
| **Minimising** — spotting that two rows share "B is 0 and A differs from C" | Section 4, segment a |
| **Shared terms** — 19 gates instead of 29, because four signals get used more than once | Stage 3 |
| **Fan-out is free** — one inverter output feeding four gates | Stage 2 |
| **Binary, three bits** — and why the display cannot show an 8 | Section 2 |
| **Octal** — counting in eights, and where it came from | Section 2 |
| **Logic synthesis** — what a chip designer's tools do, at nineteen-gate scale | Section 4 |
| **Gate delay** — 125 ns a gate at 5 V, and segment c is four gates deep | Bonus 4 |
| **A chip's drive current is the real current limit**, not your resistor | Section 5 |

Total build time is about 2½ hours in 4 stages you can stop between. Stopping after Stage 3
leaves a display that shows 1, 2, 3 and 7 correctly and the rest nearly.

---

## Parts

Everything is in the kit, and every chip is one the Gate Bench used.

### Chips

| Chip | What it is | Gates used |
|---|---|---|
| CD4081 × 2 | Quad 2-input AND | 7 of 8 — one package is full |
| CD4071 × 2 | Quad 2-input OR | 7 of 8 — one package is full |
| CD4070 | Quad 2-input XOR | 2 of 4 |
| CD4069 | Hex NOT | 3 of 6 |

**All six chips are + on pin 14 and − on pin 7.** No exceptions in this project.

### Everything else

| Qty | Part | Notes |
|---|---|---|
| 1 | 7-segment display, **common anode** | The same part as the Score Tower. Red, not white |
| 7 | Resistor 220 Ω | One per segment. 150 Ω is fine and a little brighter |
| 3 | Resistor 100 kΩ | Pull-downs on the A, B and C input rows |
| 3 | Resistor 1 kΩ | The three input lamps |
| 3 | LED, any colour | Shows the binary number you have set. Fit them |
| 6 | Capacitor 0.1 µF (**104**) | One across each chip's power pins |
| 3 | Jumper wire, loose at one end | The A, B and C switches — free end into + or − |
| — | Hook-up wire | About fifty signal wires. Colours help |

### Power

3 AA cells (4.5 V) or a 5 V breadboard supply. The whole board draws about 15 mA. **Nothing in
this project goes near mains electricity.**

**If the digit is too dim, run the board at 9 V.** These chips are specified to 18 V, and a
CD4081 output pulls down about 2.6 mA at 10 V against about 1 mA at 5 V. Keep the 220 Ω
resistors in — at 5 V they do almost nothing, and at 9 V they are the insurance.

---

## Rules for not breaking things

1. **Unplug the power before you rewire.** Every time.
2. **+ on 14, − on 7, all six chips.** Enjoy it; the Score Tower was not like this.
3. **Never leave an input dangling.** Eleven unused input pins have to go to −. They are listed
   in the wire list below, and a floating CMOS input drifts and warms the chip.
4. **Never wire an output to + or −.** Gate outputs go to gate inputs, or through a 220 Ω to
   the display, and nowhere else.
5. **One output may feed many inputs.** B̅ goes to four gates; that is free. Two *outputs* in
   one breadboard row is the thing that is never allowed.
6. **Label the rows as you use them.** Nineteen signals is more than you can hold in your head.
7. **Check each gate as you wire it**, with the input switches, before starting the next one.
8. **Warm chip means stop.** Pull the power, check rule 2, then rule 4.

---

## Complete wire list

Written as *pin → pin*, never breadboard coordinates. `+` is the red rail, `−` is the blue
rail. Chips are named left to right as **CD4069, CD4070, CD4081 #1, CD4081 #2, CD4071 #1,
CD4071 #2** — put them in that order and the signal flow runs left to right.

### Power rails

| ✓ | From | To |
|---|---|---|
| ☐ | Supply + | Top red rail |
| ☐ | Supply − | Top blue rail |
| ☐ | Top red rail | Bottom red rail |
| ☐ | Top blue rail | Bottom blue rail |

### Chip power — do this before anything else

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | **pin 14** of all six chips | + | Six wires |
| ☐ | **pin 7** of all six chips | − | Six wires |
| ☐ | 0.1 µF ("104") | across each chip's pin 14 and pin 7 | Six capacitors |

### The three inputs — Stage 1

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | Three spare rows | call them **A**, **B**, **C** | A is 1, B is 2, C is 4 |
| ☐ | 100 kΩ | row A → − | Pull-down: unplugged reads 0, not nonsense |
| ☐ | 100 kΩ | row B → − | |
| ☐ | 100 kΩ | row C → − | |
| ☐ | Jumper in row A | free end → + or − | The A switch |
| ☐ | Jumper in row B | free end → + or − | The B switch |
| ☐ | Jumper in row C | free end → + or − | The C switch |
| ☐ | Row A | 1 kΩ → LED long leg, short leg to − | The A lamp |
| ☐ | Row B | 1 kΩ → LED long leg, short leg to − | The B lamp |
| ☐ | Row C | 1 kΩ → LED long leg, short leg to − | The C lamp |

### The display — common anode, Stage 1

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | Display pin 3 | + | Common anode |
| ☐ | Display pin 8 | + | Same node inside; wire both |
| ☐ | Each segment pin | its own 220 Ω into an empty row | Seven resistors. The gates arrive at the free ends |

### Unused inputs — every one of these goes to −

| ✓ | Chip | Pins | When |
|---|---|---|---|
| ☐ | CD4069 | 9, 11, 13 | End of Stage 2 |
| ☐ | CD4070 | 8, 9, 12, 13 | End of Stage 2 |
| ☐ | CD4081 #2 | 12, 13 | End of Stage 4 |
| ☐ | CD4071 #2 | 12, 13 | End of Stage 4 |

CD4081 #1 and CD4071 #1 are completely full — nothing to ground on those two.

### Stage 2 — the shared signals, and segments a, b, c

| ✓ | Gate | Chip | Gate no. | Inputs | Out | Meaning |
|---|---|---|:-:|---|:-:|---|
| ☐ | **B̅** | CD4069 | 1 | pin 1 ← row **B** | **2** | "B is 0" — four segments need it |
| ☐ | **C̅** | CD4069 | 2 | pin 3 ← row **C** | **4** | "C is 0" |
| ☐ | **A⊕C** | CD4070 | 1 | pin 1 ← row **A**<br>pin 2 ← row **C** | **3** | "A and C disagree" |
| ☐ | **A⊕B** | CD4070 | 2 | pin 5 ← row **A**<br>pin 6 ← row **B** | **4** | "A and B disagree" |
| ☐ | **a dark** | CD4081 #1 | 1 | pin 1 ← CD4069 pin 2 (B̅)<br>pin 2 ← CD4070 pin 3 (A⊕C) | **3** | drives segment **a** |
| ☐ | **b dark** | CD4081 #1 | 2 | pin 5 ← row **C**<br>pin 6 ← CD4070 pin 4 (A⊕B) | **4** | drives segment **b** |
| ☐ | **C+B̅** | CD4071 #1 | 1 | pin 1 ← row **C**<br>pin 2 ← CD4069 pin 2 (B̅) | **3** | first half of "c is lit" |
| ☐ | **c lit** | CD4071 #1 | 2 | pin 5 ← CD4071 #1 pin 3 (C+B̅)<br>pin 6 ← row **A** | **4** | true for every digit except 2 |
| ☐ | **c dark** | CD4069 | 3 | pin 5 ← CD4071 #1 pin 4 (c lit) | **6** | drives segment **c** |

| ✓ | Segment | From | Through | To |
|---|:-:|---|:-:|---|
| ☐ | **a** | CD4081 #1 pin 3 | 220 Ω | display pin 7 |
| ☐ | **b** | CD4081 #1 pin 4 | 220 Ω | display pin 6 |
| ☐ | **c** | CD4069 pin 6 | 220 Ω | display pin 4 |

### Stage 3 — segments d, e and g

| ✓ | Gate | Chip | Gate no. | Inputs | Out | Meaning |
|---|---|---|:-:|---|:-:|---|
| ☐ | **A·B** | CD4081 #1 | 3 | pin 8 ← row **A**<br>pin 9 ← row **B** | **10** | shared by f and by "is it 7" |
| ☐ | **is 7** | CD4081 #1 | 4 | pin 12 ← CD4081 #1 pin 10 (A·B)<br>pin 13 ← row **C** | **11** | A·B·C — used by d and g |
| ☐ | **d dark** | CD4071 #1 | 3 | pin 8 ← CD4081 #1 pin 3 (a dark)<br>pin 9 ← CD4081 #1 pin 11 (is 7) | **10** | drives segment **d** |
| ☐ | **B̅·C** | CD4081 #2 | 1 | pin 1 ← CD4069 pin 2 (B̅)<br>pin 2 ← row **C** | **3** | "the number is 4 or 5" |
| ☐ | **e dark** | CD4071 #1 | 4 | pin 12 ← row **A**<br>pin 13 ← CD4081 #2 pin 3 (B̅·C) | **11** | drives segment **e** |
| ☐ | **B̅·C̅** | CD4081 #2 | 2 | pin 5 ← CD4069 pin 2 (B̅)<br>pin 6 ← CD4069 pin 4 (C̅) | **4** | "the number is 0 or 1" |
| ☐ | **g dark** | CD4071 #2 | 1 | pin 1 ← CD4081 #2 pin 4 (B̅·C̅)<br>pin 2 ← CD4081 #1 pin 11 (is 7) | **3** | drives segment **g** |

| ✓ | Segment | From | Through | To |
|---|:-:|---|:-:|---|
| ☐ | **d** | CD4071 #1 pin 10 | 220 Ω | display pin 2 |
| ☐ | **e** | CD4071 #1 pin 11 | 220 Ω | display pin 1 |
| ☐ | **g** | CD4071 #2 pin 3 | 220 Ω | display pin 10 |

### Stage 4 — segment f

| ✓ | Gate | Chip | Gate no. | Inputs | Out | Meaning |
|---|---|---|:-:|---|:-:|---|
| ☐ | **A+B** | CD4071 #2 | 2 | pin 5 ← row **A**<br>pin 6 ← row **B** | **4** | first half of f |
| ☐ | **C̅+A·B** | CD4071 #2 | 3 | pin 8 ← CD4069 pin 4 (C̅)<br>pin 9 ← CD4081 #1 pin 10 (A·B) | **10** | second half of f |
| ☐ | **f dark** | CD4081 #2 | 3 | pin 8 ← CD4071 #2 pin 4 (A+B)<br>pin 9 ← CD4071 #2 pin 10 (C̅+A·B) | **10** | drives segment **f** |

| ✓ | Segment | From | Through | To |
|---|:-:|---|:-:|---|
| ☐ | **f** | CD4081 #2 pin 10 | 220 Ω | display pin 9 |

### The seven equations

| Segment | Dark for | Equation | Final gate | → display pin |
|:-:|:-:|---|---|:-:|
| **a** | 1, 4 | `a dark = B̅·(A⊕C)` | CD4081 #1 gate 1, pin 3 | 7 |
| **b** | 5, 6 | `b dark = C·(A⊕B)` | CD4081 #1 gate 2, pin 4 | 6 |
| **c** | 2 | `c dark = NOT(C + B̅ + A)` | CD4069 gate 3, pin 6 | 4 |
| **d** | 1, 4, 7 | `d dark = B̅·(A⊕C) + A·B·C` | CD4071 #1 gate 3, pin 10 | 2 |
| **e** | 1, 3, 4, 5, 7 | `e dark = A + B̅·C` | CD4071 #1 gate 4, pin 11 | 1 |
| **f** | 1, 2, 3, 7 | `f dark = (A + B)·(C̅ + A·B)` | CD4081 #2 gate 3, pin 10 | 9 |
| **g** | 0, 1, 7 | `g dark = B̅·C̅ + A·B·C` | CD4071 #2 gate 1, pin 3 | 10 |

### The font — three bits, eight digits

| Number | C | B | A | a | b | c | d | e | f | g | Bars lit |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| **0** | 0 | 0 | 0 | 1 | 1 | 1 | 1 | 1 | 1 | · | 6 |
| **1** | 0 | 0 | 1 | · | 1 | 1 | · | · | · | · | 2 |
| **2** | 0 | 1 | 0 | 1 | 1 | · | 1 | 1 | · | 1 | 5 |
| **3** | 0 | 1 | 1 | 1 | 1 | 1 | 1 | · | · | 1 | 5 |
| **4** | 1 | 0 | 0 | · | 1 | 1 | · | · | 1 | 1 | 4 |
| **5** | 1 | 0 | 1 | 1 | · | 1 | 1 | · | 1 | 1 | 5 |
| **6** | 1 | 1 | 0 | 1 | · | 1 | 1 | 1 | 1 | 1 | 6 |
| **7** | 1 | 1 | 1 | 1 | 1 | 1 | · | · | · | · | 3 |
Read the font table by column, not by row. The **a** column *is* the specification of segment
a: lit for 0, 2, 3, 5, 6, 7, dark for 1 and 4. That column is all segment a's three gates know
about the world.

**Display pin numbers assume the usual 10-pin arrangement** (1 = e, 2 = d, 3 = common, 4 = c,
5 = decimal point, 6 = b, 7 = a, 8 = common, 9 = f, 10 = g). Test yours — the procedure is in
the [worksheet](worksheet.md).

---

## Pin reference

Pin numbers verified against the Texas Instruments datasheets: CD4070B (SCHS055E), CD4071B
(SCHS056D), CD4081B (SCHS057C) and CD4069UB (SCHS054E).

```
CD4081 / CD4071 / CD4070    quad 2-input gates — one layout, three chips
  gate 1   in  1,  2  ->  OUT  3          + VDD on 14
  gate 2   in  5,  6  ->  OUT  4          − VSS on  7
  gate 3   in  8,  9  ->  OUT 10
  gate 4   in 12, 13  ->  OUT 11

CD4069   hex NOT                          + VDD on 14, − VSS on 7
  in  1 -> OUT  2      in 13 -> OUT 12
  in  3 -> OUT  4      in 11 -> OUT 10
  in  5 -> OUT  6      in  9 -> OUT  8

7-segment display, common anode, 10 pins (the usual arrangement — test yours)
  1 e    2 d    3 common    4 c    5 decimal point
  6 b    7 a    8 common    9 f   10 g
```

Gates 2 and 3 are numbered the other way up from gates 1 and 4 — output pin 4 sits *above*
input pin 5. That is the mistake everybody makes once.

### What each chip ends up holding

| Chip | Gates | Signals |
|---|:-:|---|
| CD4069 | 3 of 6 | B̅, C̅, **c dark** |
| CD4070 | 2 of 4 | A⊕C, A⊕B |
| CD4081 #1 | 4 of 4 | **a dark**, **b dark**, A·B, is 7 |
| CD4081 #2 | 3 of 4 | B̅·C, B̅·C̅, **f dark** |
| CD4071 #1 | 4 of 4 | C+B̅, c lit, **d dark**, **e dark** |
| CD4071 #2 | 3 of 4 | **g dark**, A+B, C̅+A·B |

Nineteen gates. Built without sharing anything it would take **twenty-nine** gates — eight
chips instead of six. The signal that earns the most is B̅: one inverter feeding four gates, and
its answer ends up inside five of the seven segments.

---

## Troubleshooting

| What you see | Almost always |
|---|---|
| One bar wrong for **exactly one** number | A wire on the wrong pin of the right gate. Output pins 3, 4, 10 and 11 are easy to confuse |
| One bar wrong for **four** numbers | An input is on the wrong row — A instead of B, or C instead of C̅ |
| One bar on for everything | Its gate input is floating, or the output is wired to + through something |
| One bar never lights | Prove the segment with the Stage 1 bare-wire test first. That halves the problem in ten seconds |
| **Every** bar is the photo-negative | The display common is on − instead of +. One wire, seven wrong bars |
| Digit changes when your hand moves near the board | A floating input. Eleven pins must go to − — see the table above |
| Everything is dim | Normal. About 1 mA a segment at 5 V. Run the board at 9 V if it bothers you |
| Two segments change together | Two outputs share a breadboard row. That is a short between two chips |
| A chip gets warm | Power backwards, or an output wired to a rail. **Unplug now** |
| Everything is wrong at once | Unplug, walk away five minutes, re-read one table. This is what real engineers do |

**The fastest way to find a gate fault.** Don't trace wires. Set the switches to a number that
comes out wrong, then walk that segment's chain and ask of each gate: *is this output what this
gate's own two inputs say it should be?* The first gate that disagrees with its own inputs is
the fault. Three checks, not nineteen.

**The fastest whole-board check.** Set 7: that is the only number where "is 7" is high, so it
tests the two gates that feed d and g. Then set 0: six bars on, g off. Two numbers cover most
of the board.

---

## Files

| File | What's in it |
|---|---|
| [`guide.html`](guide.html) | The illustrated guide: the derivations, four build stages, live simulator |
| [`worksheet.md`](worksheet.md) | The font to fill in, three equations to derive yourself, the challenges |
| `README.md` | This file — parts, wire lists, pinouts, troubleshooting |
