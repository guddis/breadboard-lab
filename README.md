# Breadboard Lab

Electronics projects for kids who want to know how computers actually work — built from
loose chips on a breadboard, not from modules that hide the interesting part.

Every project is self-contained: an illustrated guide you can follow without knowing
anything first, a bench sheet with the wire lists, and a worksheet with tables to fill in
by hand. No microcontroller, no code, no app. The circuit *is* the explanation.

## Projects

| Project | Topic | Age | Time | Chips |
|---|---|---|---|---|
| [Gate Bench](projects/gate-bench/) | The six logic gates, one at a time | 11+ | 1½–2 h | CD4081, CD4071, CD4070, CD4011, CD4001, CD4069 |
| [Logic Vault](projects/logic-vault/) | Logic gates, comparators, side channels | 12+ | 2–3 h | CD4077, CD4012, CD4081 |
| [Reaction Machine](projects/reaction-machine/) | Clocks, counting, one bit of memory | 10–12 | 2–2½ h | CD40106, CD4017, CD4013, CD4081 |
| [Siren Box](projects/siren-box/) | Frequency, sound, one circuit driving another | 10–12 | 1½–2 h | CD40106, CD4066 |
| [Quiz Buzzer](projects/quiz-buzzer/) | Arbitration, race conditions, propagation delay | 10–12 | 2 h | CD4013 × 2, CD4012 |
| [Score Tower](projects/score-tower/) | Decoding, seven-segment displays, carry | 10–12 | 2½ h | CD4026 × 2, CD4069 × 3 |

The projects are in order. The **Gate Bench** introduces the six logic gates one chip at a
time, and the **Logic Vault** puts them to work. Both are combinational — they answer
instantly and forget instantly. The **Reaction Machine** breaks out of that: it makes its
own beat, counts, and remembers. The **Siren Box** takes that same beat and runs it a
thousand times faster, until you can hear it. The **Quiz Buzzer** is the one you'll keep on
the shelf: four players, one winner, decided in less than a millionth of a second. The
**Score Tower** keeps that game's score — and is the first one here that counts in digits you
can read instead of lamps you have to add up.

Open a project's `guide.html` in any browser — that's the real guide, with diagrams and a
working simulator you can play with before touching a wire. The `README.md` beside it is
the bench reference you keep open while building.

## How each project is laid out

```
projects/<name>/
├── guide.html      the illustrated guide — diagrams, build stages, live simulator
├── README.md       bench reference: parts, complete wire list, pinouts, troubleshooting
└── worksheet.md    truth tables to fill in, counting exercises, extension challenges
```

`guide.html` is deliberately a **single self-contained file** — all CSS and JS inline, no
external requests, no build step. You can email one file to someone, open it on a tablet
with no internet, or print it. The cost is that the styling is duplicated per project
rather than shared; see [template/README.md](template/README.md) for how to keep new
projects consistent.

## Starting a new project

Copy [`template/`](template/) into `projects/<your-name>/` and work through the checklist
in [template/README.md](template/README.md). The template's `guide.html` already contains
the design system and a small library of SVG generators — logic-gate symbols, DIP chip
pinouts, breadboard diagrams — so a new guide starts with working diagrams rather than a
blank page.

## Design principles

These are what make the guides work for a 12-year-old, and they're worth keeping:

- **Play before build.** Every guide opens with a simulator of the finished circuit. Seeing
  it work is what makes someone want to wire it.
- **Explain the *why*, not just the steps.** Each stage ends with a note on what the idea
  is actually for — real engineers, real chips, real consequences.
- **Never hide a disappointment.** If the LEDs will be dim because a 1968 CMOS chip can
  only push 3 mA, say so before they see it and think they broke something.
- **One idea per stage, stoppable.** Nobody finishes a 3-hour build in one sitting.
- **Verify the pinouts against the datasheet.** Every pin number in this repo was read off
  the manufacturer's own drawing. A wrong pin number wastes an afternoon and teaches
  someone that electronics is unfair.

## Safety

Everything here runs from 3 AA cells or a 5 V breadboard supply. Nothing goes near mains
electricity. The realistic hazards are a hot chip from reversed power and a popped
capacitor from reversed polarity — both covered in each project's rules section, and
neither dangerous to a person.

An adult should sit in for the first hour of a child's first build, mostly to enforce
"unplug the power before you rewire".

## Licence

[MIT](LICENSE) — use these with your own kids, your class, or your club. If you fix an
error or build a variation, a pull request is welcome.
