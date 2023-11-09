# probability theory.

## hello.

These notes are in preparation for the course **STAT410** (Introduction to Probability Theory) at the University of Maryland, College Park. However, I doubt the notes will go nearly as in-depth as that class. It's likely more similar in nature to **STAT400** (Applied Probability and Statistics I). The best resource I have found so far to self-study similar topics is MIT OpenCourseWare's [Introduction to Probability](https://ocw.mit.edu/courses/res-6-012-introduction-to-probability-spring-2018/) and this is what I will be basing my notes on. Here's the YouTube [playlist](https://www.youtube.com/playlist?list=PLUl4u3cNGP60hI9ATjSFgLZpbNJ7myAg6) of the lectures.

## sample spaces.

- A **sample space **$\Omega$, which is a set of possible outcomes.

  - Recall a *set* is an unordered list of unique items, or outcomes in this case.
  - $\Omega$ is called the **sample space:** the set containing all the possible outcomes.

- A sample space must meet certain conditions.

  1. **Mutually exclusive:** no two outcomes can both occur simultaneously.
     - A coin cannot flip heads *and* tails at the same time, so the two must be mutually exclusive.
  2. **Collectively exhaustive:** the set must account for all possible outcomes. 
     - For the event of flipping a coin, is $\Omega = \set{\text{heads}}$ a valid sample space?
     - No! If the coin flips to its tails side, the above set does not account for it.
     - A collectively exhaustive sample space would be $\Omega = \set{\text{heads}, \text{tails}}$.
  3. **Granularity:** the set shouldn't contain outcomes that aren't relevant.
     - Would $\Omega = \set{\text{heads/rain}, \text{heads/no rain}, \text{tails/rain}, \text{tails/no rain}}$ be a valid sample space?
     - While technically it is true that it either will rain or will not rain after the coin is flipped, that information is not necessarily relevant to the coin flip and can be removed for a much more *granular* set of $\Omega = \set{\text{heads}, \text{tails}}$.

- A *discrete* sample space can be formed for two rolls of a six-sided die.

  - | Roll #  | 1-1  | 1-2  | 1-3  | 1-4  | 1-5  | 1-6  |
    | ------- | ---- | ---- | ---- | ---- | ---- | ---- |
    | **2-1** | X    | X    | X    | X    | X    | X    |
    | **2-2** | X    | X    | X    | X    | X    | X    |
    | **2-3** | X    | X    | X    | X    | X    | X    |
    | **2-4** | X    | X    | X    | X    | X    | X    |
    | **2-5** | X    | X    | X    | X    | X    | X    |
    | **2-6** | X    | X    | X    | X    | X    | X    |

  - Let the rows be the outcomes of the first roll, and the columns be the outcomes of the second roll.

  - If you find the count up the total cells corresponding to each outcome of the first roll paired with each outcome of the second roll, you get a sample space of $6^2 = 36$ outcomes.

  - In fact, we can write the sample space of both rolls in terms of the sample spaces of the first and the second roll themselves.

    - Let $\Omega_1 = \set{1, 2, 3, 4, 5, 6}$ and $\Omega_2 = \set{1, 2, 3, 4, 5, 6}$ as well.
    - Now we can write $\Omega_{1,2} = \Omega_1 \times \Omega_2$, or the cartesian product of the two sample spaces.
      - Expanded a bit, $\Omega_{1,2} = \set{ (1, 1), (1, 2), \dots, (6, 5), (6, 6)}$. :open_mouth: Wow! 36 specific outcomes mean that $\Omega_{1,2}$ is a **discrete** sample space.

- A *continuous* sample space can be formed for throwing a dart on a board.

  - For the sake of simplicity, let's pretend that the dart must land on the board.
  - Logically, there are an infinite number of exact locations that the dart can land in.
  - Pretend the dartboard is a coordinate plane.
    - We can give the $x$-positions a sample space: $\Omega_x = \set{ x \mid 0 \leq x \leq width}$.
    - Same goes for the y-positions: $\Omega_y = \set{ y \mid 0 \leq y \leq height}$.

  - $\Omega_{xy} = \Omega_x \times \Omega_y$, which contains all possible points in the plane.
    - Thus, there are an infinite number of outcomes, making $\Omega_{xy}$ a **continuous** sample space.

## probability and its axioms.

- Which outcomes are more likely to occur than others?
  - We answer this question by assigning probabilities to each outcome.
- A quick clarification on probabilities for continuous sample spaces.
  - Returning to our dartboard, if we pretend that it is equally likely for the dart to land in any possible space on the board, what is the probability that the dart lands in one specific place?
  - Logically, we would opt for the following formula: $\frac{1}{n}$, where $n$ is the number of outcomes.
    - The issue is that there is an infinite number of outcomes; $\lim_{x \to \infty}\frac{1}{n} = 0$. 
    - So any individual point has a zero probability.
  - Instead of looking at individual outcomes, we can look at subsets of the sample space.
    - Let's take the top half of the board, which would naturally have $\frac{n}{2}$ outcomes. What would the probability of the dart landing in the top half of the board be?
    - Well, $\frac{\frac{n}{2}}{n} = \frac{1}{2}$, which is a number greater than zero! :happy:
- An **event** is the subset of a sample space.
  - Probability is assigned to events.
  - For example, let's say we flip a fair coin; sample space $\Omega = \set{\text{heads}, \text{tails}}$.
    - Let's now say that our event $A = \set{\text{heads}}$.
  - Since the coin has a 50/50 (by cupid) change of landing heads, we can say that $\mathbb{P}(A) = 0.5$. How delightful!
