# stat400 / exam01

## sample spaces and events.

A **sample space** $\mathcal{S}$ is the set of all possible outcomes of an experiment.

Consider flipping a coin. Logically, $\mathcal{S} = \{H, T\}$.

An **event** is a subset of the sample space. 

- An event is **simple** if it consists of just one outcome.
- It is **compound** if it consists of multiple outcomes.

Common set theory notation:

- The union of events $A$​ and $B$​, denoted $A \cup B$​, contains all outcomes that are either in $A$​ or $B$​.
- The intersection of events $A$ and $B$, denoted $A \cap B$, contains outcomes in both $A$ and $B$​.
- The complement of $A$, denoted $A^C$, contains all outcomes in $\mathcal{S}$ that aren't in $A$.

We denote the **null event** with $\emptyset$ (called the empty set). It is the event that contains no outcomes.

For any event $A$,

- $A \cup \emptyset = A$.
- $A \cap \emptyset = \emptyset$.

If $A \cap B = \emptyset$, then we say that events $A$ and $B$ are **disjoint**, or mutually exclusive, i.e. they have no common outcomes.

## axioms, interpretations, and properties of probability.

Consider the following basic axioms of probability:

1. For any event $A$, $\mathbb{P}(A) \geq 0$​.
   1. All probabilities of non-negative.
2. The probability of sample space, $\mathbb{P}(\mathcal{S}) = 1$​.
   1. Some outcome in the sample space will definitely occur.
3. If $A$ and $B$ are **disjoint**, then $\mathbb{P}(A \cup B) = \mathbb{P}(A) + \mathbb{P}(B)$.
4. If events $A_1, A_2, ...A_k$ are an finite or countably infinite collection of disjoint events, then

$$
\mathbb{P}(A_1 \cup A_2 \cup...\cup A_k) = \sum_{i = 0}^{k} \mathbb{P}(A_i)
$$

**Proof:** $\mathbb{P}(\emptyset) = 0$.

- Consider the infinite collection of events.
  $$
  A_1 = \emptyset, A_2 = \emptyset, A_3 = \emptyset, ...
  $$
  Since $\emptyset \cap \emptyset = \emptyset$, all events $A_i$ are pairwise disjoint. As a result, from axiom 3 above, 
  $$
  \mathbb{P}(\bigcup_{i = 0}^{\infty} A_i = \emptyset) = \sum_{i=0}^{\infty}\mathbb{P}(\emptyset)
  $$
  The union of two events can only be $\emptyset$ if both events are $\emptyset$ themselves. As such, $\mathbb{P}(\emptyset) = 0$.

  $\blacksquare$

**Proof:** $\mathbb{P}(A) + \mathbb{P}(A^C) = 1$.

- By definition of the complement, $A$ and $A^C$ are **disjoint** events, such that $A \cup A^C = \mathcal{S}$. By axiom 3, $\mathbb{P}(A) + \mathbb{P}(A^C) = \mathbb{P}(A \cup A^C) = \mathbb{P}(\mathcal{S}) = 1$.

  $\blacksquare$

**Proof:** $\mathbb{P}(A) \leq 1$.

- Previously, we proved that $\mathbb{P}(A) + \mathbb{P}(A^C) = 1$. By axiom 1, the least possible value for $\mathbb{P}(A^C)$ must be $0$. If we let $\mathbb{P}(A^C) = 0$, it follows that $\mathbb{P}(A) = 1$, which must be its maximum value, as the probability of $A^C$ cannot be less than $0$. In other words, for all events $A$, $\mathbb{P}(A) \leq 1$.

  $\blacksquare$

**Proof:** for any two events $A$ and $B$, $\mathbb{P}(A \cup B) = \mathbb{P}(A) + \mathbb{P}(B) - \mathbb{P}(A \cap B)$.

- **Omitted.**

## counting techniques.

An ordered subset is called a **permutation.** The number of $k$-length permutations from a set of size $n$ is
$$
P_{k, n} = \frac{n!}{(n - k)!}
$$
An unordered subset is a **combination**. The number of $k$-length combinations from a set of size $n$ is
$$
\binom{n}{k} = \frac{P_{k, n}}{k!} = \frac{n!}{k!(n - k)!}
$$
The reason we divide the number of permutations by $k!$ is to remove repeatedly counting various orderings of a given combination; order doesn't matter for combinations.

## conditional probability.

