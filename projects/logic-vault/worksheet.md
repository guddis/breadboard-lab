# The Logic Vault — Worksheet

Print this. Fill it in with a pencil at the bench, not from the internet.

Rule for every table: **1 means the wire is connected to +. 0 means it's connected to −.**
"Light on" is 1. "Light off" is 0.

---

## 1. NOT — CD4069

One input, one output. Put your jumper on pin 1 and watch the LED on pin 2.

| Input | Output |
|:-:|:-:|
| 0 | |
| 1 | |

**In your own words, what does a NOT gate do?**

_________________________________________________

---

## 2. AND — CD4081

Two inputs, pins 1 and 2. Output on pin 3.

| A | B | Out |
|:-:|:-:|:-:|
| 0 | 0 | |
| 0 | 1 | |
| 1 | 0 | |
| 1 | 1 | |

**Finish the sentence:** the output is 1 only when ______________________________

---

## 3. OR — CD4071

Same pins: inputs 1 and 2, output 3.

| A | B | Out |
|:-:|:-:|:-:|
| 0 | 0 | |
| 0 | 1 | |
| 1 | 0 | |
| 1 | 1 | |

**Finish the sentence:** the output is 1 when ________________________________

---

## 4. XOR — CD4070

Same pins again. This one surprises people.

| A | B | Out |
|:-:|:-:|:-:|
| 0 | 0 | |
| 0 | 1 | |
| 1 | 0 | |
| 1 | 1 | |

**Look at your table.** XOR gives 1 when the two inputs are ______________________

---

## 5. XNOR — CD4077

Same pins. Compare this table with the XOR one above.

| A | B | Out |
|:-:|:-:|:-:|
| 0 | 0 | |
| 0 | 1 | |
| 1 | 0 | |
| 1 | 1 | |

**Compare tables 4 and 5. What's the relationship between XOR and XNOR?**

_________________________________________________

**And the big one.** XNOR gives 1 when the inputs are _______________________,
which means an XNOR gate is really a machine that answers the question:

"_______________________________________________?"

---

## 6. NAND — CD4012, and the free inverter

The CD4012 has four inputs on one gate: pins 2, 3, 4, 5. Output is pin 1.
You only need five rows of the sixteen possible ones to see the pattern.

| P2 | P3 | P4 | P5 | Out (pin 1) |
|:-:|:-:|:-:|:-:|:-:|
| 1 | 1 | 1 | 1 | |
| 0 | 1 | 1 | 1 | |
| 1 | 0 | 1 | 1 | |
| 1 | 1 | 0 | 1 | |
| 0 | 0 | 0 | 0 | |

**When is the output 0?** ______________________________________________

Now tie **all four** inputs of the *second* gate (pins 9, 10, 11, 12) to the same wire
and watch pin 13.

| All four inputs | Out (pin 13) |
|:-:|:-:|
| 0 | |
| 1 | |

**What gate did the NAND just turn into?** _______________________________

This trick is why the vault needs only two chips to make both LOCKED and UNLOCKED.

---

## 7. Predict before you look

The vault is built. Before you flip anything, **write down your prediction**, then test it.
Score yourself.

Secret code is set to **1 0 1 1**.

| Dials | Your prediction: match lights | Your prediction: green? | Right? |
|:-:|:-:|:-:|:-:|
| 1 0 1 1 | | | |
| 0 0 1 1 | | | |
| 1 1 1 1 | | | |
| 0 1 0 0 | | | |
| 1 0 1 0 | | | |

---

## 8. Counting

There are four dials, and each one can be 0 or 1.

**a.** How many different codes are possible?

Show your working: ________________________________

**b.** If you guessed codes at random with no clues, what's the *worst* number of tries
you might need? ______________

**c.** What's the *average*? ______________

**d.** Now suppose the four yellow match lights are visible. Someone flips dial 1 and
watches its light, then dial 2, and so on. How many tries do they need now, at worst?

______________

**e.** That's a huge difference. Explain in one sentence why the match lights make the
vault so much weaker:

_________________________________________________

_________________________________________________

> Engineers have a name for this. A **side channel** is when a machine leaks a secret not
> through its front door but through something else you can see, hear or measure — a light,
> a sound, how long it takes, how warm it gets. Real attacks on real bank cards have worked
> exactly this way: not by breaking the maths, but by watching the power supply flicker.

**f.** If you added four more dials, how many codes would there be? ______________

**g.** How many dials would you need to get past a million codes? ______________

---

## 9. The gate-golf challenges

Each of these can be done with the chips in your kit. Sketch the gates, then build it.

**Challenge A — the odd-one-out.**
Three dials. Light an LED only when exactly one of the three is 1.
*Hint: XOR is a good start, but check the case where all three are 1.*

**Challenge B — the majority vote.**
Three dials. Light an LED when two or more of them are 1. This is the circuit inside
voting machines and error-correcting memory.

**Challenge C — the not-quite-XOR.**
Build an XOR gate **without** using the CD4070. You may use AND, OR and NOT.
*Hint: "A and not B, or B and not A."*

**Challenge D — the vault, but backwards.**
Change the vault so the alarm sounds when the code is **right** and stays silent when it's
wrong. How few wires can you change? (There's an answer that changes exactly one.)

**Challenge E — a doorbell for two.**
Light an LED only when both dial 1 and dial 2 are 1, *and* dial 3 is 0.

---

## 10. Notebook

Real engineers write down what went wrong. It's how you stop making the same mistake twice.

**Something that didn't work, and what fixed it:**

_________________________________________________

_________________________________________________

**The thing that surprised me most:**

_________________________________________________

**Something I want to build next:**

_________________________________________________
