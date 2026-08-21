# <Project Name>

<One sentence on what it does, written so a 12-year-old wants to build it.>

<Two or three lines on what actually happens when it works — the lights, the sound, the
thing you show someone.>

**Open [`guide.html`](guide.html) in a browser** — that's the real guide, with diagrams and
a working simulator. This file is the bench reference: parts, wire lists, troubleshooting.

---

## What it teaches

| Idea | Where it shows up |
|---|---|
| | |

Total build time is about <N> hours, in <N> stages you can stop between.

---

## Parts

### Chips

| Chip | What it is | Job |
|---|---|---|
| | | |

### Everything else

| Qty | Part | Notes |
|---|---|---|
| | | |

### Power

<Voltage, and what supplies it. State plainly that nothing touches mains.>

---

## Rules for not breaking things

1. **Unplug the power before you rewire.** Every time.
2. **The notch on a chip tells you which end is which.** Notch left → pin 1 bottom-left,
   numbers run anticlockwise. Backwards means pin 14 gets ground and pin 7 gets +5 V; the
   chip cooks.
3. **Never leave an input dangling.** Unused inputs go to −.
4. **Never wire an output straight to + or −.** That's a short through the chip.
5. **Electrolytic capacitors have a polarity.** Stripe marks the negative leg.
6. **Touch something grounded before handling chips.** Static kills CMOS.
7. **Warm chip means stop.** Pull power, check rule 2.

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

### <CHIP> — <its job>

| ✓ | From | To | Meaning |
|---|---|---|---|
| ☐ | pin 14 | + | Power |
| ☐ | pin 7 | − | Ground |
| ☐ | 0.1 µF | between pin 14 and pin 7 | Local smoothing |

---

## Pin reference

Verified against the manufacturer's datasheets.

```
<CHIP>  <description>
 in  1,  2  -> out  3
```

---

## Troubleshooting

| What you see | Almost always |
|---|---|
| Nothing lights at all | Power not reaching pin 14 / pin 7. Check both, on every chip. |
| A chip gets warm | Power in backwards. Unplug now. |
| Lights flicker on their own | A floating input. Tie it to −. |
| An LED never lights | Backwards. Long leg toward +. |
| Everything is wrong at once | Unplug, walk away five minutes, re-read one table. This is what real engineers do. |

---

## Files

| File | What's in it |
|---|---|
| [`guide.html`](guide.html) | The illustrated guide: diagrams, build stages, simulator |
| [`worksheet.md`](worksheet.md) | Tables to fill in by hand, and the challenges |
| `README.md` | This file — parts, wire lists, pinouts, troubleshooting |