Consider the probability of event $A$ *given* that event $B$ has already occurred. For any two events $A$ and $B$ (where $\mathbb{P}(B) > 0$), the conditional probability of $A$ given $B$ has occurred is described by:
$$
\mathbb{P}(A|B) = \frac{\mathbb{P}(A \cap B)}{\mathbb{P}(B)}
$$
The above expression is also often arranged as the **multiplication rule**, or:
$$
\mathbb{P}(A|B) \cdot \mathbb{P}(B) = \mathbb{P}(A \cap B)
$$
This rule is useful for the case when we are looking for $\mathbb{P}(A \cap B)$ and already have the values of  $\mathbb{P}(A|B)$ and $\mathbb{P}(B)$​.

Consider the **law of total probability**: if $A_1, ..., A_k$ are disjoint and exhaustive (their union is $\mathcal{S}$), then for any other event $B$:
$$
\mathbb{P}(B) 
= \sum_{i = 1}^{k} \mathbb{P}(A_i \cap B)
= \sum_{i = 1}^{k} \left[\mathbb{P}(B | A_i) \cdot \mathbb{P}(A_i)\right]
$$
Perhaps the most important formula to determine conditional probabilities is **Bayes' Theorem**, built upon the multiplication rule and law of total probability. If $A_1, ..., A_k$ are disjoint and exhaustive, then for any other event $B$:
$$
\mathbb{P}(A_j|B) 
= \frac{\mathbb{P}(A_j \cap B)}{\mathbb{P}(B)}
= \frac{\mathbb{P}(B|A_j) \cdot \mathbb{P}(A_j)}{\sum_{i=1}^{k} \left[\mathbb{P}(B | A_i) \cdot \mathbb{P}(A_i)\right]}
$$

## independence.

Two events $A$ and $B$ are **independent** if $\mathbb{P}(A | B) = \mathbb{P}(A)$​. Otherwise, they are **dependent**. More intuitively, if one of the events has a bearing on the other's outcome, then they are dependent.

Using the multiplication rule, $\mathbb{P}(A | B) = \mathbb{P}(A)$ *if and only if* $\mathbb{P}(B | A) = \mathbb{P}(B)$​. 

Also using the multiplication rule, we find that two events $A$ and $B$ are independent *iff*
$$
\mathbb{P}(A \cap B) = \mathbb{P}(A) \cdot \mathbb{P}(B)
$$
The above provides a notion of independences for two events. Events $A_1, A_2, ..., A_k$ are **mutually independent** if the probability of the intersection of any subset of $\{A_i | 1 \leq i \leq k \}$ is equal to the product of the probabilities of each event in the subset.

## random variables.

A **random variable** is a relation with domain $\mathcal{S}$ and range $\mathbb{R}$​.

**Bernoulli random variables** are those with possible values of 0 and 1.

There are two primary types of random variables: discrete and continuous. This exam only covers discrete random variables. A **discrete random variable** has possible values that are finite or *countably* infinite. 

## probability distributions for discrete random variables.

While a random variable can have any real possible values, the maximum probability of an outcome is still 1. The **probability distribution** of a random variable $X$ gives the probability of $X$ taking on a specific value. It is represented using a **probability mass function**, or **pdf**, of the following format:
$$
\mathbb{P}(X = x) = \text{$x$-dependent function that returns a probability.}
$$
The **cumulative distribution function**, or **cdf**, of random variable $X$ is essentially the probability that $X \leq$ some $x$. It is written as:
$$
\mathbb{F}(x) = \mathbb{P}(X \leq x)
$$

## practice midterm.

**Question 1 (2/2):** Suppose the events A, B, C and D are pairwise disjoint. Which of the following statements is true (bold them)?

- Two of the four events can occur simultaneously.
- Three of the four events can occur simultaneously.
- All four events can occur simultaneously.
- **None of the other answers are true.**

**Question 2:** An academic department has just completed voting by secret ballot for a department head. The ballot box contains three slips with votes for candidate $A$ and two slips with votes for candidate $B$​. Suppose these slips are removed from the box one by one.

- **A:** List all possible outcomes.
  - **AAABB, AABAB, AABBA, ABBAA, ABAAB, ABABA,** 
  - **BABAA, BAAAB, BAABA, BBAAA**
- **B:** Suppose a running tally is kept as slips are removed. For what outcomes does $A$ remain (strictly) ahead of $B$​ throughout the tally? 
  - **AAABB, AABAB**

