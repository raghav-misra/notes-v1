# stat400 / 01.25

## course overview.

Topics covered:

- Probability! (chapter 2)
- Discrete random variables & distributions! (chapter 3)
  - Measuring things we can count.
- Continuous random variables & distributions! (chapter 4)
  - Measuring things we can't count.
- Joint probability distributions & random samples (chapter 5)
  - Important: central limit theorem!

## defining probability?

**Probability** is the study of randomness and uncertainty. It provides methods  to quantify likelihoods of outcomes.

The language of probability is all around us; *probably*, *likely*, *there is $x$ chance I do this*, etc. We want to learn how to...

- Interpret probability.
- Compute probability.
- And precisely express informal things in probabilistic terms.

## sample spaces + events.

An **experiment** is any process with an uncertain outcome. (Note: probability can express events that are entirely certain, but it will not help us very much.)

A **sample space**, often denoted $S$, is the set of all possible outcomes of an experiment.

**Find** the sample space of outcomes of a coin toss.

- It has two outcomes: heads or tails.

  **Answer:** sample space $S = \set{H, T}$.

**Find** the sample space of outcomes of rolling a $6$-sided die.

- **Answer:** $S = \set{1, 2, 3, 4, 5, 6}$.

**Find** the sample space of the height of a random human.

- This space is not discrete, as height is a continuous measurement.

  **Answer:** $S = \mathbb{R}^{+}$. While maybe not the most precise sample space, nobody will have heights near $\infin$, it does contain all possible heights.

Mathematically, an **event** is a subset of $S$. There are two types of events:

- A **simple event** contains only one outcome, i.e. it has one element of $S$.
- A **compound event** contains multiple outcomes; it contains multiple elements of $S$.
- The empty set, $\emptyset$, is an event that is neither simple nor compound.

 **Find** the sample space of tossing two coins, where order matters.

- The first coin has space $S_1 = \set{H,T}$.

  The second coin has space $S_2 = \set{H,T}$.

  **Answer:** $S = S_1 \times S_2 = \set{HH, HT, TH, TT}$

**Find** the types of the events $A = \set{HH}$ and $B = \set{HT, TT}$.

- $A$ contains one outcome, $HH$. 

  $B$ contains two outcomes, $HT$ and $TT$. 
  
  **Answer:** $A$ is a simple event; $B$ is a compound event.

The **compliment** of an event $A$, denoted $A^C$, is the set of all outcomes in $S$ that are not in $A$.

The **union** of two events $A$ and $B$, denoted $A \cup B$, is the set of all outcomes that are either in $A$ or in $B$.

The **intersection** of two events $A$ and $B$, denoted $A \cap B$, is the set of all outcomes that are in both $A$ and $B$.

 **For example,** let's roll a die; $S = \set{1, 2, 3, 4, 5, 6}$.

- Let $A = \set{1, 3}$. Therefore, $A^C = \set{2, 4, 5, 6}$.

  Let $B = \set{2}$. Then, $A \cup B = \set{1, 2, 3}$.	

  Let $C = \set{1, 5, 6}$. We can say $A \cap C = \set{1}$. 

  $(A \cup B \cup C)^C = \set{1, 2, 3, 5, 6}^C = \set{4}$.

The **null set** $\emptyset$ (or empty set $\set{}$) is a set that contains no outcomes at all.

If $A, B \sube S$ such that $A \cap B = \emptyset$, then $A$ and $B$ are **disjoint**. In other words, they share no outcomes. There is no outcome in $B$ that is also in $A$, so their intersection set is empty (null).

Events $A_1, A_2, ..., A_k \sube S$ are **pairwise disjoint** if  $\forall (i, j) \in \set{1, 2, ..., k}$,  $(i \neq j \Rightarrow A_i \cap A_j = \emptyset)$. Basically, all of the events $A_1$ through $A_k$ are **disjoint** with each other.

**Venn diagrams** are good visual ways to represent the overlaps of outcomes across events.

- A closed shape represents the outcome set of an event $A$. The complement, $A^C$, would be visually represented by everything outside of  the $A$ shape.

  If we also draw a shape representing event $B$, then $A \cup B$ would be visualized by combining everything inside either shape. To determine $A \cap B$, we would find every event in both shape $A$ and $B$.

