# Starting a new project

Copy this whole folder to `projects/<your-project-name>/`, then work down the checklist.

```bash
cp -r template projects/my-new-project
cd projects/my-new-project
mv project-README.md README.md
```

The folder ends up as `guide.html`, `README.md`, `worksheet.md` — same three files every
project has.

## What's already in the template

`guide.html` is a **working page**, not an empty shell. Open it in a browser before you
change anything and you'll see the design system and the diagram library already running.
It contains:

| Piece | What it gives you |
|---|---|
| CSS design tokens | Light and dark themes, print styles, all the block types (`.note`, `.warn`, `.why`, `.stage`, `ol.steps`) |
| `gateSym(kind, ins)` | Logic-gate symbols: `and`, `or`, `not`, `xor`, `xnor` — proper IEEE shapes with bubbles |
| `dipSVG(chip)` | A DIP chip pinout drawing from a pin table, colour-coded by role |
| `bbSVG()` | The breadboard "how the holes are joined" diagram |
| `truthTable(gate)` | A truth table generated from a JavaScript function, so it can't disagree with reality |

Add a chip to the `CHIPS` array and its pinout diagram draws itself.

## Checklist

1. **Pick the idea before the parts.** A project needs one concept worth understanding and
   one thing that's fun to show off. The Logic Vault is "XNOR asks *are these the same?*"
   plus "a buzzer goes off when you get it wrong".

2. **Verify every pinout against the manufacturer's datasheet.** Not a tutorial, not
   memory — the actual drawing in the actual PDF. TI's are at
   `https://www.ti.com/lit/ds/symlink/<part>.pdf`. Older ones are scanned images, so render
   the page and read it with your eyes:
   ```bash
   curl -sL -o cd4077b.pdf https://www.ti.com/lit/ds/symlink/cd4077b.pdf
   pdftoppm -r 150 -png -f 2 -l 2 cd4077b.pdf pinout   # then open pinout-02.png
   ```
   A wrong pin number costs someone an afternoon and teaches them electronics is unfair.

3. **Check the current budget.** CD4000-series outputs give about 3 mA at 5 V — enough for
   a dim LED, not enough for a buzzer, relay or motor. Anything that needs muscle gets a
   PN2222 and a base resistor. Work this out before you promise "and then it spins".

4. **Write the stages so each one ends somewhere satisfying.** Nobody finishes in one
   sitting. Every stage should leave a circuit that visibly does something.

5. **Say the disappointing parts out loud.** Dim LEDs, a chip that needs inverting, a
   display that's the wrong polarity. Naming it up front turns "it's broken" into "ah, it's
   supposed to look like that".

6. **Test the logic, don't eyeball it.** Extract the scripts and run the truth tables
   against expected values:
   ```bash
   python3 -c "import re,sys; print('\n;\n'.join(re.findall(r'<script>(.*?)</script>', open('guide.html').read(), re.S)))" > /tmp/g.js
   node --check /tmp/g.js
   ```
   Then assert your gate functions and your pin tables in a small harness. If the truth
   tables are generated from the same functions the simulator uses, the guide cannot
   contradict itself.

7. **Look at it rendered, in both themes.** Bugs that only appear visually are real — the
   Logic Vault shipped with every indicator lamp stuck grey, because SVG `fill="…"`
   presentation attributes lose to class CSS. Use inline `style="fill:…"` for state
   colours. On macOS with no browser installed:
   ```bash
   qlmanage -t -s 1400 -o /tmp/out guide.html    # note: QuickLook does not run JS
   ```

8. **Keep `guide.html` self-contained.** Inline CSS and JS, no external requests, no build
   step. Somebody should be able to email the single file to a friend.

9. **Add a row to the root [README](../README.md) table** when it works.

## House style

- Second person, present tense. "Put the chip in", not "the chip should be inserted".
- Never say "simply" or "just". If it were simple they wouldn't need the guide.
- One idea per paragraph. A 12-year-old reading three paragraphs is fine; a 12-year-old
  reading one dense one is not.
- Every wire list is `pin → pin`, never breadboard coordinates, so it works wherever they
  physically put things.
- Give each stage a realistic time. Underestimating is discouraging.
- End stages with a `.why` block: what this idea is actually used for in the real world.
