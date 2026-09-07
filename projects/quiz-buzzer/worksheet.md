# The Quiz Buzzer — Worksheet

Print this. Fill it in with a pencil at the bench, not from the internet.

Rule for every table: **1 means the wire is connected to +. 0 means it's connected to −.**
"Lamp on" is 1. "Lamp off" is 0.

---

## 1. One flip-flop, by hand

Stage 1 only, before the lockout exists. Watch the lamp on pin 1.

| What you do | Lamp after |
|---|:-:|
| Switch on, touch nothing | |
| Press player 1, let go | |
| Wait ten seconds | |
| Press player 1 again | |
| Press RESET, let go | |
| Hold player 1 down, then press RESET, then release both | |

**Why does the last row leave the lamp off, when player 1's button was definitely pressed?**

_________________________________________________

---

## 2. The lockout gate

The four Q̄ wires go into one 4-input NAND. Fill in what it does. Remember a NAND outputs 0
**only** when every input is 1.

| Q̄1 | Q̄2 | Q̄3 | Q̄4 | LOCKED (pin 1) | READY (pin 13) |
|:-:|:-:|:-:|:-:|:-:|:-:|
| 1 | 1 | 1 | 1 | | |
| 0 | 1 | 1 | 1 | | |
| 1 | 0 | 1 | 1 | | |
| 0 | 0 | 1 | 1 | | |

**a.** Which row means "nobody has buzzed yet"? ______________

**b.** Which row means "two people buzzed"? ______________

**c.** Does the gate tell you *who* buzzed? ______________

**d.** So how does each player's lamp know it was them?

_________________________________________________

---

## 3. Unused inputs

In Stage 3 you have only two players, so two of the NAND's inputs are spare and you tie them
to **+**.

**a.** What would happen if you tied them to − instead? Work it out from the NAND rule
before you try it.

_________________________________________________

**b.** Try it. What actually happened? ______________

**c.** If the lockout gate had been a **NOR** instead of a NAND, which rail would the spare
inputs go to? ______________

**d.** Write the rule in your own words:

_________________________________________________

---

## 4. Add up the lockout time

Every gate takes time. These are the datasheet figures at 5 V — copy them from the guide,
then add them up yourself.

| Step | Chip | Typical (ns) | Worst allowed (ns) |
|---|---|:-:|:-:|
| Button edge → Q̄ drops | CD4013 | | |
| Q̄ → LOCKED rises | CD4012 | | |
| LOCKED → READY drops | CD4012 | | |
| **Total** | | | |

**a.** Convert your typical total to milliseconds. (1 ms = 1 000 000 ns.)

______________ ms

**b.** A very good human reaction time is 200 ms. How many times longer is that than your
answer to (a)?

Show your working: _________________________________________________

**c.** Two people trying to press at exactly the same moment manage about 2 ms apart. How
many times longer is *that* than the lockout?

______________

**d.** Finish the sentence: the buzzer is fair because ______________________________

_________________________________________________

---

## 5. Try to force a tie

Twenty rounds with a friend, counting down "three, two, one, press".

| Round | Who won | Two lamps? |
|:-:|:-:|:-:|
| 1–5 | | |
| 6–10 | | |
| 11–15 | | |
| 16–20 | | |

**How many times out of twenty did two lamps light?** ______________

**Were you surprised?** ______________

Now bridge the P1 and P2 button nodes with a jumper wire and press once.

**What happened?** _________________________________________________

**Why did the machine allow it this time?**

_________________________________________________

---

## 6. Which is faster — you, or a gate?

Take your typical lockout total from exercise 4. Light travels about 30 cm in one nanosecond.

**a.** How far does light travel during your whole lockout window?

______________ metres

**b.** Sound travels about 340 metres per second. How far does sound travel in the same time?

______________ (a useful unit here is millimetres)

**c.** Which is the better description of what "instant" means in this circuit — faster than
light can cross a room, or faster than sound can cross a grain of rice?

_________________________________________________

---

## 7. Predict before you unplug

Each row removes exactly one wire from a finished, working buzzer. Predict first, then try
it, then put the wire back.

| Wire removed | Your prediction | What actually happened |
|---|---|---|
| CD4012 pin 13 → CD4013 pin 5 (player 1's D) | | |
| CD4013 pin 2 → CD4012 pin 2 (player 1's Q̄) | | |
| CD4012 pin 1 → pin 9 (one of the four inverter ties) | | |
| Player 3's 10 kΩ pull-down | | |
| RESET node → CD4013 pin 10 | | |

**Which of those five faults would be hardest to find if somebody else had made it, and
why?**

_________________________________________________

---

## 8. Challenges

**A. Three players.** You have four flip-flops but only want three players. What do you do
with the fourth flip-flop's Q̄ so the other three still work? (There are two right answers —
find both.)

_________________________________________________

**B. Eight players.** What would you need? The CD4012's gate has four inputs, so what does
the lockout gate become? Sketch it.

_________________________________________________

**C. The host's lockout.** Add a button that stops anybody buzzing until the host has
finished reading the question. Where does it go, and what does it interrupt?

_________________________________________________

**D. Second place.** Could this machine remember who was *second*? Explain what extra
information you would have to store, and why one flip-flop per player isn't enough.

_________________________________________________

**E. The illegal state.** The CD4013 datasheet says that if SET and RESET are both 1, then Q
and Q̄ are **both 1** — which is impossible for a thing called "Q and not-Q". In this project
SET is tied to −, so it never happens. Explain what would go wrong with the lockout if it
did.

_________________________________________________
