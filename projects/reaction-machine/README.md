# The Reaction Machine

A ring of ten lights with a dot running round it, and one press of a button to stop the dot
on the gold one. Green light and a beep if you hit it, red light if you didn't.

There is no computer in it. A resistor and a capacitor decide how fast time runs, a counter
decides which light is on, and a flip-flop remembers that you pressed.

Built for a curious 10-to-12-year-old, using CD4000-series logic chips, a breadboard and a
dozen LEDs.

**Open [`guide.html`](https://guddis.github.io/breadboard-lab/projects/reaction-machine/guide.html) in a browser** — that's the real guide, and the game is
playable on the page before you build anything. This file is the bench reference: parts,
wire lists, troubleshooting.

---

## What it teaches

| Idea | Where it shows up |
|---|---|
| A capacitor is a bucket; a resistor is the pipe filling it | Stage 1 |
| An inverter fed from its own output can never settle — it oscillates | Stage 1 |
| A Schmitt trigger has *two* thresholds, and that's what makes a clean beat | Stage 1 |
| f ≈ 1.23 ÷ (R × C) — timing you can predict before you build it | Stage 1, worksheet |
| Resistors side by side make a *smaller* resistance | Stage 5 |
| A counter turns beats into positions | Stage 2 |
| Datasheet pin order isn't logical order — read the drawing | Stage 2 |
| Not every chip is 14-pin | Stage 2, the hard way if you're careless |
| A flip-flop stays changed after you let go — one bit of memory | Stage 3 |
| Memory wakes up holding nonsense until you reset it | Stage 3 |
| An AND gate used as a valve: signal on one input, permission on the other | Stage 4 |
| A wire has a *strength* as well as a value — loading and logic levels | Stage 4 |
| Chips think, transistors shove | Stage 4 |

Total build time is about 2–2½ hours, in five stages you can stop between.

---

## Parts

### Chips

| Chip | What it is | Job in the machine |
|---|---|---|
| CD40106 | Hex Schmitt-trigger inverter | The clock, plus one spare inverter for MISS |
| CD4017 | Decade counter, 10 decoded outputs | Walks the dot round the ring — **16 pins** |
| CD4013 | Dual D-type flip-flop | Remembers that you pressed STOP |
| CD4081 | Quad 2-input AND | The WIN and MISS verdicts |

### Everything else

| Qty | Part | Notes |
|---|---|---|
| 9 | Red LED | The ring |
| 1 | Yellow LED | The gold target |
| 1 | Green LED | WIN |
| 1 | Red LED | MISS — the tenth red one |
| 3 | PN2222 NPN transistor | Flat side toward you, legs down: **E – B – C** |
| 1 | Active buzzer | The kind that beeps on its own from DC |
| 2 | Push button (small) | STOP and RESET |
| 9 | 220 Ω resistor | The nine plain ring LEDs |
| 3 | 330 Ω resistor | Gold, WIN and MISS LEDs |
| 1–4 | 1 MΩ resistor | Clock speed — more in parallel means faster |
| 1 | 100 kΩ resistor | Slow mode, for building and debugging |
| 3 | 10 kΩ resistor | Gold transistor base, two button pull-downs |
| 2 | 5.1 kΩ resistor | WIN and MISS transistor bases |
| 1 | 1 kΩ resistor | Stage 1 test LED only, removed afterwards |
| 5 | 0.1 µF ceramic ("104") | One per chip across its power pins, plus one for the clock |
| 1 | 10 µF electrolytic | Slow mode — **stripe goes to −** |
| 1 | 100 µF electrolytic | Across the power rails — **stripe goes to −** |
| 1 | Breadboard | Full-size. Four chips and twelve LEDs need the room |
| ~45 | Jumper wires | Red for +, black for −, colours for signals |

### Power

**4.5 V to 5 V.** Either three AA cells, or the MB102 breadboard power module set to 5 V.

All four chips are happy anywhere from 3 V to 18 V, so nothing here is fragile about
voltage. Nothing in this project touches mains electricity.

---

## Rules for not breaking things

1. **Unplug the power before you rewire.** Every time.
2. **Count the pins.** The CD40106, CD4013 and CD4081 are 14-pin chips with **+ on 14** and
   **− on 7**. The CD4017 is a 16-pin chip with **+ on 16** and **− on 8**. Wire the CD4017
   like a 14-pin chip and you put 5 V straight into an output.
3. **The notch tells you which end is which.** Notch to the left → pin 1 is bottom-left,
   and pin numbers run anticlockwise. Backwards means power and ground swap, and the chip
   gets hot and dies.
4. **Never leave an input wire dangling.** A CMOS input connected to nothing picks up radio
   noise and flickers randomly. Every input goes to + or to − or to another chip's output.
   Unused inputs go to −.
5. **Never wire an output straight to + or −.** That's a short circuit through the chip.
   The CD4017 has ten outputs in a row and it is easy to ground one by accident.
6. **The electrolytic capacitors have a polarity.** The stripe marks the negative leg.
   Backwards, they can pop. The little "104" ceramics don't care.
7. **Touch something metal and grounded before you pick up a chip.** Static kills CMOS.
8. If a chip ever feels **warm**, pull the power immediately and check the wiring.

---

## Complete wire list

Everything is written as *pin → pin*, never as breadboard coordinates, so it works no
matter where you place things. `+` means the red rail, `−` means the blue/black rail.

### Power rails

| ✓ | From | To |
|---|---|---|
| ☐ | Supply + | Top red rail |
| ☐ | Supply − | Top blue rail |
| ☐ | Top red rail | Bottom red rail |
| ☐ | Top blue rail | Bottom blue rail |
| ☐ | 100 µF + leg | Red rail (stripe/− leg to blue rail) |

### CD40106 — the clock

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | pin 14 | + | Power |
| ☐ | pin 7 | − | Ground |
| ☐ | 0.1 µF | between pin 14 and pin 7 | Local smoothing |
| ☐ | 1 MΩ | pin 2 → pin 1 | Timing resistor — output back to its own input |
| ☐ | 0.1 µF ("104") | pin 1 → − | Timing capacitor |
| ☐ | pins 5, 9, 11, 13 | − | Unused inputs |

Outputs: **pin 2 = CLOCK**. **pin 4 = NOT GOLD** once Stage 4 wires pin 3.
Leave pins 6, 8, 10 and 12 unconnected — they are outputs of unused inverters.

For slow mode while building, use **100 kΩ** and the **10 µF** (+ leg to pin 1, stripe to
−) instead. About 1.2 beats per second.

### CD4017 — the counter

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | **pin 16** | + | Power — not pin 14 |
| ☐ | **pin 8** | − | Ground — not pin 7 |
| ☐ | 0.1 µF | between pin 16 and pin 8 | |
| ☐ | CD40106 pin 2 | CD4017 pin 14 | Clock in |
| ☐ | pin 15 | − | Reset off — we never zero the count |
| ☐ | pin 13 | CD4013 pin 1 | Clock inhibit ← FROZEN |

Pin 12 is carry out — leave it empty unless you build a bonus.

### The ring — ten lamps

Each lamp is **CD4017 output pin → resistor → LED long leg**, and **LED short leg → −**.
The outputs are *not* in counting order, so follow the pin column exactly.

| ✓ | Ring position | Count | CD4017 pin | LED | Resistor |
|---|---|---|---|---|---|
| ☐ | 1 | 0 | 3 | Red | 220 Ω |
| ☐ | 2 | 1 | 2 | Red | 220 Ω |
| ☐ | 3 | 2 | 4 | Red | 220 Ω |
| ☐ | 4 | 3 | 7 | Red | 220 Ω |
| ☐ | 5 | 4 | 10 | Red | 220 Ω |
| ☐ | **6** | **5** | **1** | **Yellow — the gold one** | see below |
| ☐ | 7 | 6 | 5 | Red | 220 Ω |
| ☐ | 8 | 7 | 6 | Red | 220 Ω |
| ☐ | 9 | 8 | 9 | Red | 220 Ω |
| ☐ | 10 | 9 | 11 | Red | 220 Ω |

Arrange them in a circle if your jumpers reach, or a straight row if they don't. Keep the
gold one at position 6 either way, so it isn't at an end where it's easier to hit.

### The gold lamp — Q1, via a transistor

In Stage 2 you wire position 6 like all the others, to get the ring working. In Stage 4 you
**remove that 220 Ω and yellow LED** and replace them with this:

| ✓ | From | To |
|---|---|---|
| ☐ | CD4017 pin 1 | 10 kΩ → Q1 base (middle leg) |
| ☐ | Q1 emitter (left leg) | − |
| ☐ | + | 330 Ω → yellow LED long leg |
| ☐ | Yellow LED short leg | Q1 collector (right leg) |

This is not decoration. CD4017 pin 1 also has to be *read* by the CD4081 and the CD40106,
and a pin dragged down to 2.5 V by an LED is neither a 0 nor a 1. Through 10 kΩ into a
transistor base it draws 0.43 mA, stays at about 4.6 V, and reads as a clean 1 — and the
gold lamp ends up the brightest in the ring.

### CD4013 — the freeze latch

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | pin 14 | + | Power |
| ☐ | pin 7 | − | Ground |
| ☐ | 0.1 µF | between pin 14 and pin 7 | |
| ☐ | pin 5 (D1) | − | Not using the clocked input |
| ☐ | pin 3 (CLOCK1) | − | Held quiet |
| ☐ | pin 6 (SET1) | STOP node | Press = remember |
| ☐ | pin 4 (RESET1) | RESET node | Press = forget |
| ☐ | pins 8, 9, 10, 11 | − | The whole second flip-flop, unused |

Output: **pin 1 = FROZEN**. Leave pins 2, 12 and 13 unconnected.

### The two buttons

A 4-pin tactile button has its legs joined in hidden pairs. Using **diagonally opposite**
legs is the one choice that is always right.

| ✓ | From | To |
|---|---|---|
| ☐ | STOP leg | + |
| ☐ | STOP leg, **diagonally opposite** | STOP node |
| ☐ | STOP node | 10 kΩ → − |
| ☐ | STOP node | CD4013 pin 6 |
| ☐ | RESET leg | + |
| ☐ | RESET leg, **diagonally opposite** | RESET node |
| ☐ | RESET node | 10 kΩ → − |
| ☐ | RESET node | CD4013 pin 4 |

The 10 kΩ pull-downs are not optional. Without them the button node is connected to
nothing when the button is up, and the latch will set and reset itself as you walk past.

### CD4081 — the two verdicts

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | pin 14 | + | Power |
| ☐ | pin 7 | − | Ground |
| ☐ | 0.1 µF | between pin 14 and pin 7 | |
| ☐ | CD4017 pin 1 | CD40106 pin 3 | Gold into the spare inverter |
| ☐ | CD4013 pin 1 | CD4081 pin 1 | FROZEN |
| ☐ | CD4017 pin 1 | CD4081 pin 2 | GOLD |
| ☐ | CD4013 pin 1 | CD4081 pin 5 | FROZEN |
| ☐ | CD40106 pin 4 | CD4081 pin 6 | NOT GOLD |
| ☐ | pins 8, 9, 12, 13 | − | Two unused gates |

Outputs: **pin 3 = WIN**, **pin 4 = MISS**. Leave pins 10 and 11 unconnected.

### Output block — Q2, the win

| ✓ | From | To |
|---|---|---|
| ☐ | CD4081 pin 3 | 5.1 kΩ → Q2 base |
| ☐ | Q2 emitter | − |
| ☐ | + | 330 Ω → green LED long leg |
| ☐ | Green LED short leg | Q2 collector |
| ☐ | Buzzer + (long leg) | + |
| ☐ | Buzzer − | Q2 collector |

### Output block — Q3, the miss

| ✓ | From | To |
|---|---|---|
| ☐ | CD4081 pin 4 | 5.1 kΩ → Q3 base |
| ☐ | Q3 emitter | − |
| ☐ | + | 330 Ω → red LED long leg |
| ☐ | Red LED short leg | Q3 collector |

Q1 gets 10 kΩ because CD4017 pin 1 also has to be read as a logic level by two chips, so
it must stay lightly loaded. Q2 and Q3 drive nothing but their own transistor, so they can
afford the 5.1 kΩ that makes those outputs brighter and louder.

---

## Clock speeds

The timing resistor sits between CD40106 pin 2 and pin 1. To speed the game up, plug extra
1 MΩ resistors into the same two holes, side by side.

| 1 MΩ resistors | Behaves like | Beats/sec | Times round per second |
|---|---|---|---|
| 1 | 1 MΩ | ≈ 12 | 1.2 |
| 2 in parallel | 500 kΩ | ≈ 25 | 2.5 |
| 3 in parallel | 333 kΩ | ≈ 37 | 3.7 |
| 4 in parallel | 250 kΩ | ≈ 49 | 4.9 |

Slow mode for building and debugging: **100 kΩ + 10 µF**, about 1.2 beats per second.

The formula is **f ≈ 1.23 ÷ (R × C)**, where the 1.23 comes from the CD40106's two trigger
thresholds at 5 V — 2.9 V going up and 1.9 V coming down, both from the datasheet. Expect
your own build to land anywhere within about 30% of the table; "104" capacitors are allowed
to be 20% out and the thresholds vary between chips. Nothing here cares.

---

## Pin reference

Checked against the Texas Instruments datasheets. **Note the CD4017 is the odd one out.**

```
CD40106  hex Schmitt NOT       CD4013  dual D flip-flop
 in  1 -> out  2                 1 Q1        14 +VDD
 in  3 -> out  4                 2 Q1-not    13 Q2
 in  5 -> out  6                 3 CLOCK1    12 Q2-not
 in  9 -> out  8                 4 RESET1    11 CLOCK2
 in 11 -> out 10                 5 D1        10 RESET2
 in 13 -> out 12                 6 SET1       9 D2
 +VDD = 14   -VSS = 7            7 -VSS       8 SET2

CD4081  quad AND               CD4017  decade counter  ** 16 PINS **
 in 1,  2  -> out  3            count: 0 1 2 3  4 5 6 7 8  9
 in 5,  6  -> out  4            pin:   3 2 4 7 10 1 5 6 9 11
 in 8,  9  -> out 10
 in 12,13  -> out 11            pin 14 = CLOCK    pin 13 = CLOCK INHIBIT
 +VDD = 14   -VSS = 7           pin 15 = RESET    pin 12 = CARRY OUT
                                +VDD = 16         -VSS = 8
```

The CD4017's ten outputs are laid out to keep its internal wiring short, not to be
convenient for you. Copy the count/pin row; don't reason about it.

---

## Troubleshooting

| What you see | Almost always |
|---|---|
| Nothing lights at all | Power not reaching a chip. Check both pins on every chip — and remember the CD4017 wants + on **16** and − on **8**. |
| A chip gets warm | Power in backwards, or an output wired to a rail. Unplug now. |
| Clock LED never blinks | The 1 MΩ must go from pin 2 **back to pin 1**. To a rail instead means no feedback and no oscillation. |
| Clock LED glows steadily instead of blinking | It's running fast — that's the 0.1 µF. Fit the 10 µF for slow mode. |
| Ring is frozen the moment you power up | Normal. A flip-flop wakes up in a random state. Press RESET. |
| Dot hops around out of order | The LEDs are wired in pin order. Use the count/pin table. |
| Dot skips one position | That LED is backwards, or its resistor leg isn't in the same column. |
| Two lamps lit at once | Two LEDs sharing a resistor, or a jumper bridging two outputs. |
| Whole ring lit dimly | The clock is much too fast, or CD4017 pin 13 is floating. |
| STOP does nothing | Button legs aren't diagonal, or the 10 kΩ pull-down is missing. |
| STOP works but it un-freezes on its own | RESET node floating — its pull-down is missing. |
| Green light is moody: sometimes on, sometimes not, for the same stop | The gold LED is still hanging straight off CD4017 pin 1. Fit the Q1 transistor. |
| Green and red both on | CD40106 pin 3 isn't connected to CD4017 pin 1, so NOT GOLD is stuck high. |
| Neither verdict lamp ever lights | CD4013 pin 1 isn't reaching CD4081 pins 1 and 5. |
| Buzzer silent but green works | Buzzer polarity, or a passive buzzer instead of the active one. |
| Buzzer never stops | It shouldn't until you press RESET. That's the design. |
| Ring looks too dim to play | Nine lamps at 2½ mA, each lit a tenth of the time. Turn the room lights down. |
| Everything is wrong at once | Unplug, walk away for five minutes, come back and re-read one table. This is what real engineers do. |

---

## Files

| File | What's in it |
|---|---|
| [`guide.html`](guide.html) | The illustrated guide: five stages, and the game playable in the browser |
| [`worksheet.md`](worksheet.md) | Timing measurements, the counter's pin map, and the score sheet |
| `README.md` | This file — parts, wire lists, pinouts, troubleshooting |
