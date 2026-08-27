# The Logic Vault

A combination safe with no computer inside it — just logic gates.

You set a secret 4-bit code with four hidden jumper wires. Someone else has to find it
using four dials. Get all four right and the green light comes on and the vault lights up.
Press **OPEN** with the wrong code and a buzzer screams.

Built for a curious 12-year-old, using nothing but CD4000-series logic chips, a breadboard
and a handful of LEDs.

**Open [`guide.html`](https://guddis.github.io/breadboard-lab/projects/logic-vault/guide.html) in a browser** — that's the real guide, with diagrams and a
working simulator you can play with before you build anything. This file is the bench
reference: parts, wire lists, troubleshooting.

---

## What it teaches

| Idea | Where it shows up |
|---|---|
| A wire is either 1 or 0 (voltage or no voltage) | Every dial |
| NOT, AND, OR, XOR, XNOR | Stages 1–3, one chip each |
| XNOR is a **comparator** — "are these two the same?" | Stage 3, the key insight |
| Four comparators + one AND = a 4-bit comparator | Stage 4–5 |
| A NAND gate with its inputs tied together becomes a NOT gate | Stage 5, the free inverter |
| Logic chips can *think* but not *push* — transistors do the muscle | Stage 5, output block |
| Fan-out and loading: why you can't hang lights on every wire | Sidebar |
| Side channels: helpful lights can leak the secret | Stage 7 |

Total build time is about 2–3 hours, in seven stages you can stop between.

---

## Parts

Everything here is in the kit. Quantities are what the finished vault needs.

### Chips

| Chip | What it is | Job in the vault |
|---|---|---|
| CD4077 | Quad 2-input XNOR | The four "does this dial match?" detectors |
| CD4012 | Dual 4-input NAND | The judge, plus a free inverter |
| CD4081 | Quad 2-input AND | Arms the alarm |

Stages 1–3 also borrow **CD4069** (hex NOT), **CD4071** (quad OR) and **CD4070** (quad XOR)
for the gate experiments. They come back out afterwards.

### Everything else

| Qty | Part | Notes |
|---|---|---|
| 3 | PN2222 NPN transistor | Flat side toward you, legs down: **E – B – C** |
| 1 | Active buzzer | The kind that beeps on its own from DC |
| 1 | Red LED | LOCKED |
| 1 | Green LED | UNLOCKED |
| 2 | White LED | Vault lights |
| 4 | Yellow LED | Stage 4 only — the match lights, removed afterwards |
| 1 | Push button (small) | OPEN |
| 4 + 4 | 220 Ω resistor | LED current limit (4 permanent, 4 for stage 4) |
| 2 | 10 kΩ resistor | Q1 base, button pull-down |
| 2 | 5.1 kΩ resistor | Q2 and Q3 bases |
| 3 | 0.1 µF ceramic ("104") | One across each chip's power pins |
| 1 | 100 µF electrolytic | Across the power rails — **stripe goes to −** |
| 1 | Breadboard | Half-size is enough; full-size is comfier |
| ~35 | Jumper wires | Red for +, black for −, colours for signals |

### Power

**4.5 V to 5 V.** Either three AA cells, or the MB102 breadboard power module set to 5 V.

These chips are happy anywhere from 3 V to 18 V, so nothing here is fragile about voltage.
Nothing in this project touches mains electricity.

---

## Rules for not breaking things

1. **Unplug the power before you rewire.** Every time.
2. **The notch on a chip tells you which end is which.** Notch on the left → pin 1 is
   bottom-left, and pin numbers run anticlockwise. Put a chip in backwards and pin 14 gets
   ground while pin 7 gets +5 V; the chip gets hot and dies.
3. **Never leave an input wire dangling.** A CMOS input that is connected to nothing
   picks up radio noise and flickers randomly. Every input goes to + or to − or to another
   chip's output. Unused inputs go to −.
4. **Never wire an output straight to + or −.** That's a short circuit through the chip.
5. **The electrolytic capacitor has a polarity.** The stripe down one side marks the
   negative leg. Backwards, it can pop.
6. **Touch something metal and grounded before you pick up a chip.** Static kills CMOS.
7. If a chip ever feels **warm**, pull the power immediately and check the wiring.

---

## Complete wire list

Everything is written as *chip pin → chip pin*, never as breadboard coordinates, so it
works no matter where you place things. `+` means the red rail, `−` means the blue/black rail.

### Power rails

| ✓ | From | To |
|---|---|---|
| ☐ | Supply + | Top red rail |
| ☐ | Supply − | Top blue rail |
| ☐ | Top red rail | Bottom red rail |
| ☐ | Top blue rail | Bottom blue rail |
| ☐ | 100 µF + leg | Red rail (stripe/− leg to blue rail) |

### CD4077 — the four match detectors

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | pin 14 | + | Power |
| ☐ | pin 7 | − | Ground |
| ☐ | 0.1 µF | between pin 14 and pin 7 | Local smoothing |
| ☐ | DIAL 1 jumper | pin 1 | Free end plugs into + or − |
| ☐ | SECRET 1 jumper | pin 2 | Free end plugs into + or − |
| ☐ | DIAL 2 jumper | pin 5 | |
| ☐ | SECRET 2 jumper | pin 6 | |
| ☐ | DIAL 3 jumper | pin 8 | |
| ☐ | SECRET 3 jumper | pin 9 | |
| ☐ | DIAL 4 jumper | pin 12 | |
| ☐ | SECRET 4 jumper | pin 13 | |

Outputs, which you wire in the next block: pin 3 = MATCH 1, pin 4 = MATCH 2,
pin 10 = MATCH 3, pin 11 = MATCH 4.

### CD4012 — the judge

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | pin 14 | + | Power |
| ☐ | pin 7 | − | Ground |
| ☐ | 0.1 µF | between pin 14 and pin 7 | |
| ☐ | CD4077 pin 3 | CD4012 pin 2 | MATCH 1 in |
| ☐ | CD4077 pin 4 | CD4012 pin 3 | MATCH 2 in |
| ☐ | CD4077 pin 10 | CD4012 pin 4 | MATCH 3 in |
| ☐ | CD4077 pin 11 | CD4012 pin 5 | MATCH 4 in |
| ☐ | CD4012 pin 1 | CD4012 pin 9 | LOCKED into the free inverter |
| ☐ | CD4012 pin 1 | CD4012 pin 10 | |
| ☐ | CD4012 pin 1 | CD4012 pin 11 | |
| ☐ | CD4012 pin 1 | CD4012 pin 12 | |

Pins 6 and 8 are "no connection" — leave them empty.
Outputs: **pin 1 = LOCKED**, **pin 13 = UNLOCKED**.

### CD4081 — arms the alarm

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | pin 14 | + | Power |
| ☐ | pin 7 | − | Ground |
| ☐ | 0.1 µF | between pin 14 and pin 7 | |
| ☐ | CD4012 pin 1 | CD4081 pin 1 | LOCKED |
| ☐ | OPEN node | CD4081 pin 2 | Button |
| ☐ | pins 5, 6, 8, 9, 12, 13 | − | Unused inputs, all to ground |

Output: **pin 3 = ALARM**. Leave pins 4, 10 and 11 unconnected.

### OPEN button

| ✓ | From | To |
|---|---|---|
| ☐ | Button leg | + |
| ☐ | Button leg, **diagonally opposite** | OPEN node |
| ☐ | OPEN node | 10 kΩ → − |
| ☐ | OPEN node | CD4081 pin 2 |

A 4-pin tactile button has its legs joined in pairs. Using diagonally opposite legs is
the one choice that is always right.

### Output block — Q1, the red LOCKED light

| ✓ | From | To |
|---|---|---|
| ☐ | CD4012 pin 1 | 10 kΩ → Q1 base (middle leg) |
| ☐ | Q1 emitter (left leg) | − |
| ☐ | + | 220 Ω → red LED long leg |
| ☐ | Red LED short leg | Q1 collector (right leg) |

### Output block — Q2, the green light and the vault lights

| ✓ | From | To |
|---|---|---|
| ☐ | CD4012 pin 13 | 5.1 kΩ → Q2 base |
| ☐ | Q2 emitter | − |
| ☐ | + | 220 Ω → green LED long leg |
| ☐ | Green LED short leg | Q2 collector |
| ☐ | + | 220 Ω → white LED 1 long leg |
| ☐ | White LED 1 short leg | Q2 collector |
| ☐ | + | 220 Ω → white LED 2 long leg |
| ☐ | White LED 2 short leg | Q2 collector |

### Output block — Q3, the alarm

| ✓ | From | To |
|---|---|---|
| ☐ | CD4081 pin 3 | 5.1 kΩ → Q3 base |
| ☐ | Q3 emitter | − |
| ☐ | Buzzer + (long leg) | + |
| ☐ | Buzzer − | Q3 collector |

Q1 gets a 10 kΩ base resistor because the LOCKED wire also has to talk to two chips, and
a smaller resistor would drag its voltage down too far to count as a clean 1. Q2 and Q3
drive nothing but their own transistor, so they can afford the 5.1 kΩ that makes those
outputs brighter and louder.

---

## Pin reference

All five verified against the Texas Instruments datasheets. Pin 14 is always +, pin 7 is
always −, on every chip here.

```
CD4077  quad XNOR          CD4012  dual 4-input NAND
 in 1,  2  -> out  3        in 2, 3, 4, 5  -> out  1
 in 5,  6  -> out  4        in 9,10,11,12  -> out 13
 in 8,  9  -> out 10        pins 6 and 8: no connection
 in 12,13  -> out 11

CD4081  quad AND           CD4071  quad OR
 in 1,  2  -> out  3        in 1,  2  -> out  3
 in 5,  6  -> out  4        in 5,  6  -> out  4
 in 8,  9  -> out 10        in 8,  9  -> out 10
 in 12,13  -> out 11        in 12,13  -> out 11

CD4070  quad XOR           CD4069  hex NOT
 in 1,  2  -> out  3        in  1 -> out  2
 in 5,  6  -> out  4        in  3 -> out  4
 in 8,  9  -> out 10        in  5 -> out  6
 in 12,13  -> out 11        in  9 -> out  8
                            in 11 -> out 10
                            in 13 -> out 12
```

CD4077, CD4081, CD4071 and CD4070 all share the same pin layout. Learn it once.

---

## Troubleshooting

| What you see | Almost always |
|---|---|
| Nothing lights at all | Power not reaching pin 14 / pin 7 on a chip. Check both, on every chip. |
| A chip gets warm | Power in backwards. Unplug now. Notch to the left, pin 14 top-left. |
| Lights flicker or change on their own | An input is floating. Find the input with nothing on it and tie it to −. |
| Green never comes on | One MATCH wire is on the wrong CD4012 pin. Inputs are 2, 3, 4, 5 — not 1. |
| Green is always on | The four jumpers from CD4012 pin 1 to pins 9–12 are missing or on wrong pins. |
| LEDs very dim in stages 1–4 | Normal. These chips only push about 3 mA. Stage 5 adds transistors and real brightness. |
| An LED never lights | Backwards. Long leg toward +, short leg toward −. |
| Buzzer silent, alarm LED logic fine | Buzzer polarity, or a passive buzzer instead of the active one. |
| Buzzer always on | CD4081 pin 2 is floating — the button pull-down resistor is missing. |
| Everything is wrong at once | Unplug, walk away for five minutes, come back and re-read one table. This is what real engineers do. |

---

## Files

| File | What's in it |
|---|---|
| [`guide.html`](guide.html) | The illustrated guide: diagrams, seven build stages, live simulator |
| [`worksheet.md`](worksheet.md) | Truth tables to fill in by hand, and the code-cracking challenges |
| `README.md` | This file — parts, wire lists, pinouts, troubleshooting |
