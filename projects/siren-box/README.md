# The Siren Box

A blinking LED and a musical note are the same circuit. The only difference is how fast.

Four buttons give four notes. A photoresistor lets you bend the pitch with your hand. Two
jumpers put a second and third oscillator in charge of the first, and the box turns into a
police siren, an alarm clock, or an ambulance.

Built for a curious 10-to-12-year-old, using two CD4000-series chips, two transistors and
one buzzer.

**Open [`guide.html`](https://guddis.github.io/breadboard-lab/projects/siren-box/guide.html) in a browser** — that's the real guide, and the box is
playable on the page, with sound, before you build anything. This file is the bench
reference: parts, wire lists, troubleshooting.

---

## What it teaches

| Idea | Where it shows up |
|---|---|
| A note and a blink are one circuit at two speeds | Stage 1 |
| Frequency is set by R × C, and you can predict it | Stage 1, worksheet |
| A chip's output has its own hidden resistance — about 1 kΩ | Stage 2, worksheet |
| Resistors in parallel: more paths, less resistance, higher pitch | Stage 2 |
| A sensor can *be* a circuit component, not just something you read | Stage 3 |
| Deliberate limits: a floor resistor stops a circuit leaving its safe range | Stage 3 |
| Resonance — why one note is louder than all the others | Section 2 |
| An oscillator's output is just a signal, so it can control another oscillator | Stage 4 |
| Frequency modulation — the idea behind FM radio | Stage 4 |
| An analog switch is a wire you can turn off, and is not a gate | Section 3, Stage 4 |
| Two transistors in series make an AND for power | Stage 5 |
| Active and passive buzzers are not the same part | Bonus |

Total build time is about 1½–2 hours, in five stages you can stop between.

---

## Parts

### Chips

| Chip | What it is | Job in the box |
|---|---|---|
| CD40106 | Hex Schmitt-trigger inverter | All three oscillators: sound, wail and chop |
| CD4066 | Quad analog switch | Switches the second timing resistor in and out |

### Everything else

| Qty | Part | Notes |
|---|---|---|
| 1 | **Passive** buzzer | The one that is silent on plain DC. **Not** the active one |
| 2 | PN2222 NPN transistor | Flat side toward you, legs down: **E – B – C** |
| 1 | Photoresistor | The theremin |
| 4 | Push button (small) | The four notes |
| 1 | 100 Ω resistor | In series with the buzzer — **not optional**, see below |
| 2 | 1 kΩ resistor | Top note, and the photoresistor's floor |
| 1 | 2 kΩ resistor | Note 3 |
| 1 | 5.1 kΩ resistor | Note 2 |
| 6 | 10 kΩ resistor | Note 1, siren resistor, chop timing, two transistor bases, one pull-down |
| 1 | 100 kΩ resistor | Wail timing |
| 1 | 1 MΩ resistor | The bleed resistor that keeps the audio input from floating |
| 3 | 0.1 µF ceramic ("104") | One per chip across its power pins, plus the audio timing capacitor |
| 2 | 10 µF electrolytic | Wail and chop timing — **stripe goes to −** |
| 1 | 100 µF electrolytic | Across the power rails — **stripe goes to −** |
| 1 | Breadboard | Half-size is enough |
| ~30 | Jumper wires | Red for +, black for −, colours for signals |

### The 100 Ω resistor

Some passive buzzers are a coil of wire measuring about 16 Ω. Straight across 5 V that is a
third of an amp, which will cook the transistor and flatten your batteries. The 100 Ω holds
it to a sensible 40 mA.

If yours is too quiet, try the 10 Ω. If the transistor gets warm, put the 100 Ω back and
leave it there. This is the one value in the project worth tuning by ear.

### Power

**4.5 V to 5 V.** Three AA cells, or the MB102 breadboard module set to 5 V. Both chips run
from 3 V to 18 V. Nothing in this project touches mains electricity.

---

## Rules for not breaking things

1. **Don't hold the buzzer against your ear.** This is the one real hazard in the series. A
   small buzzer a centimetre from your ear is loud enough to be genuinely unpleasant, and
   the 2 kHz note is the loudest one. Test at arm's length, and don't do it to somebody else
   as a joke.
2. **Unplug the power before you rewire.** Every time.
3. **Both chips are 14-pin, + on 14 and − on 7.** Notch to the left → pin 1 is bottom-left,
   and pin numbers run anticlockwise.
4. **Never leave an input dangling.** Every unused inverter input goes to −, and so does
   every unused CD4066 **control** pin. The CD4066's **switch** pins are different — they
   are neither inputs nor outputs, and may be left empty.
5. **Never wire an output straight to + or −.** That's a short circuit through the chip.
6. **The electrolytic capacitors have a polarity.** The stripe marks the negative leg.
   Backwards, they can pop. The little "104" ceramics don't care.
7. **Touch something metal and grounded before you pick up a chip.** Static kills CMOS.
8. If a chip ever feels **warm**, pull the power immediately — and check that the 100 Ω is
   really in series with the buzzer.

---

## Complete wire list

Everything is written as *pin → pin*, never as breadboard coordinates. `+` means the red
rail, `−` means the blue/black rail.

### Power rails

| ✓ | From | To |
|---|---|---|
| ☐ | Supply + | Top red rail |
| ☐ | Supply − | Top blue rail |
| ☐ | Top red rail | Bottom red rail |
| ☐ | Top blue rail | Bottom blue rail |
| ☐ | 100 µF + leg | Red rail (stripe/− leg to blue rail) |

### CD40106 — all three oscillators

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | pin 14 | + | Power |
| ☐ | pin 7 | − | Ground |
| ☐ | 0.1 µF | between pin 14 and pin 7 | Local smoothing |
| ☐ | pins 9, 11, 13 | − | The three unused inverter inputs |

**Inverter A — the sound**, about 1 100 Hz upward:

| ✓ | From | To |
|---|---|---|
| ☐ | 0.1 µF ("104") | pin 1 → − |
| ☐ | 1 MΩ | pin 2 → pin 1 |
| ☐ | pin 2 → button 1 → 10 kΩ | pin 1 |
| ☐ | pin 2 → button 2 → 5.1 kΩ | pin 1 |
| ☐ | pin 2 → button 3 → 2 kΩ | pin 1 |
| ☐ | pin 2 → button 4 → 1 kΩ | pin 1 |
| ☐ | pin 2 → 1 kΩ → photoresistor | pin 1 |

Use **diagonally opposite legs** on every button. Output: **pin 2 = the note**.

**Inverter B — the wail**, 1.2 per second:

| ✓ | From | To |
|---|---|---|
| ☐ | 100 kΩ | pin 4 → pin 3 |
| ☐ | 10 µF **+ leg** | pin 3 |
| ☐ | 10 µF **stripe leg** | − |

Output: **pin 4 = WAIL**.

**Inverter C — the chop**, 11 per second:

| ✓ | From | To |
|---|---|---|
| ☐ | 10 kΩ | pin 6 → pin 5 |
| ☐ | 10 µF **+ leg** | pin 5 |
| ☐ | 10 µF **stripe leg** | − |

Output: **pin 6 = CHOP**. Leave pins 8, 10 and 12 unconnected — unused outputs.

### CD4066 — the pitch switch

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | pin 14 | + | Power |
| ☐ | pin 7 | − | Ground |
| ☐ | 0.1 µF | between pin 14 and pin 7 | |
| ☐ | CD40106 pin 2 | 10 kΩ → CD4066 **pin 1** | The siren resistor |
| ☐ | CD4066 **pin 2** | CD40106 **pin 1** | Back to the timing node |
| ☐ | CD4066 **pin 13** | **WAIL jumper** | Switch A's control |
| ☐ | pins 5, 6, 12 | − | Unused controls — rule 4 |

Leave pins 3, 4, 8, 9, 10 and 11 empty — unused switch pins.

The switch and its 10 kΩ form a second timing path in parallel with the first. Closed means
less resistance, which means a higher note.

### The buzzer and the two transistors

| ✓ | From | To |
|---|---|---|
| ☐ | CD40106 **pin 2** | 10 kΩ → Q1 base (middle leg) |
| ☐ | Q1 collector (right leg) | buzzer leg |
| ☐ | Buzzer other leg | 100 Ω → + |
| ☐ | Q1 emitter (left leg) | Q2 collector (right leg) |
| ☐ | Q2 emitter (left leg) | − |
| ☐ | Q2 base (middle leg) | 10 kΩ → **CHOP jumper** |
| ☐ | Q2 base | 10 kΩ → − |

In Stage 1, before Q2 exists, Q1's emitter goes straight to −. Stage 5 moves that one wire.

Q1 goes on top because its base is driven by the audio oscillator's full 0–5 V swing, so it
has voltage to spare above Q2's collector. Stacked the other way, the note comes out weak
and distorted. The 10 kΩ from Q2's base to − keeps Q2 off if the CHOP jumper is unplugged.

### The two jumpers — how you pick the sound

Each is a single wire you move between two holes.

| Jumper | In here | Result |
|---|---|---|
| **WAIL** → CD4066 pin 13 | − rail | Switch open. One steady note |
| | CD40106 pin 4 | Pitch flips 1.2 times a second — **siren** |
| **CHOP** → Q2 base resistor | + rail | Q2 always on. Sound passes |
| | CD40106 pin 6 | Sound cut 11 times a second — **beeping** |

| WAIL | CHOP | What you get |
|---|---|---|
| − | + | A steady note — an instrument |
| pin 4 | + | **Police siren** — two tones |
| − | pin 6 | **Alarm clock** — one note, beeping |
| pin 4 | pin 6 | **Ambulance** — warbling beeps |

---

## The notes, and why they are flat

The clean formula is **f ≈ 1.23 ÷ (R × C)**. It is accurate for the two slow oscillators.
For the audio oscillator it is not, because a CD4000 output behaves as if it has about
**1 kΩ** of resistance built into it. With a 1 MΩ timing resistor that hidden kilohm is
nothing; with a 2 kΩ one it is a third of the total. So:

**f ≈ 1.23 ÷ ( (R + 1 kΩ) × C )**

Every button's resistor sits in parallel with the 1 MΩ bleed resistor, which barely changes
anything but is what keeps the input from floating.

| Button | R in parallel with 1 MΩ | Naive f | With the 1 kΩ correction |
|---|---|---|---|
| none | 1 MΩ | 12.3 Hz | 12.3 Hz — a tick, not a note |
| 1 — 10 kΩ | 9.90 kΩ | 1 242 Hz | **1 133 Hz** |
| 2 — 5.1 kΩ | 5.07 kΩ | 2 425 Hz | **2 040 Hz** |
| 3 — 2 kΩ | 1.996 kΩ | 6 162 Hz | **4 168 Hz** |
| 4 — 1 kΩ | 0.999 kΩ | 12 312 Hz | **6 295 Hz** |

Notice the correction hardly matters for button 1 and nearly halves button 4. Measuring that
gap and working backwards to the hidden resistance is exercise 3 in the worksheet.

With the WAIL switch closed, its 10 kΩ (plus the switch's own 470 Ω) joins the parallel
group, so holding button 1 gives a siren alternating between **1 133 Hz and 2 035 Hz**.

Slow oscillators, both with the 10 µF:

| Job | R | Rate |
|---|---|---|
| WAIL | 100 kΩ | 1.2 per second |
| CHOP | 10 kΩ | 11 per second |

Expect your own build to land within about 30% of every number here. "104" capacitors are
allowed to be 20% out, electrolytics far worse, and the trigger thresholds vary between
chips. Nothing in this box cares.

---

## Pin reference

Checked against the Texas Instruments datasheets. Both chips: **+ on 14, − on 7**.

```
CD40106  hex Schmitt NOT        CD4066  quad analog switch
 in  1 -> out  2                 switch A: pins 1 + 2   control 13
 in  3 -> out  4                 switch B: pins 3 + 4   control  5
 in  5 -> out  6                 switch C: pins 8 + 9   control  6
 in  9 -> out  8                 switch D: pins 10 + 11 control 12
 in 11 -> out 10
 in 13 -> out 12                 control HIGH = switch closed
                                 on-resistance about 470 Ω at 5 V
 in this project:
   A = the note, B = wail, C = chop
```

A CD4066 switch has no input and no output — just two ends of a wire, and current flows
either way. That is why it can sit inside a timing network, where a gate would wreck it.
Its control pins are ordinary logic inputs and must never float.

---

## Troubleshooting

| What you hear | Almost always |
|---|---|
| Nothing at all, ever | The **active** buzzer fitted instead of the passive one, or the 100 Ω not connected. Touch the buzzer straight across + and − — if it beeps on its own, it's the active one. |
| One fixed beep whatever you press | That is the active buzzer. Its oscillator is sealed inside and ignores yours. Use the passive one. |
| A slow tick instead of a note | The 1 MΩ is doing the timing. No button resistor is actually reaching pin 1. |
| A squeal that changes when you touch the board | Pin 1 is floating — the 1 MΩ bleed resistor is missing. |
| Every note lower than the table | Your timing capacitor is bigger than 0.1 µF. Check it says 104. |
| Only the top two notes lower than the table | Expected. That's the chip's own 1 kΩ. |
| Notes 3 and 4 sound weak or wobbly | Also expected — the chip is near the current it can push. Nothing is broken. |
| Pitch doesn't change with the photoresistor | The 1 kΩ floor and the sensor must be in series with each other, both between pin 2 and pin 1. |
| Siren won't wail, just one note | WAIL jumper still in the − rail, or CD4066 pin 2 not reaching CD40106 pin 1. |
| Wail changes volume but not pitch | The siren resistor is on the wrong side of the switch. Path is pin 2 → 10 kΩ → CD4066 pin 1, switch, CD4066 pin 2 → pin 1. |
| Wail is far too fast or too slow | The two 10 µF capacitors swapped with each other, or one is in backwards. |
| Chop doesn't chop | CHOP jumper still in the + rail, or Q1's emitter is still wired to − instead of to Q2's collector. |
| Silent after adding Q2 | Q2 in backwards. Flat side toward you, legs down: E – B – C, left to right. |
| Sound is very quiet | Try the 10 Ω in place of the 100 Ω. If the transistor warms up, put it back. |
| A chip gets warm | Unplug now. Power backwards, or the buzzer's 100 Ω is missing. |
| Everybody in the house is annoyed with you | Working as designed. Fit the 1 MΩ and it becomes a quiet tick. |

---

## Files

| File | What's in it |
|---|---|
| [`guide.html`](guide.html) | The illustrated guide: five stages, and the box playable with sound in the browser |
| [`worksheet.md`](worksheet.md) | Pitch measurements, finding the chip's hidden resistance, and the hearing test |
| `README.md` | This file — parts, wire lists, pinouts, troubleshooting |