**Question 3:** Suppose that we flip a fair coin twice. Which of the following events are independent?

- $\{HH\}$ and $\{TT\}$ (independent/**dependent**)
  - If $A$ happens, $B$ definitely can't happen.
- $\{HT, TH\}$ and $\emptyset$​ (**independent**/dependent)
  - All are independent with $\emptyset$.
- $\{HH, HT, TH, TT\}$ and $\{HH, TT\}$​ (**independent**/dependent)
  - $A$ always happens anyways, it's sample space.
- $\{HH, HT, TH\}$ and $\{HT, TH, TT\}$​ (independent/**dependent**)
  - If $A$ happens, the likelihood of $B$ is different than if $A$​ was not considered at all.

**Question 4:** An oil exploration company currently has two active projects, one in Asia and the other in Europe. Let $A$ be the event that the Asian project is successful and $B$ be the event that the European project is successful. Suppose that $A$ and $B$ are independent events with $\mathbb{P}(A) = 0.4$ and $\mathbb{P}(B) = 0.7$​.

- **A:** If the Asian project is not successful, what is the probability that the European project is also not successful?

  - Since the two events are independent, the outcome of $A$ has no bearing on the outcome of $B$. As a result, the probability that the European project is not successful is:

  $$
  \mathbb{P}(B^C) = 1 - \mathbb{P}(B) = 1 - 0.7 = 0.3
  $$

- **B:** What is the probability that at least one of the two projects will be successful?

  - We want to determine $\mathbb{P}(A \cup B)$.
  - To do so, we can use the law of total probability as follows:

  $$
  \begin{align*}
  	\mathbb{P}(A \cup B) 
  	&= 
  		\mathbb{P}((A \cup B) | A) \cdot \mathbb{P}(A) + 
  		\mathbb{P}((A \cup B) | A^C) \cdot \mathbb{P}(A^C) \\
      &= (1)(0.4) + (0.7)(0.6) \\
      &= 0.82
  	
  \end{align*}
  $$

- **C:** Given that at least one of the two projects is successful, what is the probability that only the Asian project is successful?

  - We want to determine $\mathbb{P}((A \cap B^C) | (A \cup B))$.
  - We will apply Bayes' Theorem:

  $$
  \begin{align*}
  \mathbb{P}((A \cap B^C) | (A \cup B)) 
  &= \frac{\mathbb{P}((A \cup B) | (A \cap B^C)) \cdot \mathbb{P}(A \cap B^C)}{\mathbb{P}(A \cup B)} \\
  &= \frac{(1)(0.4)(0.3)}{(0.82)} \\
  &\approx 0.146
  \end{align*}
  $$

**Question 5:** Which of the following is (surely) an example of a discrete random variable?

- The height of a random individual.
- The temperature on a random day.
- **The number of heads obtained in three fair coin tosses.**
- The time it takes a random runner to complete a marathon.

**Question 6:** A concrete beam may fail either by shear (S) or flexure (F). Suppose that three failed beams are randomly selected and the type of failure is determined for each one. Let $X$ be the number of beams among the three selected that failed by shear.

- **A:** List each outcome in the sample space along with the associated value of $X$​.
  - Assuming that the order of failure doesn't matter,
  - SSS ($X = 3$), SFS ($X = 2$), FFS ($X = 1$), FFF ($X = 0$).
- **B:** Suppose that 90% of all failed concrete beams failed by shear. Determine the probability function of $X$​ when the failing beams are assumed to be independent. 
  - $\mathbb{P}(X = x) = (0.9^{x})(0.1^{3 - x})$. **BINOMIAL NOT COVERED YET.**
  - **More applicable answer:**
    - For $X = 0$, no beams failed by shear, all beams failed by flexure. Probability is $(0.1)^3 = 0.001$, as all 3 beams saw the same outcome.
    - For $X = 1$, one beam failed by shear, two failed by flexure. There are $\binom{3}{2} = 3$ combinations of beams such that this can happen. As such, the probability is $3(0.9)^2(0.1)^1 = 0.243$​.
    - For $X = 2$, two beams failed by shear, one by flexure. There are $\binom{3}{1} = 3$ combinations of beams such that this can occur. As such, the probability is $3(0.9)^1(0.1)^2 = 0.027$.
    - For $X = 3$, all three beams failed by shear. As such, the probability is $(0.9)^3 = 0.729$, as all 3 beams saw the same outcome.