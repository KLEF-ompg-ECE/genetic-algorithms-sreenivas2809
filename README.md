# Assignment 2 — Genetic Algorithm: Knapsack Problem
## Observation Report

**Student Name  :** Sreenivas Sreeramadas  
**Student ID    :** 2310040078
**Date Submitted:** 20-03-2026

---

## How to Submit

1. Run each experiment following the instructions below
2. Fill in every answer box — do not leave placeholders
3. Make sure the `plots/` folder contains all required images
4. Commit this README and the `plots/` folder to your GitHub repo

---

## Before You Begin — Read the Code

Open `ga_knapsack.py` and read through it. Then answer these questions.

**Q1. What does the `fitness()` function return? Why does an overweight solution score 0?**

```
The fitness() function returns the total value of all the items packed in the knapsack. If the total weight exceeds the maximum allowed weight (MAX_WEIGHT), it scores 0 to penalize invalid solutions so they die off and have no chance of being selected for reproduction.
```

**Q2. What does `tournament_select()` do? Why are higher-fitness individuals more likely to be chosen?**

```
It randomly picks 'k' candidates from the population and returns the one with the highest fitness. Higher-fitness individuals are more likely to be chosen because when they are pitted against others in the tournament, their superior fitness guarantees a win in that specific random matchup.
```

**Q3. Look at the `run_ga()` loop. Find this line:**
```python
next_gen = [best_chromosome[:]]
```
**What is this doing? Why is it important to always keep the best solution?**

```
This implements "elitism" by copying the absolute best solution from the current generation directly into the next generation. It is important because it guarantees that the best solution found so far is never lost due to random, potentially negative crossover or mutation operations.
```

---

## Experiment 1 — Baseline Run

**Instructions:** Run the program without changing anything.
```bash
python ga_knapsack.py
```

**Fill in this table:**

| Metric | Your result |
|--------|-------------|
| Number of generations | 50 |
| Best value at generation 1 |60 |
| Final best value | 77|
| Total weight of best solution (kg) |14.4 |
| Is solution valid (Yes / No) | Yes |

**Copy the printed packing list here:**
```
[ PASTE PACKING LIST OUTPUT HERE ]
``` Best Packing List
--------------------------------------
  + Water bottle
  + First aid kit
  + Sleeping bag
  + Torch
  + Energy bars (x6)
  + Rain jacket
  + Map & compass
  + Cooking stove
  + Rope (10 m)
  + Sunscreen
  + Power bank
--------------------------------------
  Weight : 14.4 / 15.0 kg
  Value  : 77
  Valid  : Yes

**Look at `plots/experiment_1.png` and describe what you see (2–3 sentences).**  
*Where does the biggest improvement happen? Does the curve flatten at some point?*
```
[ YOUR OBSERVATION ]
```
The biggest improvement happens very early on, roughly within the first 10-15 generations. After that rapid climb, the curve flattens out entirely as the algorithm hones in on an optimum and no better mutations are easily discovered.
---

## Experiment 2 — Effect of Mutation Rate

**Instructions:** In `ga_knapsack.py`, find the `# EXPERIMENT 2` block in `__main__`.  
Copy it three times and run with `mutation_rate` = **0.01**, **0.05**, and **0.30**.  
Save plots as `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`.

**Results table:**

| mutation_rate | Final best value | Weight (kg) | Valid? | Shape of curve |
|--------------|-----------------|-------------|--------|----------------|
| 0.01         | 75              | 14.9        | Yes    | Flattens early, stuck low |
| 0.05         | 77              | 14.4        | Yes    | Steady early climb, flattens |
| 0.30         | 78              | 14.1        | Yes    | Random/erratic jumps, luck-based |

**Compare the three plots. What happens when mutation is too low? Too high? (3–4 sentences)**  
*Hint: Too low = no diversity, may get stuck. Too high = random search. What is the sweet spot?*
```
[ YOUR OBSERVATION ]
```
When the mutation rate is too low (0.01), there is very little genetic diversity, causing the algorithm to converge and flatten out prematurely on a suboptimal solution. When it is too high (0.30), the algorithm acts like a random search, which means it struggles to systematically build on good traits and instead relies on luck combined with elitism. A balanced mutation rate (0.05) is the sweet spot because it introduces enough diversity to escape local optima while allowing good traits to successfully propagate.

**Which mutation_rate gave the best result? Why do you think that is?**
```
[ YOUR ANSWER ]
```
Interestingly, the 0.30 mutation rate found the highest final value (78) in this specific run. However, this is largely an artifact of elitism working with a random search: the system essentially made millions of random guesses, and once it randomly stumbled into a great solution, elitism locked it in forever.
---

## Summary

**Complete this table with your best result from each experiment:**

| Experiment | Key setting | Final value | Main finding in one sentence |
|------------|-------------|-------------|------------------------------|
| 1 — Baseline | mutation_rate = 0.05 | 77 | A balanced genetic algorithm rapidly optimizes the knapsack loading. |
| 2 — Mutation rate | mutation_rate = 0.30 | 78 | Mutation scaling is key; 0.05 is consistent, but 0.30 got a lucky hit because of elitism. |

**In your own words — what is the most important thing you learned about Genetic Algorithms from these experiments? (3–5 sentences)**
```
[ YOUR REFLECTION ]
```
The most important thing I learned is how critical the balance between exploration and exploitation is in Genetic Algorithms. Crossover allows us to combine good existing traits, while mutation ensures we don't get stuck in local optima by maintaining diversity. Furthermore, elitism is an incredibly powerful tool—without it, higher mutation rates would continuously destroy the best solutions, but with it, the algorithm is strictly monotonic over generations.
---

## Submission Checklist

- [x] Student name and ID filled in
- [x] Q1, Q2, Q3 answered
- [x] Experiment 1: table filled, packing list pasted, plot observation written
- [x] Experiment 2: results table filled (3 rows), observation and answer written
- [x] Summary table completed and reflection written
- [x] `plots/` contains: `experiment_1.png`, `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`
