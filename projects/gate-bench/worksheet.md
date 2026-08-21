# The Gate Bench — Worksheet

Print this. Fill it in with a pencil at the bench, not from the internet.

Rule for every table: **1 means the wire is connected to +. 0 means it's connected to −.**
"Lamp on" is 1. "Lamp off" is 0.

Fill in each table by trying all four combinations of your two jumpers. Write down what you
*see*, even when you're sure you know what it should be. Twice today, what you see will not
be what you expected — and both times it will teach you something.

---

## 1. AND — CD4081

Inputs on pins 1 and 2, output on pin 3.

| A | B | Out |
|:-:|:-:|:-:|
| 0 | 0 | |
| 0 | 1 | |
| 1 | 0 | |
| 1 | 1 | |

**Finish the sentence:** the output is 1 only when ______________________________

---

## 2. OR — CD4071

Same pins. You changed nothing but the chip.

| A | B | Out |
|:-:|:-:|:-:|
| 0 | 0 | |
| 0 | 1 | |
| 1 | 0 | |
| 1 | 1 | |

**Finish the sentence:** the output is 1 when ________________________________

---

## 3. XOR — CD4070

Same pins again. This is the one that surprises people.

| A | B | Out |
|:-:|:-:|:-:|
| 0 | 0 | |
| 0 | 1 | |
| 1 | 0 | |
| 1 | 1 | |

**a.** Compare this table with table 2. Circle the row where they disagree.

**b.** In one sentence, what question does an XOR gate answer?

_________________________________________________

**c.** "You can have pudding **or** ice cream." Is that an OR or an XOR?  ____________

---

## 4. NAND — CD4011

| A | B | Out |
|:-:|:-:|:-:|
| 0 | 0 | |
| 0 | 1 | |
| 1 | 0 | |
| 1 | 1 | |

**Compare with table 1.** Write down what you notice: __________________________

_________________________________________________

---

## 5. NOR — CD4001

| A | B | Out |
|:-:|:-:|:-:|
| 0 | 0 | |
| 0 | 1 | |
| 1 | 0 | |
| 1 | 1 | |

**Compare with table 2.** Write down what you notice: __________________________

**When is a NOR's output 1?** ______________________________________________

> The little circle on a gate symbol always means the same thing: *work out the answer,
> then flip it.* Once you know that, NAND and NOR stop being two new gates to memorise and
> become two old gates wearing a hat.

---

## 6. NOT — made out of a NAND

Put the CD4011 back and wire the A column to **both** pin 1 and pin 2. Park the B jumper
in −. Now only two things can happen, so this table has two rows.

| A | Out |
|:-:|:-:|
| 0 | |
| 1 | |

**Why does tying both inputs of a NAND together turn it into a NOT?** Use the word "all"
in your answer.

_________________________________________________

_________________________________________________

**Now check it against the real thing.** Wire the CD4069 as in Stage 4 and test it. Does
your home-made NOT behave identically to the bought one?  ____________

---

## 7. The guessing game

Somebody plugs in one of the five quad chips — CD4081, CD4071, CD4070, CD4011, CD4001 —
while you look away. Find out which. Write down each test *before* you do it.

### Round 1

| Test | A | B | Lamp | Chips still possible after this test |
|:-:|:-:|:-:|:-:|---|
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |
| 4 | | | | |

My answer: ______________  Correct? ______  Tests used: ______

### Round 2

| Test | A | B | Lamp | Chips still possible after this test |
|:-:|:-:|:-:|:-:|---|
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |
| 4 | | | | |

My answer: ______________  Correct? ______  Tests used: ______

### Round 3

| Test | A | B | Lamp | Chips still possible after this test |
|:-:|:-:|:-:|:-:|---|
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |
| 4 | | | | |

My answer: ______________  Correct? ______  Tests used: ______

**a.** Which single test rules out the most chips when you know nothing yet? Look at your
five tables and work out which test splits them most evenly.

Best first test: A = ______  B = ______

**b.** Write down how that test splits the five chips.

Lamp off → ________________________  Lamp on → ________________________

**c.** Three tests are always enough. Explain why four are never needed:

_________________________________________________

_________________________________________________

> Each test gives you one bit — the lamp is on, or off. Three bits can tell apart eight
> possibilities, and you only have five chips, so three tests is enough. Two tests could
> only separate four, so three is also the smallest number that always works. Engineers
> call this bounding the problem: knowing the answer *is three* before doing any testing.

---

## 8. Counting

**a.** A gate with two inputs has four rows in its truth table. Each row's output can be 0
or 1. How many different two-input rules are therefore possible?

Show your working: ________________________________

Answer: ____________

**b.** You have chips for AND, OR, XOR, NAND and NOR on the bench, and the CD4077 in the
drawer is XNOR. What fraction of all the possible two-input rules do you own?

____________

**c.** How many rules are possible for a gate with **one** input? Name all of them —
two are useful and two are silly.

_________________________________________________

**d.** How many rows would a truth table for a gate with **eight** inputs have?

____________

---

## 9. Predict before you look

Do this for every chip *before* you test it. Write the prediction first. Score yourself
honestly — a wrong prediction that you wrote down is worth more than a right one you
didn't.

| Chip | Row you predicted | Your prediction | What happened | Right? |
|---|:-:|:-:|:-:|:-:|
| | | | | |
| | | | | |
| | | | | |
| | | | | |
| | | | | |
| | | | | |

Score: ______ out of ______

---

## 10. De Morgan, by hand

In the bonus stage you build an OR gate out of NAND gates by inverting both inputs first.
Fill this in with a pencil before you wire it — no chips needed.

| A | B | NOT A | NOT B | NAND of those two |
|:-:|:-:|:-:|:-:|:-:|
| 0 | 0 | | | |
| 0 | 1 | | | |
| 1 | 0 | | | |
| 1 | 1 | | | |

**Compare the last column with table 2.** What do you notice?

_________________________________________________

Now build it and check that the board agrees with your pencil.

---

## 11. Challenges

Each of these can be built with the chips in your kit and the bench you already have.
Sketch the gates on paper first.

**Challenge A — the gate nobody sold you.**
Light the lamp only when A is 1 **and** B is 0. You'll need a NOT and an AND. Which chips,
and which pins?

**Challenge B — the three-input AND.**
Light the lamp only when three jumpers are all 1. You have four AND gates in the CD4081 and
you only need two of them. How?

**Challenge C — XOR without the CD4070.**
Build an XOR out of AND, OR and NOT gates.
*Hint: "A and not B, or B and not A."*

**Challenge D — the odd one out.**
Three jumpers. Light the lamp when exactly one of them is 1. Check the case where all three
are 1 — most first attempts get that row wrong.

**Challenge E — the alarm panel.**
Three jumpers, each one a sensor. Light a green lamp when **none** of them is 1, and a red
lamp when **any** of them is. Two gates, one chip.

---

## 12. Notebook

Real engineers write down what went wrong. It's how you stop making the same mistake twice.

**Something that didn't work, and what fixed it:**

_________________________________________________

_________________________________________________

**The chip that behaved least like I expected:**

_________________________________________________

**The thing that surprised me most:**

_________________________________________________

**Something I want to build next:**

_________________________________________________
