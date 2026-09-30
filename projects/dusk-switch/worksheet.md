# The Dusk Switch — Worksheet

Print this. Fill it in with a pencil at the bench, not from the internet.

This project is more than half measurement. Two rules for all of it:

- **1 means the wire is at +, 0 means it is at −**, as always.
- **Write the prediction down before you look.** A prediction you kept in your head was never
  wrong.

---

## 1. Your own photoresistor

The table in the guide is somebody else's sensor. This is how you find out about yours, with no
multimeter, using the fact that **the divider's middle sits at half the supply when the two
resistances are equal**.

Build Stage 1. Set the light to the level where you want the lamp to switch — the dusk you care
about, or a hand at a particular distance. Then try each fixed resistor and note whether the
indicator LED is clearly bright, clearly dim, or right on the edge.

| Fixed resistor | LED at your chosen light level | So your sensor is… |
|---|---|---|
| 1 kΩ | | |
| 2 kΩ | | |
| 5k1 | | |
| 10 kΩ | | |
| 100 kΩ | | |
| 1 MΩ | | |

**a.** Which resistor put the LED right on the edge — half bright? ______________

**b.** That resistor's value **is your sensor's resistance at that light level**. Write it down;
every later stage uses it: ______________

**c.** Now cover the sensor completely and find the resistor that balances it again:
______________

**d.** And point a torch at it: ______________

**e.** How many times bigger is your "covered" resistance than your "torch" one?

______________ ×  — and that is the whole range your circuit has to work across.

---

## 2. Count the flickers

Stage 2, CD4011 fitted. Move your hand towards the sensor **as slowly as you can bear** and count
how many times the LED changes on the way past. Do it five times.

| Try | Flickers (CD4011) | Flickers (CD4093, Stage 3) |
|:-:|:-:|:-:|
| 1 | | |
| 2 | | |
| 3 | | |
| 4 | | |
| 5 | | |

**a.** Are your five CD4011 numbers the same as each other? ______ What does that tell you about
the cause?

_________________________________________________

**b.** Now with the room light **off** (use a torch from far away instead). More flickers or
fewer? ______________ Why would mains-powered room light make it worse?

_________________________________________________

**c.** Hold your hand still at the distance where it cannot decide. What does the LED do, and for
how long?

_________________________________________________

---

## 3. Measure the hysteresis with a ruler

Stage 3, CD4093 fitted. Move your hand slowly in until the lamp switches **on**, and mark the
distance. Then move it slowly out until the lamp switches **off**, and mark that.

**a.** Lamp ON at ________ cm from the sensor.

**b.** Lamp OFF again at ________ cm.

**c.** The gap: ________ cm.

**d.** Which is further away — the on point or the off point? ______________ Explain why that is
the right way round for a nightlight:

_________________________________________________

**e.** Do the same on the CD4011 (no feedback). How big is the gap? ________ cm. What does that
tell you?

_________________________________________________

---

## 4. Choose your own hysteresis

Stage 4. The gap is **V<sub>DD</sub> × R1 ÷ R2**, with V<sub>DD</sub> = 5 V and R1 = 10 kΩ.

Work out the third column *before* you wire anything:

| R2 | Gap (your calculation) | Prediction | What actually happened |
|---|:-:|---|---|
| 1 MΩ | ________ V | | |
| 100 kΩ | ________ V | | |
| 10 kΩ | ________ V | | |

**a.** Your noise, from part 2, is roughly a tenth of a volt. Which of the three gaps are bigger
than that? ______________

**b.** Which R2 gave the *worst* behaviour, and why is "sometimes fine" worse than "always
broken"?

_________________________________________________

**c.** With R2 = 10 kΩ the gap comes out as the whole supply. Explain, in one sentence, why the
lamp can then never switch off:

_________________________________________________

**d.** What is that circuit now called? (You built two of them in another project.)

______________

**e.** You want a gap of exactly 1 V. With R1 = 10 kΩ, what should R2 be? ______________

Is that value in your kit? ______ Name a combination of kit resistors that gets you there —
there is an answer using five of one value in series, and a neater one using two of another
value in parallel:

______________________________________

---

## 5. Predict before you look

| What you do | Your prediction | What happened | Right? |
|---|---|---|:-:|
| Swap the photoresistor and the fixed resistor over, top for bottom | | | |
| Breathe on the sensor | | | |
| Hold the sensor up to a phone screen showing white | | | |
| Point the Stage 5 white LED straight at the sensor | | | |
| Pull the 104 capacitor out | | | |
| Put the CD4093 in and *also* fit the R2 feedback resistor | | | |

The last one is worth thinking about. Two lots of hysteresis, one inside the chip and one built
from resistors. Does it add up? _________________________________________

---

## 6. The sums

**a.** Your supply is 5 V, the fixed resistor is 10 kΩ and the sensor reads 30 kΩ. What is the
voltage at **S**?

Show your working: ________________________________  Answer: ________ V

**b.** Is that above or below the CD4093's lower threshold of 1.9 V? ______ So is the lamp on or
off? ______

**c.** The CD4093 trips down at 1.9 V and up at 2.9 V. With a 10 kΩ fixed resistor, what sensor
resistance does each of those correspond to?

On at ________ kΩ.  Off at ________ kΩ.

**d.** Divide the bigger by the smaller: ________ ×. The guide says 2.25. Do you agree?

**e.** One 1.5 V cell in your pack goes flat and the supply drops to 3.8 V. The thresholds are
fractions of the supply, so they drop with it. Does the lamp now come on *earlier* or *later* in
the evening? ______________ Explain:

_________________________________________________

---

## 7. Challenges

**Challenge A — the thermistor.**
Pull the photoresistor out and put the thermistor in its place. Nothing else changes.
What is the machine now? ____________________
Squeeze the thermistor between finger and thumb. Does the lamp come on when it gets *hotter* or
*colder*? ______________ How would you swap that round? ____________________

**Challenge B — build the oscillator on purpose.**
Point the Stage 5 white LED at the sensor so the lamp's own light turns itself off.
Blinks per second, with R2 = 100 kΩ: ________  With R2 = 1 MΩ: ________
Which way does more hysteresis push the rate, and why?

_________________________________________________

**Challenge C — count the dusks.**
Feed your output into the Score Tower's count input and leave it in a doorway.
*Do it once with the CD4011 fitted and once with the CD4093.* One shadow gives you how many
counts on each?  CD4011: ________  CD4093: ________
This is the best possible proof that hysteresis is real.

**Challenge D — think, don't build.**
A thermostat should heat to 21 °C and not switch on again until 19.5 °C. Which part of your
circuit sets that 1.5-degree gap, and would you make it bigger or smaller for a room that loses
heat quickly?

_________________________________________________

---

## 8. Notebook

**The thing that surprised me most:**

_________________________________________________

**A measurement I had to do twice, and why:**

_________________________________________________

**The value I ended up choosing for my fixed resistor, and the light level it means:**

_________________________________________________

**Something I want to build next:**

_________________________________________________
