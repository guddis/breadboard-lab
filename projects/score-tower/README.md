# The Score Tower

A scoreboard that shows a real number — press the button and an actual **7** appears, not a
row of lights you have to count.

Nine more presses and a second digit wakes up to keep the tens, so it counts to 99. RESET
wipes it, HOLD freezes it, BLANK hides it while it keeps counting in the dark.

**Open [`guide.html`](https://guddis.github.io/breadboard-lab/projects/score-tower/guide.html) in a browser** — that's the real guide, with diagrams and a
working simulator. This file is the bench reference: parts, wire lists, troubleshooting.

---

## What it teaches

| Idea | Where it shows up |
|---|---|
| **Decoding** — turning a count into seven separate yes/no answers | The CD4026's seven segment outputs |
| **The seven-segment font** — why a 9 has no bottom bar | Section 2, and your display |
| **Polarity mismatch** — a chip that drives the wrong way round | Fourteen inverters that shouldn't be needed |
| **Debouncing** — one press must mean one count | Stage 3, one resistor and one capacitor |
| **Schmitt-trigger inputs** — why a sagging edge is legal | Why Stage 3 needs no extra chip |
| **Carry** — the thing you learnt at seven years old, as one wire | Stage 5, CD4026 pin 5 |
| **Overflow** — what comes after 99 | Stage 5, the end |
| **Idempotence** — why RESET needs no debounce | Stage 4 |

Total build time is about 2½ hours, in 5 stages you can stop between. Stopping after Stage 4
leaves a working scoreboard that counts to 9.

---

## Parts

### Chips

| Chip | What it is | Job |
|---|---|---|
| CD4026 × 2 | Decade counter + 7-segment decoder, **16 pins** | One per digit: counts, and works out the seven bars |
| CD4069 × 3 | Hex NOT | Fourteen of its eighteen inverters flip the segment signals for the common-anode displays |

### Everything else

| Qty | Part | Notes |
|---|---|---|
| 2 | 7-segment display, **common anode** | Use the red ones — white needs 3 V a segment and looks dimmer |
| 14 | Resistor 220 Ω | One per segment. 330 Ω is fine too; mix them freely |
| 2 | Resistor 100 kΩ | Clock pull-up, RESET pull-down |
| 2 | Resistor 100 kΩ | Only if you fit HOLD and BLANK buttons |
| 1 | Capacitor 0.1 µF (**104**) | The debounce |
| 5 | Capacitor 0.1 µF (**104**) | One across each chip's power pins |
| 2–4 | Push buttons | COUNT and RESET; add HOLD and BLANK if you want them |
| — | Hook-up wire | A lot of it. Fourteen segment runs alone |

### Power

3 AA cells (4.5 V) or a 5 V breadboard supply. **Nothing in this project goes near mains
electricity.** Both digits showing 88 draws about 40 mA, which three AAs will run for days.

---

## Rules for not breaking things

1. **Unplug the power before you rewire.** Every time.
2. **The notch on a chip tells you which end is which.** Notch up → pin 1 to its left, numbers
   run anticlockwise.
3. **The CD4026 is a 16-pin chip: + on 16, − on 8.** Every other chip in this box is 14-pin
   with + on 14 and − on 7. Your hands will go there out of habit. On a CD4026, pin 14 is the
   UNGATED C output and 5 V into it is a short through the chip.
4. **Never leave an input dangling.** Unused CD4069 inputs go to −. On the CD4026, pin 2 goes
   to − and **pin 3 goes to +**.
5. **Never wire an output straight to + or −.** The segment outputs go to inverter inputs and
   nowhere else.
6. **Every segment gets its own resistor.** One resistor in the common pin makes every digit a
   different brightness.
7. **Electrolytic capacitors have a polarity.** The 104s here don't, so nothing to get wrong.
8. **Touch something grounded before handling chips.** Static kills CMOS.
9. **Warm chip means stop.** Pull power, check rule 2 and rule 3.

---

## Complete wire list

Written as *pin → pin*, never breadboard coordinates, so it works wherever you put things.
`+` is the red rail, `−` is the blue rail.

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
| ☐ | CD4026 #1 **pin 16** | + | Power. **16, not 14** |
| ☐ | CD4026 #1 **pin 8** | − | Ground. **8, not 7** |
| ☐ | CD4069 #1 pin 14 | + | Power |
| ☐ | CD4069 #1 pin 7 | − | Ground |
| ☐ | CD4069 #2 pin 14 | + | Power |
| ☐ | CD4069 #2 pin 7 | − | Ground |
| ☐ | 0.1 µF ("104") | across each chip's + and − pins | Local smoothing, one per chip |

### The display — common anode

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | Display pin 3 | + | Common anode |
| ☐ | Display pin 8 | + | Same node inside; wire both |

### CD4026 #1 — the units digit

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | pin 3 | **+** | DISPLAY ENABLE IN. Low here = dead display |
| ☐ | pin 2 | − | CLOCK INHIBIT off |
| ☐ | pin 15 | − | RESET off (a button replaces this in Stage 4) |
| ☐ | 100 kΩ | pin 1 → **+** | Clock pull-up |
| ☐ | 0.1 µF ("104") | pin 1 → − | The debounce capacitor |
| ☐ | Button | pin 1 → − | COUNT. Counts on release |
| ☐ | pin 4 | leave empty | DISPLAY ENABLE OUT, unused |
| ☐ | pin 14 | leave empty | UNGATED C, unused |
| ☐ | pin 5 | leave empty until Stage 5 | CARRY OUT |

### The seven segments — units digit

Each row is the same shape: *counter out → inverter in*, then *inverter out → 220 Ω →
display*.

| ✓ | Seg | CD4026 #1 out | → inverter in | inverter out → | → 220 Ω → display |
|---|---|---|---|---|---|
| ☐ | **a** | pin 10 | CD4069 #1 pin 1 | CD4069 #1 pin 2 | display pin 7 |
| ☐ | **b** | pin 12 | CD4069 #1 pin 3 | CD4069 #1 pin 4 | display pin 6 |
| ☐ | **c** | pin 13 | CD4069 #1 pin 5 | CD4069 #1 pin 6 | display pin 4 |
| ☐ | **d** | pin 9 | CD4069 #1 pin 9 | CD4069 #1 pin 8 | display pin 2 |
| ☐ | **e** | pin 11 | CD4069 #1 pin 11 | CD4069 #1 pin 10 | display pin 1 |
| ☐ | **f** | pin 6 | CD4069 #1 pin 13 | CD4069 #1 pin 12 | display pin 9 |
| ☐ | **g** | pin 7 | CD4069 #2 pin 1 | CD4069 #2 pin 2 | display pin 10 |

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | CD4069 #2 pins 5, 9, 11, 13 | − | Unused inputs. Pin 3 is the tens digit's g in Stage 5 |

**Display pin numbers assume the usual 10-pin arrangement** (1 = e, 2 = d, 3 = common,
4 = c, 5 = decimal point, 6 = b, 7 = a, 8 = common, 9 = f, 10 = g). Test yours first — the
procedure is in the guide, the table to fill in is in the worksheet.

### The three control buttons — Stage 4

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | 100 kΩ | pin 15 → − | RESET pull-down, replacing the plain wire |
| ☐ | Button | pin 15 → **+** | RESET. No capacitor needed — see below |
| ☐ | 100 kΩ | pin 2 → − | HOLD pull-down, replacing the plain wire |
| ☐ | Button | pin 2 → **+** | HOLD. Ignores the clock while held |
| ☐ | 100 kΩ | pin 3 → **+** | BLANK pull-up, replacing the plain wire |
| ☐ | Button | pin 3 → − | BLANK. All segments off, count keeps running |

RESET needs no debounce capacitor: bouncing it just resets to zero several times, and zero
several times is still zero.

### CD4026 #2 and CD4069 #3 — the tens digit, Stage 5

Wire the second digit exactly like the first, with these differences:

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | CD4026 #1 **pin 5** | CD4026 #2 **pin 1** | **The carry.** One pulse per ten counts |
| ☐ | CD4026 #2 pin 16 / pin 8 | + / − | Power. 16 and 8 again |
| ☐ | CD4026 #2 pin 3 | + | DISPLAY ENABLE IN |
| ☐ | CD4026 #2 pin 2 | − | CLOCK INHIBIT off |
| ☐ | CD4026 #2 pin 15 | the **same** node as the RESET button | One button must zero both digits |
| ☐ | CD4069 #3 pin 14 / pin 7 | + / − | Power |
| ☐ | Segments **a**–**f** | CD4069 **#3**, same pin pattern as the table above | Second digit's inverters |
| ☐ | Segment **g** | CD4026 #2 pin 7 → CD4069 #2 **pin 3**, out on **pin 4** | The shared spare inverter |
| ☐ | CD4069 #2 pins 5, 9, 11, 13 | − | Still unused |
| ☐ | Display #2 pins 3 and 8 | + | Common anode |

There is no hundreds digit. After 99 the display goes to 00 without warning — that's
overflow, and it is the point of the last section of the guide.

---

## Pin reference

Verified against the manufacturer's datasheets: TI CD4026B (SCHS031B) and CD4069UB
(SCHS054E).

```
CD4026   decade counter + 7-segment decoder      ** 16 PINS: + on 16, − on 8 **
  1 CLOCK              16 + VDD
  2 clock inhibit      15 RESET            (high = count held at 0)
  3 display enable in  14 ungated c  OUT
  4 disp. en. out OUT  13 seg c      OUT
  5 CARRY OUT     OUT  12 seg b      OUT
  6 seg f         OUT  11 seg e      OUT
  7 seg g         OUT  10 seg a      OUT
  8 − VSS               9 seg d      OUT

CD4069   hex NOT                                 ** 14 pins: + on 14, − on 7 **
  in  1 -> OUT  2      in 13 -> OUT 12
  in  3 -> OUT  4      in 11 -> OUT 10
  in  5 -> OUT  6      in  9 -> OUT  8

7-segment display, common anode, 10 pins (the usual arrangement — test yours)
  1 e    2 d    3 common    4 c    5 decimal point
  6 b    7 a    8 common    9 f   10 g
```

### The font the CD4026 draws

Read off the timing diagram on page 3 of the datasheet. Note that **6 keeps its top bar** and
**9 has no bottom bar**.

| Digit | a | b | c | d | e | f | g | bars |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0 | 1 | 1 | 1 | 1 | 1 | 1 | 0 | 6 |
| 1 | 0 | 1 | 1 | 0 | 0 | 0 | 0 | 2 |
| 2 | 1 | 1 | 0 | 1 | 1 | 0 | 1 | 5 |
| 3 | 1 | 1 | 1 | 1 | 0 | 0 | 1 | 5 |
| 4 | 0 | 1 | 1 | 0 | 0 | 1 | 1 | 4 |
| 5 | 1 | 0 | 1 | 1 | 0 | 1 | 1 | 5 |
| 6 | 1 | 0 | 1 | 1 | 1 | 1 | 1 | 6 |
| 7 | 1 | 1 | 1 | 0 | 0 | 0 | 0 | 3 |
| 8 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 7 |
| 9 | 1 | 1 | 1 | 0 | 0 | 1 | 1 | 5 |

CARRY OUT (pin 5) is **high for counts 0–4 and low for 5–9**, so its rising edge lands exactly
on 9 → 0. That is why wiring it straight to the next digit's CLOCK gives the right answer.

---

## Troubleshooting

| What you see | Almost always |
|---|---|
| Display completely dead, chip cool | **Pin 3 is not at +.** The most common fault in this project |
| Digits look like photo-negatives | A segment skips its inverter. Count the wrong bars — that's how many wires to recheck |
| One bar never lights | Resistor, inverter output, or segment pin. Probe the segment by hand first |
| One bar never goes off | Its inverter input is floating |
| Jumps 2–3 per press | Bounce. Capacitor missing, in the wrong row, or a 22 pF instead of a 104 |
| Counts randomly | The 100 kΩ still goes to − instead of + |
| Never leaves 0 | Pin 15 is high — stuck RESET button or missing pull-down |
| Stuck, button does nothing | Pin 2 is high. HOLD is on |
| Tens digit ticks at the wrong time | Carry went to the tens chip's pin 2 instead of pin 1 |
| A chip gets warm | Power in backwards — on a CD4026, + on 14 instead of 16. **Unplug now** |
| Everything is wrong at once | Unplug, walk away five minutes, re-read one table. This is what real engineers do |

**The fastest segment check:** hold RESET so the display shows 0 — that lights six bars and
leaves g dark. Then count to 8: all seven on. Two numbers test the whole display.

---

## Files

| File | What's in it |
|---|---|
| [`guide.html`](guide.html) | The illustrated guide: diagrams, build stages, simulator |
| [`worksheet.md`](worksheet.md) | The display test table, the font to fill in, the challenges |
| `README.md` | This file — parts, wire lists, pinouts, troubleshooting |
