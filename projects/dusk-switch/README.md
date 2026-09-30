# The Dusk Switch

A lamp that comes on when it gets dark — and the project where you find out why that is harder
than it sounds.

Everything else in this box is told what to do by a switch: a thing that is 1 or 0 because a
finger says so. A photoresistor is not like that. It hands you 2.3 volts and walks away, and
somebody has to decide where 1 stops and 0 begins. Decide it carelessly and the lamp flickers at
dusk. This project builds it carelessly first, on purpose, so the fix means something.

**Open [`guide.html`](https://guddis.github.io/breadboard-lab/projects/dusk-switch/guide.html) in a browser** — that's the real guide, with diagrams and
a live simulator with a little scope in it. This file is the bench reference: parts, wire lists,
troubleshooting.

Do [the Gate Bench](../gate-bench/) first if you haven't: this project leans on "a NAND with its
inputs tied together is a NOT", and on the transistor from its bonus stage.

---

## What it teaches

| Idea | Where it shows up |
|---|---|
| **A sensor is a resistor that listens** — ohms in, nothing else | Section 2 |
| **The voltage divider**, and why every resistive sensor is read with one | Section 2 |
| **Choosing the fixed resistor *is* choosing the threshold** | Section 2, Stage 1 |
| **A null measurement** — reading your sensor's resistance with no multimeter | Stage 1 |
| **Every gate has a threshold**, and a noisy signal crossing it chatters | Section 3, Stage 2 |
| **Where noise actually comes from** — 100 Hz room light, a moving hand, a sagging supply | Section 3 |
| **Hysteresis**: two thresholds instead of one | Section 4, Stage 3 |
| **Reading a catalogue is engineering** — CD4093 instead of CD4011, same price, bug gone | Stage 3 |
| **Typical is not guaranteed** — 0.9 V typical, 0.3 V promised, 1.6 V permitted | Section 4 |
| **Positive feedback**, in a small enough dose to be useful | Stage 4 |
| **Too much hysteresis is a memory, not a switch** | Stage 4 |
| **Logic decides, transistors push** | Stage 5 |
| **The circuit has no idea what it is sensing** — swap in the thermistor | Bonus 1 |

About 2 hours in 5 stages. Stopping after Stage 3 leaves a working, reliable dusk switch.

---

## Parts

### Chips — one on the board at a time

| Chip | What it is | Used in |
|---|---|---|
| CD4011 | Quad 2-input NAND | Stages 2, 4, 5 |
| CD4093 | Quad 2-input NAND with **Schmitt-trigger inputs** | Stage 3 |

Identical pinouts. That is the whole point of Stage 3.

### Everything else

| Qty | Part | Notes |
|---|---|---|
| 1 | **Photoresistor** (LDR) | The sensor. Two legs, no polarity, either way round |
| 1 | LED, red or yellow | The indicator, all the way through |
| 1 | Resistor 1 kΩ | The indicator LED's resistor |
| 1 each | Resistor **1 k, 2 k, 5k1, 10 k, 100 k, 1 M** | Candidates for the fixed half of the divider |
| 1 | Resistor 10 kΩ | Stage 4 — R1, the input resistor |
| 1 each | Resistor **1 M, 100 k, 10 k** | Stage 4 — R2, three amounts of hysteresis |
| 1 | **PN2222** transistor | Stage 5 — the muscle |
| 1 | White LED **or** the active buzzer | Stage 5 — the thing worth switching on |
| 1 | Resistor 220 Ω | Stage 5 — the white LED's resistor |
| 1 | Resistor 10 kΩ | Stage 5 — into the base |
| 2 | Capacitor 0.1 µF (**104**) | One across the chip's power pins |
| 1 | **Thermistor** (optional) | The bonus. Same two holes, different machine |

### Power

3 AA cells (4.5 V) or a 5 V breadboard supply. A few milliamps until Stage 5. **Nothing in this
project goes near mains electricity.**

Every threshold here is a fraction of the supply, so a sagging battery moves the trip point. If
you leave it running in a shed for a month, expect it to switch a little earlier than it did on
day one.

---

## Rules for not breaking things

1. **Unplug the power before you swap the chip.** You will swap between the CD4011 and the
   CD4093 more than once, and a live swap is what kills chips.
2. **Both chips are + on 14 and − on 7.** And they are the same pinout as each other.
3. **Never leave an input dangling.** Unused inputs go to −.
4. **A NAND with its two inputs tied together is a NOT.** Used on every stage.
5. **Never wire an output to + or −.** Outputs drive gate inputs, LEDs through a resistor, or a
   base through a resistor.
6. **The transistor's legs are not interchangeable.** PN2222, flat face toward you, legs down:
   **E – B – C**.
7. **Warm chip means stop.** Pull the power, check rules 2 and 5.

---

## Complete wire list

Written as *pin → pin*, never breadboard coordinates. `+` is the red rail, `−` is the blue rail.
Two named rows do all the work: **S** is the divider's midpoint, and **X** (Stage 4 only) is the
input of your own Schmitt trigger.

### Stage 1 — the divider, no chips

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | Supply + | Top red rail | Power in |
| ☐ | Supply − | Top blue rail | Ground in |
| ☐ | + rail | One leg of the photoresistor | Sensor on top |
| ☐ | Other leg of the photoresistor | a spare row — call it **S** | The voltage you are making |
| ☐ | Row **S** | **10 kΩ** → − rail | The fixed half. This is the one you swap |
| ☐ | Row **S** | 1 kΩ → LED long leg, short leg to − | A rough meter, for this stage only |

### Stage 2 — one gate (CD4011)

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | **pin 14** | + | Power |
| ☐ | **pin 7** | − | Ground |
| ☐ | 0.1 µF ("104") | pin 14 → pin 7 | Local smoothing |
| ☐ | Row **S** | pin 1 **and** pin 2 | Both inputs of gate 1 — so it acts as a NOT |
| ☐ | pin 3 | 1 kΩ → LED long leg, short leg to − | Move the LED here from row S |
| ☐ | pins 5, 6, 8, 9, 12, 13 | − | The three spare gates' inputs |

### Stage 3 — the swap

Power off. CD4011 out, **CD4093** in, notch the same way round. **Change nothing else.**

### Stage 4 — your own Schmitt trigger (CD4011 back in)

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | Remove the wire from row **S** to pins 1 and 2 | | A resistor takes its place |
| ☐ | **R1** = 10 kΩ | row **S** → row **X** | The sensor pulls on X through a resistor |
| ☐ | Row **X** | pin 1 **and** pin 2 | Gate 1, still a NOT |
| ☐ | pin 3 | pin 5 **and** pin 6 | Gate 2, the second NOT |
| ☐ | **R2** = 100 kΩ | pin 4 → row **X** | **The feedback.** This one resistor is the stage |
| ☐ | pin 4 | pin 8 **and** pin 9 | Gate 3, the lamp's buffer |
| ☐ | pin 10 | 1 kΩ → LED long leg, short leg to − | The LED moves off pin 3 |
| ☐ | pins 12, 13 | − | The last spare gate |

The LED has to move to a third gate: a CD4011 output cannot light an LED *and* hold a gate input
at a valid high at the same time — it sags to about two volts and the next gate can't read it.

### Stage 5 — the transistor

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | Output pin (**10** after Stage 4, **3** before it) | 10 kΩ → PN2222 **base** (middle leg) | About 0.4 mA — all the chip can spare |
| ☐ | PN2222 **emitter** (left leg) | − rail | |
| ☐ | + rail | 220 Ω → white LED long leg | Current off the rail, not out of the chip |
| ☐ | White LED short leg | PN2222 **collector** (right leg) | |

Swap the white LED for the **active buzzer** and it is a drawer alarm instead of a nightlight.

---

## Choosing the fixed resistor

This is the design decision of the whole project. The rule is simple: **the divider's midpoint
arrives when the sensor's resistance equals the fixed resistor's.** So the fixed resistor decides
how dark it has to get.

| Fixed resistor | Lamp on when the sensor rises past | Off again below | Which is about |
|---|:-:|:-:|---|
| **1 kΩ** | 1.6 kΩ | 0.7 kΩ | a torch pointed at it |
| **2 kΩ** | 3.3 kΩ | 1.4 kΩ | an ordinary lit room |
| **5k1** | 8.3 kΩ | 3.7 kΩ | an ordinary lit room |
| **10 kΩ** | 16 kΩ | 7.2 kΩ | an ordinary lit room |
| **100 kΩ** | 163 kΩ | 72 kΩ | curtains shut, lights off |
| **1 MΩ** | 1.6 MΩ | 724 kΩ | a shut drawer |

| R2 (feedback) | Gap = 5 V × R1/R2 | Against 100 mV of noise | What you see |
|---|:-:|---|---|
| **1 MΩ** | **0.05 V** | about the same size | Clean sometimes, flickers other times |
| **100 kΩ** | **0.50 V** | comfortably clear | One clean switch, every time |
| **10 kΩ** | **5.00 V** | wider than the supply | On for ever — a memory, not a switch |
Both tables above are worked out from the CD4093's *typical* thresholds on a 5 V supply. Your
photoresistor is not the one those numbers assume — Stage 1 is how you find yours, and the
worksheet has the table to write it in.

---

## Pin reference

Verified against the Texas Instruments datasheets: **CD4093B (SCHS115D)** and **CD4011B
(SCHS021D)**.

```
CD4011  quad 2-input NAND                 ** + on 14, − on 7 **
CD4093  quad 2-input NAND, Schmitt        ** identical pinout **
  gate 1   in  1,  2  ->  OUT  3
  gate 2   in  5,  6  ->  OUT  4
  gate 3   in  8,  9  ->  OUT 10
  gate 4   in 12, 13  ->  OUT 11

  Tie a gate's two inputs together and it is a NOT.

PN2222  NPN transistor — flat face toward you, legs down
  E   B   C
  |   |   +--- the lamp (and the lamp's other end to +, via 220 Ω)
  |   +------- 10 kΩ from the gate output
  +----------- − rail

Photoresistor / thermistor — two legs, no polarity, either way round.
```

### The CD4093's numbers, at 5 V

| | min | typ | max |
|---|:-:|:-:|:-:|
| V<sub>P</sub> — trips going up | 2.2 | **2.9** | 3.6 |
| V<sub>N</sub> — trips coming down | 0.9 | **1.9** | 2.8 |
| V<sub>H</sub> — the gap | 0.3 | **0.9** | 1.6 |

Volts. **Read the min column.** Typical is 0.9 V but the datasheet only promises 0.3 V and
permits 1.6 V, so the chip in your hand is somewhere in a five-to-one range and you do not get to
know where. That is the argument for Stage 4, where the gap is `5 V × R1 / R2` and you choose it.

The front page is worth reading too — *"Schmitt-trigger action on each input with no external
components"*, and *"no limit on input rise and fall times"*, which is exactly the promise you need
when the input is the sunset.

---

## Troubleshooting

| What you see | Almost always |
|---|---|
| **Lamp always on**, whatever the light | Fixed resistor too big — the circuit thinks it is always dark. Go down a value. After Stage 4, also suspect R2 = 10 kΩ: that latches |
| **Lamp always off**, whatever the light | Fixed resistor too small. Go up a value, and cover the sensor *completely* when you test |
| Switches, but at the wrong light level | That is the fixed resistor's job. Tuning, not a fault |
| Flickers at the crossing | The CD4011 with no feedback resistor — Stage 2 working correctly. Stage 3 or 4 fixes it |
| Flickers **sometimes** | Not enough hysteresis for your noise. R2 too big: 1 MΩ → 100 kΩ |
| Goes on and never comes off | Too much hysteresis. R2 is close to R1 and it has become a latch |
| Indicator LED feeble | Normal — about 1 mA out of a CD4000. Stage 5 is the cure |
| White LED dark but the indicator works | Transistor in backwards, or the LED is. Flat face toward you: E – B – C |
| Blinks steadily and won't stop | Your lamp is shining on your sensor. Turn it away — or keep it, and read the end of Stage 5 |
| Everything changes when you touch the board | A floating input, or your finger is acting as the sensor. Spare gate inputs to − |
| A chip gets warm | Power backwards, or an output wired to a rail. **Unplug now** |

**The fastest way to split this circuit in half.** Put an LED straight on row **S** through
1 kΩ, exactly as in Stage 1. If it responds to light, the sensor half is fine and the fault is in
the gates. If it doesn't, stop looking at the chip.

---

## Files

| File | What's in it |
|---|---|
| [`guide.html`](guide.html) | The illustrated guide: five stages, the hysteresis figures, a simulator with a scope |
| [`worksheet.md`](worksheet.md) | Measure your own sensor, count the flickers, choose your own hysteresis |
| `README.md` | This file — parts, wire lists, pinouts, troubleshooting |
