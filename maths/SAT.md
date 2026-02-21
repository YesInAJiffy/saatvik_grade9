<img width="730" height="309" alt="image" src="https://github.com/user-attachments/assets/335c68c9-c1e9-46d7-a994-dc2aca1ed7d0" />
<img width="810" height="427" alt="image" src="https://github.com/user-attachments/assets/4cb0ba22-9a02-49ad-8d2a-8ea826014a83" />


## Probability

In its simplest form, **probability** is the mathematical measure of how likely an event is to occur. It is the language of uncertainty, helping us turn "maybe" into a specific number.

---

## 1. The Probability Scale

Probability is always expressed as a number between **0 and 1** (or 0% and 100%).

* **0 (0%):** The event is **impossible** (e.g., rolling a 7 on a standard six-sided die).
* **0.5 (50%):** The event is **equally likely** to happen or not happen (e.g., a fair coin flip).
* **1 (100%):** The event is **certain** (e.g., the sun rising tomorrow).

---

## 2. The Basic Formula

To calculate the probability of an event, you divide the number of ways that specific event can happen by the total number of possible outcomes.

### Example: Rolling a Die

If you want to roll an **even number** (2, 4, or 6) on a six-sided die:

* **Favorable outcomes:** 3 (the numbers 2, 4, and 6).
* **Total outcomes:** 6 (the numbers 1, 2, 3, 4, 5, and 6).
* **The Calculation:**  or **0.5**.

---

## 3. Theoretical vs. Experimental

There are two main ways to look at probability:

1. **Theoretical Probability:** What *should* happen based on math. (e.g., "Mathematically, I have a 50% chance of heads.")
2. **Experimental Probability:** What *actually* happens when you run a trial. If you flip a coin 10 times, you might get 7 heads. Your experimental probability was 0.7, even though the theoretical was 0.5.

> **The Law of Large Numbers:** As you perform an experiment more and more times (like flipping a coin 1,000 times instead of 10), the experimental probability gets closer and closer to the theoretical probability.

---

## 4. Why Does It Matter?

Probability isn't just for dice and cards; it’s the engine behind:

* **Insurance:** Calculating the risk of an accident to set premiums.
* **Weather Forecasting:** When a meteorologist says there is a "70% chance of rain."
* **Medicine:** Determining the effectiveness of a new drug in clinical trials.
* **Artificial Intelligence:** Large Language Models (like me!) use probability to predict which word is most likely to come next in a sentence.

---

### Quick Summary Table

| Term | Definition |
| --- | --- |
| **Outcome** | A possible result of an experiment (e.g., landing on "Heads"). |
| **Sample Space** | The set of *all* possible outcomes (e.g., {Heads, Tails}). |
| **Event** | A specific outcome or set of outcomes we are looking for. |
| **Complement** | The probability of the event **not** happening (). |


In probability, we multiply values when we want to find the likelihood of **multiple events happening together**. This is often referred to as the **Multiplication Rule**.

The "trigger word" to look for in word problems is almost always **"AND."**

---

## 1. Independent Events

Events are independent if the outcome of the first one doesn't change the chances of the second one. To find the probability of both occurring, you simply multiply their individual probabilities.

**The Formula:**


### Example: Flipping a Coin and Rolling a Die

What is the probability of flipping **Heads** AND rolling a **4**?

* Probability of Heads: 
* Probability of rolling a 4: 
* **The Calculation:**  (approx. **8.3%**)

---

## 2. Dependent Events (Conditional Probability)

Events are dependent if the first event **changes the pool of options** for the second event. This usually happens in "without replacement" scenarios.

**The Formula:**



*(Where  is the probability of B happening **given** that A already happened.)*

### Example: Drawing Marbles from a Bag

Imagine a bag with **3 Red** marbles and **7 Blue** marbles (10 total). You want to draw two Red marbles in a row **without** putting the first one back.

* **First Draw:** The chance of Red is .
* **Second Draw:** Now there are only 9 marbles left, and only 2 are Red. The chance is .
* **The Calculation:**  (approx. **6.7%**)

---

## Summary Table: When to Multiply vs. Add

| Scenario | Keyword | Operation | Logic |
| --- | --- | --- | --- |
| **Combined Events** | "AND" | **Multiply** | I need both A and B to happen. (Narrower odds) |
| **Alternative Events** | "OR" | **Add** | I'm happy if either A or B happens. (Broader odds) |

---

> **A Quick Tip:** If you multiply two probabilities (which are fractions), your result gets **smaller**. This makes sense: it is much harder to win two games in a row than it is to win just one!

In probability, we **add** when we are looking for the likelihood of **either** one event **or** another event occurring.

The "trigger word" to look for in word problems is almost always **"OR."**

---

## 1. Mutually Exclusive Events

Events are **mutually exclusive** if they cannot happen at the same time. If one happens, the other is impossible in that same moment.

* **The Logic:** If you roll a single die, you can't roll a "2" and a "5" simultaneously.
* **The Formula:** 


### Example: Rolling a Die

What is the probability of rolling a **2** OR a **5**?

* Probability of a 2: 
* Probability of a 5: 
* **The Calculation:**  (approx. **33.3%**)

---

## 2. Non-Mutually Exclusive Events

Events are **non-mutually exclusive** if there is an "overlap"—a scenario where both things could happen at once. If you just add them normally, you'll be double-counting that overlap.

* **The Logic:** If you pull a card from a deck, it could be a **Heart**, or it could be a **King**. But one card is both (the King of Hearts).
* **The Formula:** 


### Example: Drawing a Card

What is the probability of drawing a **Heart** OR a **King**?

* Probability of a Heart: 
* Probability of a King: 
* The Overlap (King of Hearts): 
* **The Calculation:**  (approx. **30.7%**)

---

## The "Golden Rule" Comparison

| Goal | Keyword | Operation | Effect on Probability |
| --- | --- | --- | --- |
| **Combined** (Both) | **AND** | **Multiply** | Probability gets **smaller** (harder to achieve) |
| **Alternatives** (Either) | **OR** | **Add** | Probability gets **larger** (easier to achieve) |

---

> **Pro Tip:** If your addition results in a probability greater than **1** (or 100%), you’ve likely forgotten to subtract the overlap! Probability can never exceed 1.
