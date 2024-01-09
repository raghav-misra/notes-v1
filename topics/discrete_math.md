# discrete math.

## hello.

These notes go over the vast majority of the content of the course **CMSC250** (Discrete Structures) at the University of Maryland, College Park. It probably also contains stuff not covered in the class, and probably misses smaller details covered in the course. (I haven't taken the class; tested out of it.) 

I found a really good [video series by Dr. Trefor Bazett](https://www.youtube.com/playlist?list=PLHXZ9OQGMqxersk8fUxiUMSIx0DBqsKZS) that I used to guide my self-study of the course content. Apart from his videos, I also studied from [Dr. Justin Wyss-Gallifent's notes](https://www.math.umd.edu/~immortal/CMSC250/) on the course to fill in gaps in knowledge.

## statements.

A **statement** is some construct that is either distinctly *true* or *false*.

- The statement $p: 5 > 2$ is a *true* statement.
- Similarly, saying $q: 4 > 68$ would be a *false* statement.
- Something like $r: x > 6$ isn't a statement on its own, as its "truthiness" depends on the value of some variable $x$ that we don't know.

The following symbols are often used when writing complex statements.

- Let's say we have two statements $p$ and $q$.
- Saying $\neg p$ translates to "not" $p$.
- $p \land q$ translates to $p$ "and" $q$.
- And lastly, $p \lor q$ translates to $p$ "or" $q$.

Let's break down the following statement: "my shirt is gray, but my shorts are not."

- We can separate the above into some manipulation of two assertions.
  - $p:$ "my shirt is gray." (This is *true*.)
  - $q:$ "my shorts are gray." (This is *false*.)
- So we can rewrite the original statement as $p \land \neg q$.
  - The $\neg q$ resolves to *true* when $q$ is *false*, which it is in this case.

We can use **truth tables** to visually represent the outcomes of more complex statements.

- Let's create a truth table for negation, or $\neg p$.

  - |   $p$   |  $\neg p$   |
    | :-----: | :---------: |
    | *true*  | ***false*** |
    | *false* | ***true***  |

  - Essentially, we are resolving the possible values for $\neg p$ based on every possible value of $p$.

  - While this example is pretty simple, truth tables can become very useful in more complex scenarios.

- Let's try another one for $p \land (\neg q)$.

  - We have two statements to define before we can "calculate" the possibilities.

  - |   $p$   |   $q$   | $\neg q$ | $p \land (\neg q)$ |
    | :-----: | :-----: | :------: | :---------------: |
    | *true*  | *true*  | *false*  |    ***false***    |
    | *false* | *true*  | *false*  |    ***false***    |
    | *true*  | *false* |  *true*  |    ***true***     |
    | *false* | *false* |  *true*  |    ***false***    |

  - Why do we have four rows for $p$ and $q$? Can't each of them only have two values? (*true* and *false*.)

    - Yes, but notice how we need to account for all possibilities.
    - Two variables each having two possible values means $2^2 = 4$ total combinations.

  - Notice how we made a column especially for $\neg q$.

    - While this isn't the final value we are looking for, writing down intermediate steps in the table can make balancing all the *true*s and *false*s a lot easier.

## logical equivalence.

- Sometimes two statements can be **logically equivalent**, but be expressed in different ways. Truth tables can help determine whether differently-written statements can have equivalent outcomes.

- Let's use a truth table to determine if $(\neg p) \lor (\neg q) \leftrightarrow \neg(p \land q)$.

- Here, the $\leftrightarrow$ symbol signifies logical equivalence.

- |   $p$   |   $q$   | $\neg p$ | $\neg q$ | $(\neg p) \lor (\neg q)$ | $p \land q$ | $\neg(p \land q)$ |
  | :-----: | :-----: | :------: | :------: | :---------------------: | :--------: | :--------------: |
  | *true*  | *true*  | *false*  | *false*  |       ***false***       |   *true*   |   ***false***    |
  | *false* | *true*  |  *true*  | *false*  |       ***true***        |  *false*   |    ***true***    |
  | *true*  | *false* | *false*  |  *true*  |       ***true***        |  *false*   |    ***true***    |
  | *false* | *false* |  *true*  |  *true*  |       ***true***        |  *false*   |    ***true***    |

- Notice how the two columns corresponding to $(\neg p) \lor (\neg q) $ and $\neg(p \land q)$ are identical. 

- Since the outcome of both statements are the same when provided with the same values for $p$ and $q$, we consider them to be **logically equivalent**.

A **tautology** is a statement that is considered to be *always true*.

- A tautology might be $t: 5 > 2$.
- Tautologies have some interesting properties.
- Given some statement $p$ and some tautology $t$:
  - $p \lor t$ is always *true*.
    - $t$ is always *true,* which satisfies at least one of the two.
  - $p \land t$ is always $p$.
    - $t$ is always *true*; $p$ will determine whether both are *true* or not.
- Try to make truth tables for the above two!
  - When determining the # of rows, remember that $t$ is always *true.*

A **contradiction** is a statement considered to be *always false.*

- A contradiction might be $c: 2 > 9$.
- As with tautologies, contradictions have some unique properties.
- Given some statement $p$ and some contradiction $c$.
  - $p \land c$ is always *false*.
    - $c$ is always *false*; so both will never be *true*.
  - $p \lor c$ is always $p$.
    - $c$ is always *false*; $p$ will determine whether at least one of them are *true* or not.

**DeMorgan's Laws** are two important identities of logical equivalence that are worth understanding (as opposed to memorizing).

- Here's the first one: $\neg(p \land q) \leftrightarrow (\neg p) \lor (\neg q)$.

  - "If both $p$ and $q$ are not *true*, then either $p$ or $q$ must be *false*."

  - While thinking about it hard enough might make it make sense, let's try to "prove" this equivalence with a truth table!

  - |   $p$   |   $q$   | $p \land q$ | $\neg(p \land q)$ | $\neg p$ | $\neg q$ | $(\neg p) \lor (\neg q)$ |
    | :-----: | :-----: | :---------: | :---------------: | :------: | :------: | :----------------------: |
    | *true*  | *true*  |   *true*    |    ***false***    | *false*  | *false*  |       ***false***        |
    | *false* | *true*  |   *false*   |    ***true***     |  *true*  | *false*  |        ***true***        |
    | *true*  | *false* |   *false*   |    ***true***     | *false*  |  *true*  |        ***true***        |
    | *false* | *false* |   *false*   |    ***true***     |  *true*  |  *true*  |        ***true***        |

  - And there we go, the two columns are identical!

- And the second identity: $\neg(p \lor q) \leftrightarrow (\neg p) \land (\neg q)$.

  - "If neither of $p$ or $q$ are *true*, then both $p$ and $q$ must be *false.*"
  - Notice that this looks very similar to the first identity, but the $\land$s and $\lor$s are swapped.
  - Once again, this might already make logical sense to you, but I encourage you to demonstrate the equivalence with a truth table.

Let's try and apply the ideas we've just learned by simplifying the following:

- We start with $(\neg(p \lor q)) \land t$, where $p$ and $q$ are some statements and $t$ is a tautology.
- Immediately we can simplify to just $\neg(p \lor q)$.
  - Why? Because $t$ $\land$ any statement $n$ is just $n$.
-  Lastly, we get $(\neg p) \land (\neg q)$.
  - How? By applying DeMorgan's Law.
- With these laws and definitions, simplifying complex statements can be a lot less clunkier than a whole truth table.

## conditionals.

A **conditional** defines an implied relationship between two statements.

- Writing the conditional $p \rightarrow q$ is the equivalent of saying "if $p$ is *true*, then $q$ must also be *true*" or, more concisely, $p$ implies $q$.

The conditional $p \rightarrow q$ is defined as $(\neg p) \lor q$.

- "Either $p$ is *not true*, or $q$ is *true*."

- This might already make sense to you, but let's once again refer to our truth table!

- |   $p$   |   $q$   | $\neg p$ | $(\neg p) \lor q$ | $p \rightarrow q$ |
  | :-----: | :-----: | :------: | :---------------: | :---------------: |
  | *true*  | *true*  | *false*  |      *true*       |      *true*       |
  | *false* | *true*  |  *true*  |      *true*       |       *???*       |
  | *true*  | *false* | *false*  |      *false*      |      *false*      |
  | *false* | *false* |  *true*  |      *true*       |       *???*       |

- Here we have something interesting. In the cases where $p$ is *true*, we can clearly match up the outcomes of $p \rightarrow q$ and $(\neg p) \lor q$. However, when $p$ is *false*, we can't predict the outcome of $q$ with our conditional.

- So how do we determine the truthiness of $p \rightarrow q$ in those cases?

  - We assume it is **vacuously *true***. This will be defined very soon, and it will make sense why this is our outcome.

- If we replace the *???*s in our table with *true* values, we've demonstrated that $(p \rightarrow q) \leftrightarrow ((\neg p) \lor q)$.

The idea of **vacuous truth** is essentially "you can't prove that it's *false*."

- Not the most rigorous definition, but it more or less holds.
- Since the conditional can't really predict anything about $q$ when $p$ is *false*, we can't specifically say that $q$ can be *false*.
- So we assume it is **vacuously *true***.
- Here's a good [discussion (Reddit lol)](https://www.reddit.com/r/math/comments/vj5lyg/why_do_we_say_its_vacuously_true/) about vacuous truth. It's not a reliable mathematical source by any means, but the points made are very beginner friendly.

Now that we know more about the definition of a conditional, let's have fun with it!

- How might we negate a conditional?
  - Initial statement: $\neg (p \rightarrow q)$.
  - Definition of a conditional: $\neg((\neg p) \lor q)$.
  - DeMorgan's Law: $(\neg (\neg p)) \land (\neg q)$.
  - Simplify double negative: $p \land (\neg q)$.
    - Our final answer!
- The **contrapositive** of a conditional $p \rightarrow q$ is $(\neg q) \rightarrow (\neg p)$.
  - A conditional and its contrapositive are logically equivalent.
  - Let's see if this makes sense: "if I am hungry, I will eat food."
    - Let $p$ be "I am hungry."
    - Let $q$ be "I will eat food."
  - Now we write out our contrapositive $(\neg q) \rightarrow (\neg p)$: "If I do not eat food, I am not hungry."
    - Since $q$ is *false*, we know that $p$ cannot be *true* either. If $p$ was *true*, then our original conditional would not hold.
- The **converse** of a conditional $p \rightarrow q$ is $q \rightarrow p$.
  - A conditional and its converse are very clearly *not* logically equivalent.
    - The direction of implication is flipped.
  - Let's take our first example again: "if I am hungry, I will eat food."
    - Let $p$ be "I am hungry."
    - Let $q$ be "I will eat food."
  - Taking the converse $q \rightarrow p$: "If I will eat food, I am hungry."
    - This is clearly very different than the initial statement.
- Lastly, the **inverse** of a conditional  $p \rightarrow q$ is $(\neg p) \rightarrow (\neg q)$.
  - A conditional's inverse is the contrapositive of its converse.
    - The inverse and converse are logically equivalent.
    - This also means that a conditional and its inverse are *not* logically equivalent.
  - Let's take our first example again: "if I am hungry, I will eat food."
    - Let $p$ be "I am hungry."
    - Let $q$ be "I will eat food."
  - Taking the converse $q \rightarrow p$: "If I am not hungry, I will not eat food."
    - This is clearly very different than the initial statement.
    - 