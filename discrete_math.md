# notes on discrete math

## overview.

These notes go over the vast majority of the content of the course **CMSC250** "Discrete Structures" at the University of Maryland, College Park. I found a really good [video series by Dr. Trefor Bazett](https://www.youtube.com/playlist?list=PLHXZ9OQGMqxersk8fUxiUMSIx0DBqsKZS) that I used to guide my self-study of the course content. Apart from his videos, I also studied from [Dr. Justin Wyss-Gallifent's notes](https://www.math.umd.edu/~immortal/CMSC250/) on the course to fill in gaps in knowledge.

## statements.

- A **statement** is some construct that is either distinctly *true* or *false*.

  - The statement $p: 5 > 2$ is a *true* statement.
  - Similarly, saying $q: 4 > 68$ would be a *false* statement.
  - Something like $r: x > 6$ isn't a statement on its own, as its "truthiness" depends on the value of some variable $x$ that we don't know.

- The following symbols are often used when writing complex statements.

  - Let's say we have two statements $p$ and $q$.
  - Saying $\neg p$ translates to "not $p$."
  - $p \and q$ translates to "$p$ and $q$."
  - And lastly, $p \or q$ translates to "$p$ or $q$."

- Let's break down the following statement: "my shirt is gray, but my shorts are not."

  - We can separate the above into some manipulation of two assertions.
    - $p:$ "my shirt is gray." (This is *true*.)
    - $q:$ "my shorts are gray." (This is *false*.)
  - So we can rewrite the original statement as $p \and \neg q$.
    - The $\neg q$ resolves to *true* when $q$ is *false*, which it is in this case.

- We can use **truth tables** to visually represent the outcomes of more complex statements.

  - Let's create a truth table for negation, or $\neg p$.

    - |   $p$   |  $\neg p$   |
      | :-----: | :---------: |
      | *true*  | ***false*** |
      | *false* | ***true***  |

    - Essentially, we are resolving the possible values for $\neg p$ based on every possible value of $p$.

    - While this example is pretty simple, truth tables can become very useful in more complex scenarios.

  - Let's try another one for $p \land (\neg q)$.

    - We have two statements to define before we can "calculate" the possibilities.

    - |   $p$   |   $q$   | $\neg q$ | $p \and (\neg q)$ |
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

- Let's use a truth table to determine if $(\neg p) \lor (\neg q) \leftrightarrow \neg(p \and q)$.

  - Here, the $\leftrightarrow$ symbol signifies logical equivalence.

  - |   $p$   |   $q$   | $\neg p$ | $\neg q$ | $(\neg p) \or (\neg q)$ | $p \and q$ | $\neg(p \and q)$ |
    | :-----: | :-----: | :------: | :------: | :---------------------: | :--------: | :--------------: |
    | *true*  | *true*  | *false*  | *false*  |       ***false***       |   *true*   |   ***false***    |
    | *false* | *true*  |  *true*  | *false*  |       ***true***        |  *false*   |    ***true***    |
    | *true*  | *false* | *false*  |  *true*  |       ***true***        |  *false*   |    ***true***    |
    | *false* | *false* |  *true*  |  *true*  |       ***true***        |  *false*   |    ***true***    |

  - Notice how the two columns corresponding to $(\neg p) \or (\neg q) $ and $\neg(p \and q)$ are identical. 

  - Since the outcome of both statements are the same when provided with the same values for $p$ and $q$, we consider them to be **logically equivalent**.