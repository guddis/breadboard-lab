# The Quiz Buzzer

Four buttons, four lamps, one buzzer. The first person to press lights their lamp, and the
other three buttons go completely dead until the host presses RESET.

The interesting part isn't the lamp. It's that the machine works out who was first in less
than a millionth of a second — about five thousand times faster than the closest tie two
people can produce — which is the entire reason it is never wrong.

Built for a curious 10-to-12-year-old, using three CD4000-series chips and a handful of LEDs.

**Open [`guide.html`](https://guddis.github.io/breadboard-lab/projects/quiz-buzzer/guide.html) in a browser** — that's the real guide, and the buzzer is
playable on the page, including the part where you try to cheat. This file is the bench
reference: parts, wire lists, troubleshooting.

---

## What it teaches

| Idea | Where it shows up |
|---|---|
| Arbitration: exactly one winner out of four competitors | The whole project |
| A flip-flop's Q̄ output is free logic you already own | Section 6, Stage 3 |
| One gate can watch four signals at once | Stage 3 |
| Edge-triggered vs level-triggered — and why it decides fairness | Stage 3 |
| A spare NAND with its inputs tied is an inverter | Stage 3 |
| An unused input goes to + on a NAND, − on a NOR | Rule 4, Stage 3 |
| Propagation delay: gates take time, and you can add it up | Section 3, worksheet |
| Race conditions and metastability | Stage 5 |
| Put the lamp on the loaded output, the logic on the clean one | Section 6 |
| Get one channel right, then repeat it | Stage 4 |

Total build time is about 2 hours, in five stages you can stop between.

---

## Parts

### Chips

| Chip | What it is | Job in the buzzer |
|---|---|---|
| CD4013 × 2 | Dual D-type flip-flop | One one-bit memory per player |
| CD4012 | Dual 4-input NAND | Watches all four memories, plus the free inverter |

### Everything else

| Qty | Part | Notes |
|---|---|---|
| 1 | Red LED | Player 1 |
| 1 | Yellow LED | Player 2 |
| 1 | Green LED | Player 3 |
| 1 | Blue LED | Player 4 — will be the dimmest of the four |
| 1 | White LED | READY, the host's "board is armed" lamp |
| 2 | PN2222 NPN transistor | Buzzer and READY lamp. Flat side toward you: **E – B – C** |
| 1 | Active buzzer | The kind that beeps on its own from DC |
| 5 | Push button (small) | Four players and the host's RESET |
| 4 | 220 Ω resistor | The four player lamps |
| 1 | 330 Ω resistor | The READY lamp |
| 7 | 10 kΩ resistor | Five button pull-downs, two transistor bases |
| 3 | 0.1 µF ceramic ("104") | One across each chip's power pins |
| 1 | 100 µF electrolytic | Across the power rails — **stripe goes to −** |
| 1 | Breadboard | Full-size is comfier; three chips and five buttons need the room |
| ~45 | Jumper wires | Red for +, black for −, colours for signals |

### Power

**4.5 V to 5 V.** Three AA cells, or the MB102 breadboard module set to 5 V. Both chip types
run from 3 V to 18 V. Nothing in this project touches mains electricity.

---

## Rules for not breaking things

1. **Unplug the power before you rewire.** Every time.
2. **All three chips are 14-pin, + on 14 and − on 7.** Notch to the left → pin 1 is
   bottom-left, and pin numbers run anticlockwise.
3. **Never leave an input dangling** — including the SET pins you aren't using.
4. **An unused input goes to whichever rail its gate ignores.** This is a refinement of the
   rule used in Projects 01–04. For a gate you are not using at all, − is fine. For an unused
   input on a gate you *are* using: **AND and NAND → +**, because those gates only care about
   inputs that are 0. **OR and NOR → −**. A NAND with a spare input tied to − is jammed shut
   permanently.
5. **Never wire an output straight to + or −.** That's a short circuit through the chip. Q and
   Q̄ are outputs.
6. **The electrolytic capacitor has a polarity.** The stripe marks the negative leg.
   Backwards, it can pop.
7. **Touch something metal and grounded before you pick up a chip.** Static kills CMOS.
8. If a chip ever feels **warm**, pull the power immediately and check the wiring.

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

### The five buttons

Every button is wired the same way. Use **diagonally opposite legs** — a 4-pin tactile
button has its legs joined in hidden pairs, and diagonal is the one choice that is always
right.

| ✓ | From | To |
|---|---|---|
| ☐ | Button leg | + rail |
| ☐ | Button leg, **diagonally opposite** | its node |
| ☐ | Node | 10 kΩ → − rail |

Five nodes: **P1, P2, P3, P4** and **RESET**. The 10 kΩ pull-downs are not optional —
without them a node is connected to nothing when the button is up, and lamps will latch by
themselves as you move around the room.

### CD4013 number 1 — players 1 and 2

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | pin 14 | + | Power |
| ☐ | pin 7 | − | Ground |
| ☐ | 0.1 µF | between pin 14 and pin 7 | Local smoothing |
| ☐ | pin 6 (SET1) | − | Unused, never floating |
| ☐ | pin 8 (SET2) | − | Unused, never floating |
| ☐ | CD4012 pin 13 | pin 5 (D1) | READY — what a press stores |
| ☐ | CD4012 pin 13 | pin 9 (D2) | READY |
| ☐ | P1 node | pin 3 (CLOCK1) | *When* to store |
| ☐ | P2 node | pin 11 (CLOCK2) | |
| ☐ | RESET node | pin 4 (RESET1) | |
| ☐ | RESET node | pin 10 (RESET2) | |
| ☐ | pin 1 (Q1) | 220 Ω → red LED → − | Player 1's lamp |
| ☐ | pin 13 (Q2) | 220 Ω → yellow LED → − | Player 2's lamp |
| ☐ | pin 2 (Q̄1) | CD4012 pin 2 | "Player 1 is still empty" |
| ☐ | pin 12 (Q̄2) | CD4012 pin 3 | "Player 2 is still empty" |

### CD4013 number 2 — players 3 and 4

Identical, on the other two CD4012 inputs.

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | pin 14 | + | Power |
| ☐ | pin 7 | − | Ground |
| ☐ | 0.1 µF | between pin 14 and pin 7 | |
| ☐ | pins 6 and 8 (both SETs) | − | |
| ☐ | CD4012 pin 13 | pin 5 (D1) | READY |
| ☐ | CD4012 pin 13 | pin 9 (D2) | READY |
| ☐ | P3 node | pin 3 (CLOCK1) | |
| ☐ | P4 node | pin 11 (CLOCK2) | |
| ☐ | RESET node | pins 4 and 10 | |
| ☐ | pin 1 (Q1) | 220 Ω → green LED → − | Player 3's lamp |
| ☐ | pin 13 (Q2) | 220 Ω → blue LED → − | Player 4's lamp |
| ☐ | pin 2 (Q̄1) | CD4012 pin 4 | "Player 3 is still empty" |
| ☐ | pin 12 (Q̄2) | CD4012 pin 5 | "Player 4 is still empty" |

### CD4012 — the lockout and the free inverter

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | pin 14 | + | Power |
| ☐ | pin 7 | − | Ground |
| ☐ | 0.1 µF | between pin 14 and pin 7 | |
| ☐ | pins 2, 3, 4, 5 | the four Q̄ outputs | See the two tables above |
| ☐ | pin 1 | pin 9 | LOCKED into the free inverter |
| ☐ | pin 1 | pin 10 | |
| ☐ | pin 1 | pin 11 | |
| ☐ | pin 1 | pin 12 | |

Pins **6 and 8 are no-connection** — leave them empty. Don't ground them.

Outputs: **pin 1 = LOCKED** (1 when somebody has buzzed), **pin 13 = READY** (1 when nobody
has). READY is the signal every D input reads.

### Output block — Q1, the buzzer

| ✓ | From | To |
|---|---|---|
| ☐ | CD4012 pin 1 (LOCKED) | 10 kΩ → Q1 base (middle leg) |
| ☐ | Q1 emitter (left leg) | − |
| ☐ | Buzzer + (long leg) | + |
| ☐ | Buzzer − | Q1 collector (right leg) |

### Output block — Q2, the READY lamp

| ✓ | From | To |
|---|---|---|
| ☐ | CD4012 pin 13 (READY) | 10 kΩ → Q2 base |
| ☐ | Q2 emitter | − |
| ☐ | + | 330 Ω → white LED long leg |
| ☐ | White LED short leg | Q2 collector |

Both transistors get 10 kΩ because their signals are also being *read* by other chips —
LOCKED by the free inverter, READY by four D inputs. A 10 kΩ into a base draws 0.43 mA, which
leaves those pins sitting at about 4.6 V and comfortably above the 3.5 V a CMOS input needs
to call something a 1.

The four **player** lamps need no transistor, because each hangs on a Q output while the
matching Q̄ output does all the logic. Two separate outputs, two separate jobs.

---

## Why the lamps aren't bright, and why that's the right choice

A CD4013 output pushes about 2½ mA into an LED, which glows rather than blazes. For four
lamps side by side that's enough — you only need to see *which* one changed. The blue LED
will be dimmest because blue needs the most forward voltage.

If you want them bright, give each Q output a 10 kΩ to a transistor base and hang the LED
from + through 330 Ω, exactly like the READY lamp. That costs four transistors, and the kit
has two spare.

---

## The lockout window

When somebody presses, the lockout has to travel all the way round: flip-flop, NAND,
inverter, and back to the other three D inputs. Every step costs time, and the datasheets say
how much at 5 V.

| Step | Chip | Typical | Worst allowed |
|---|---|---|---|
| Button edge → Q̄ drops | CD4013 | 150 ns | 300 ns |
| Q̄ → LOCKED rises | CD4012 | 125 ns | 250 ns |
| LOCKED → READY drops | CD4012 | 125 ns | 250 ns |
| **Total** | | **400 ns** | **800 ns** |

400 nanoseconds is 0.0004 milliseconds. Two people trying their hardest to tie will still be
a couple of milliseconds apart — several thousand times slower. That margin is the whole
reason the device is fair, and it is also why you cannot produce a genuine tie by hand. To
see one, bridge two button nodes with a jumper so a single press arrives at two flip-flops at
once.

---

## Pin reference

Checked against the Texas Instruments datasheets. All three chips: **+ on 14, − on 7**.

```
CD4013  dual D flip-flop           CD4012  dual 4-input NAND
  1 Q1          14 +VDD              in 2, 3, 4, 5  -> out  1
  2 Q1-bar      13 Q2                in 9,10,11,12  -> out 13
  3 CLOCK1      12 Q2-bar            pins 6 and 8: NO CONNECTION
  4 RESET1      11 CLOCK2
  5 D1          10 RESET2          A NAND outputs 0 only when every
  6 SET1         9 D2              input is 1.  Tie all four inputs
  7 -VSS         8 SET2            together and it becomes a NOT gate.

  stores D on the RISING edge of CLOCK
  SET = 1 forces Q = 1, RESET = 1 forces Q = 0, both are level-triggered
  SET and RESET high together drives BOTH outputs high — an illegal state,
  which is why SET is tied to - in this project
```

---

## Troubleshooting

| What you see | Almost always |
|---|---|
| Nothing works at all | Power missing from a chip. Check pin 14 and pin 7 on all three. |
| A lamp is lit at switch-on | Normal. Flip-flops wake up holding random values. Press RESET. |
| Every button does nothing, ever | READY is stuck at 0. Either a CD4012 input is on − instead of + (Stage 3), or a Q̄ wire is missing, or pin 1 isn't jumpered to pins 9–12. |
| All four lamps light together | The D inputs are still on the + rail from Stages 1–2. They belong on CD4012 pin 13. |
| One player never works, the rest do | Their CD4012 input is stuck at 1 — you left a + wire on pin 4 or 5 after Stage 4. |
| One player can buzz even after somebody else won | That flip-flop's D pin isn't reaching READY. |
| A lamp latches by itself when you touch the board | That button node is floating. Its 10 kΩ pull-down is missing. |
| RESET clears three players but not the fourth | The RESET node isn't reaching that reset pin — 4 and 10 on both chips. |
| A player buzzes the instant you press RESET | They are holding their button down. That's supposed to fail — if it succeeds, check that their button goes to a CLOCK pin (3 or 11) and not to a SET pin (6 or 8). |
| Lamp lights but no buzzer | Buzzer polarity, or a passive buzzer instead of the active one. |
| Buzzer never stops | Somebody is still latched — press RESET. If it truly never stops, a Q̄ wire is off and LOCKED is stuck at 1. |
| White READY lamp never lights | Q2 in backwards. Flat side toward you, legs down: E – B – C. |
| Two lamps light on one press | Two button nodes are shorted together, or two CLOCK pins share a node. |
| Everything is wrong at once | Unplug, walk away for five minutes, come back and re-read one table. This is what real engineers do. |

---

## Files

| File | What's in it |
|---|---|
| [`guide.html`](guide.html) | The illustrated guide: five stages, and the buzzer playable in the browser |
| [`worksheet.md`](worksheet.md) | The timing arithmetic, reaction-time experiments, and the race |
| `README.md` | This file — parts, wire lists, pinouts, troubleshooting |
