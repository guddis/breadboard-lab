# The Step Sequencer

Eight steps, three chips, and an analog synthesizer playing a looping bassline on your bench.

A master clock ticks, a decade counter steps through eight positions in sequence, and eight
trim pots dial in eight separate musical notes. A quad bilateral switch acts as an analog gate,
cutting the audio between steps so each note hits with crisp rhythm instead of an endless siren.
There is no microcontroller, no MIDI, and no code — this is the exact analog-digital hybrid
architecture behind the legendary Roland TB-303 and early Moog modular synthesizers.

**Open [`guide.html`](https://guddis.github.io/breadboard-lab/projects/step-sequencer/guide.html) in a browser** — that's the real guide, with diagrams and
a working Web Audio synthesizer you can play with before touching a wire. This file is the
bench reference: parts, wire lists, pinouts, and troubleshooting.

Build [the Reaction Machine](../reaction-machine/) and [the Siren Box](../siren-box/) first if
you haven't. This project takes the counter from the Reaction Machine and the audio oscillator
and bilateral switch from the Siren Box, combining them into a standalone musical instrument.

---

## What it teaches

| Idea | Where it shows up |
|---|---|
| **Analog-digital hybrid design** — digital logic controlling analog pitch | The whole project |
| **Clock division & tempo** — RC oscillator setting beats per minute (BPM) | Stage 1 |
| **Sequence looping (Modulo-8)** — resetting a decade counter on step 8 | Stage 2 |
| **The 16-pin trap** — CD4017 has power on pin 16 and ground on pin 8 | Stage 2 |
| **Audio waveform generation** — high-frequency Schmitt-trigger square waves | Stage 3 |
| **Transistor speaker driver** — PN2222 amplifying CMOS output for a speaker | Stage 3 |
| **Control Voltage (CV) & pitch mixing** — steering resistance per step with diodes | Stage 4 |
| **Bilateral analog gating** — CD4066 creating staccato articulation and glide | Stage 5 |
| **Synthesizer history** — how the TR-808 and TB-303 sequenced dance music | Section 2 and `.why` |

Total build time is about 2½–3 hours, in 5 stages you can stop between. Every stage leaves a
circuit that visibly or audibly does something rewarding.

---

## Parts

Everything here is in the standard kit.

### Chips

| Chip | What it is | Pins | Job in the sequencer |
|---|---|---|---|
| CD40106 | Hex Schmitt-trigger inverter | 14 | Inverter 1 = Tempo clock; Inverter 2 = Pitch oscillator; Inverter 3 = Gate shaper |
| CD4017 | Decade counter, 10 decoded outputs | **16** | Advances the sequence 0 $\rightarrow$ 7, and loops back on 8 |
| CD4066 | Quad bilateral analog switch | 14 | Switch A = Note gate / articulation; Switch B = Octave jump; Switch C = Slide / glide |

> **Crucial Warning:** The CD40106 and CD4066 are standard 14-pin chips (+ on 14, − on 7).
> The **CD4017 is a 16-pin chip** (+ on **16**, − on **8**). Wiring the CD4017 like a 14-pin
> chip puts 5 V directly into an output and destroys the chip.

### Everything else

| Qty | Part | Notes |
|---|---|---|
| 1 | **Passive** buzzer or 8 Ω mini speaker | The kind that requires an AC audio signal (silent on DC). **Not** active |
| 1 | PN2222 NPN transistor | Flat side facing you, legs down: **E – B – C** (Emitter, Base, Collector) |
| 8 | Potentiometer / trim pot (10 kΩ, 50 kΩ, or 100 kΩ) | One per step to tune the pitch |
| 8 | Diode 1N4148 (or 1N4001) | Isolation diodes on each step wiper to prevent steps back-feeding |
| 8 | LED 5 mm (Red, Yellow, or Green) | Playhead position indicators for steps 1 through 8 |
| 1 | LED 5 mm (Teal or Blue) | Tempo clock beat indicator |
| 9 | Resistor 220 Ω (or 330 Ω) | One per step LED, plus one for the tempo LED |
| 1 | Resistor 100 Ω | Speaker current limiter — **mandatory**, protects transistor |
| 2 | Resistor 10 kΩ | Transistor base resistor, CD4066 gate control pull-down |
| 1 | Resistor 47 kΩ (or 100 kΩ) | Audio oscillator base frequency resistor |
| 1 | Resistor 1 MΩ | Bleed resistor across audio oscillator input |
| 1 | Resistor 100 kΩ pot (or 100 kΩ resistor) | Tempo speed control |
| 3 | Capacitor 0.1 µF ceramic ("104") | Power decoupling (one per chip), plus audio pitch capacitor |
| 1 | Capacitor 1 µF electrolytic (or 10 µF) | Tempo clock timing capacitor (stripe to −) |
| 1 | Capacitor 100 µF electrolytic | Bulk power rail smoothing (stripe to −) |
| 1 | Breadboard | Full-size recommended for the 8 trim pots and LEDs |
| — | Hookup wire | Solid-core 22 AWG jumpers |

---

## Rules for not breaking things

1. **Unplug power before rewiring.** Always.
2. **Watch the CD4017 pin count.** 16 pins! + goes to pin 16, − goes to pin 8.
3. **The 100 Ω speaker resistor is not optional.** An 8 Ω or 16 Ω speaker coil connected
   straight across 5 V draws over 300 mA, which will burn the PN2222 transistor and kill your battery.
4. **Passive buzzer only.** An active buzzer has its own internal beeper and cannot change pitch.
   Touch the buzzer to a 5 V battery: if it beeps on DC, it's active (wrong part); if it makes a single click, it's passive (correct part).
5. **Diodes have a polarity.** The black band marks the cathode (negative end). Current only flows
   toward the band.
6. **Electrolytic capacitors have a stripe.** The white stripe with minus signs marks the negative leg.
7. **Tie unused inputs.** Every unused logic input goes to −. CD4066 control pins must never float.

---

## Complete wire list

Written as *pin → pin*, never breadboard coordinates.
`+` is the red rail, `−` is the blue rail.

### Power rails

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | Supply + | Top red rail (+) | Main 5 V power |
| ☐ | Supply − | Top blue rail (−) | Main ground |
| ☐ | Top red rail | Bottom red rail | Link rails |
| ☐ | Top blue rail | Bottom blue rail | Link rails |
| ☐ | 100 µF capacitor | Across + and − rails | Bulk smoothing (stripe to −) |

### Chip power and decoupling

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | CD40106 pin 14 | + rail | Hex Schmitt power |
| ☐ | CD40106 pin 7 | − rail | Hex Schmitt ground |
| ☐ | 0.1 µF capacitor | CD40106 pin 14 to pin 7 | Local decoupling |
| ☐ | CD40106 pins 11, 13 | − rail | Tie unused inverter inputs |
| ☐ | **CD4017 pin 16** | + rail | **Counter power — note pin 16!** |
| ☐ | **CD4017 pin 8** | − rail | **Counter ground — note pin 8!** |
| ☐ | 0.1 µF capacitor | CD4017 pin 16 to pin 8 | Local decoupling |
| ☐ | CD4017 pin 13 | − rail | Clock inhibit off (enable count) |
| ☐ | CD4066 pin 14 | + rail | Quad switch power |
| ☐ | CD4066 pin 7 | − rail | Quad switch ground |
| ☐ | 0.1 µF capacitor | CD4066 pin 14 to pin 7 | Local decoupling |
| ☐ | CD4066 pin 12 | − rail | Tie unused Switch D control |

### Stage 1: Tempo Clock (CD40106 Inverter 1)

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | CD40106 pin 1 | 1 µF capacitor (positive leg) | Timing node |
| ☐ | 1 µF capacitor (negative leg) | − rail | Clock timing capacitor (stripe to −) |
| ☐ | CD40106 pin 2 (OUT 1) | 100 kΩ pot (left leg) | Feedback path |
| ☐ | 100 kΩ pot (middle wiper) | CD40106 pin 1 | Variable timing resistance |
| ☐ | CD40106 pin 2 | Tempo LED anode (long leg) | Beat indicator |
| ☐ | Tempo LED cathode | 220 Ω resistor to − rail | Current limiter |

### Stage 2: 8-Step Counter & Chasing LEDs (CD4017)

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | CD40106 pin 2 (Clock) | CD4017 pin 14 (CLOCK IN) | Tempo clock drives counter |
| ☐ | **CD4017 pin 9 (Q8)** | **CD4017 pin 15 (RESET)** | **Reset on step 8 $\rightarrow$ makes 8-step loop** |

#### Step LEDs (Q0 through Q7):
Outputs are arranged by counting order, not pin order.

| ✓ | Step | Count | CD4017 Output Pin | LED connection |
|---|---|---|---|---|
| ☐ | Step 1 | Q0 | Pin 3 | Pin 3 $\rightarrow$ LED 1 anode $\rightarrow$ 220 Ω $\rightarrow$ − rail |
| ☐ | Step 2 | Q1 | Pin 2 | Pin 2 $\rightarrow$ LED 2 anode $\rightarrow$ 220 Ω $\rightarrow$ − rail |
| ☐ | Step 3 | Q2 | Pin 4 | Pin 4 $\rightarrow$ LED 3 anode $\rightarrow$ 220 Ω $\rightarrow$ − rail |
| ☐ | Step 4 | Q3 | Pin 7 | Pin 7 $\rightarrow$ LED 4 anode $\rightarrow$ 220 Ω $\rightarrow$ − rail |
| ☐ | Step 5 | Q4 | Pin 10 | Pin 10 $\rightarrow$ LED 5 anode $\rightarrow$ 220 Ω $\rightarrow$ − rail |
| ☐ | Step 6 | Q5 | Pin 1 | Pin 1 $\rightarrow$ LED 6 anode $\rightarrow$ 220 Ω $\rightarrow$ − rail |
| ☐ | Step 7 | Q6 | Pin 5 | Pin 5 $\rightarrow$ LED 7 anode $\rightarrow$ 220 Ω $\rightarrow$ − rail |
| ☐ | Step 8 | Q7 | Pin 6 | Pin 6 $\rightarrow$ LED 8 anode $\rightarrow$ 220 Ω $\rightarrow$ − rail |

### Stage 3: Audio Oscillator & Speaker Driver (CD40106 Inverter 2)

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | CD40106 pin 3 | 0.1 µF ceramic ("104") | Audio timing node |
| ☐ | 0.1 µF other leg | − rail | Audio pitch capacitor |
| ☐ | CD40106 pin 3 | 1 MΩ resistor to CD40106 pin 4 | High-impedance bleed resistor |
| ☐ | CD40106 pin 4 (OUT 2) | CD4066 pin 1 (Switch A IN) | Raw audio square wave |
| ☐ | CD4066 pin 2 (Switch A OUT) | 10 kΩ resistor $\rightarrow$ PN2222 Base (middle leg) | Gated audio drives transistor |
| ☐ | PN2222 Emitter (left leg) | − rail | Transistor ground reference |
| ☐ | PN2222 Collector (right leg) | Speaker / passive buzzer negative wire | Switched audio current |
| ☐ | Speaker positive wire | 100 Ω resistor to + rail | **Mandatory current limiter** |

*(In Stage 3 testing before CD4066 is wired, jump CD40106 pin 4 directly through 10 kΩ to PN2222 base to hear the raw continuous tone).*

### Stage 4: 8-Step Pitch Tuning Network (The Melody Bus)

Each of the 8 CD4017 step outputs connects to a 10 kΩ or 50 kΩ trim pot.
The wipers all meet at a common **Pitch Bus** through isolation diodes:

| ✓ | Step | Pot Input | Pot Wiper | Diode | Destination |
|---|---|---|---|---|---|
| ☐ | Step 1 | CD4017 pin 3 | Middle pin | 1N4148 (black band to bus) | Common Pitch Bus |
| ☐ | Step 2 | CD4017 pin 2 | Middle pin | 1N4148 (black band to bus) | Common Pitch Bus |
| ☐ | Step 3 | CD4017 pin 4 | Middle pin | 1N4148 (black band to bus) | Common Pitch Bus |
| ☐ | Step 4 | CD4017 pin 7 | Middle pin | 1N4148 (black band to bus) | Common Pitch Bus |
| ☐ | Step 5 | CD4017 pin 10 | Middle pin | 1N4148 (black band to bus) | Common Pitch Bus |
| ☐ | Step 6 | CD4017 pin 1 | Middle pin | 1N4148 (black band to bus) | Common Pitch Bus |
| ☐ | Step 7 | CD4017 pin 5 | Middle pin | 1N4148 (black band to bus) | Common Pitch Bus |
| ☐ | Step 8 | CD4017 pin 6 | Middle pin | 1N4148 (black band to bus) | Common Pitch Bus |
| ☐ | **Pitch Bus** | CD40106 pin 3 | — | — | Feeds audio oscillator node |

*(Left leg of each trim pot connects to the step pin; right leg stays unconnected or to ground for voltage-divider mode).*

### Stage 5: Gating & Analog Articulation (CD4066)

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | CD40106 pin 2 (Clock) | CD4066 pin 13 (Switch A Control) | Note Gate: on during clock pulse |
| ☐ | CD4066 pin 13 | 10 kΩ resistor to − rail | Pull-down keeps gate closed when silent |
| ☐ | **SLIDE Jumper:** | CD4066 pin 8 & 9 (Switch C) | Connects 1 µF capacitor across Pitch Bus |
| ☐ | CD4066 pin 6 (Switch C Control) | + rail (or jumper) | Engages analog portamento slide |

---

## Pin reference

Verified against Texas Instruments datasheets: CD40106B (SCHS097B), CD4017B (SCHS027C), and CD4066B (SCHS051E).

```
CD40106  hex Schmitt NOT (14 pins)     CD4066  quad bilateral switch (14 pins)
  in  1 -> out  2                       switch A: pins  1 +  2   control 13
  in  3 -> out  4                       switch B: pins  3 +  4   control  5
  in  5 -> out  6                       switch C: pins  8 +  9   control  6
  in  9 -> out  8                       switch D: pins 10 + 11   control 12
  in 11 -> out 10                       + VDD on pin 14,  − VSS on pin 7
  in 13 -> out 12
  + VDD on pin 14, − VSS on pin 7

CD4017  decade counter (16 PINS — DO NOT CONFUSE WITH 14-PIN CHIPS)
  outputs:  Q0  Q1  Q2  Q3  Q4  Q5  Q6  Q7  Q8  Q9
  pins:      3   2   4   7  10   1   5   6   9  11
  pin 14 = CLOCK IN         pin 13 = CLOCK INHIBIT (tie to −)
  pin 15 = RESET            pin 12 = CARRY OUT
  + VDD on pin 16           − VSS on pin 8
```

---

## Troubleshooting

| What you experience | Almost always |
|---|---|
| No sound and no LEDs | Power not reaching a chip. Check both rails and remember the CD4017 wants **+ on 16** and **− on 8**. |
| Continuous high-pitched whine that never steps | CD40106 tempo clock is not oscillating. Check the 1 µF capacitor and 100 kΩ pot on pins 1 and 2. |
| Steps count, but only one note sounds for all 8 steps | Diodes are missing or in backwards. The black stripe must face the common pitch bus. |
| The counter stops on step 8 instead of looping | CD4017 pin 9 (Q8) is not wired to pin 15 (RESET), or pin 13 (CLOCK INHIBIT) is floating instead of grounded. |
| Notes drone continuously without rhythm gaps | The CD4066 gate switch is bypassed or control pin 13 is tied directly to +. Connect pin 13 to clock pin 2. |
| Buzzer is dead silent, but LEDs sequence nicely | Active buzzer used instead of passive, or PN2222 transistor is inserted backwards (flat side must face you, E-B-C). |
| Transistor or chips get warm | The mandatory 100 Ω resistor was omitted from the speaker line. Unplug now and insert the 100 Ω. |
| Pitch jumps wildly when your hand nears the board | The 1 MΩ bleed resistor across CD40106 pins 3 and 4 is missing, leaving the audio input floating between steps. |
| The melody sounds chaotic or out of order | CD4017 outputs are not in counting order physically on the chip. Use the pin reference table: 3, 2, 4, 7, 10, 1, 5, 6. |
