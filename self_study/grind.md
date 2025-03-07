# Grind

## GPT Question/Answer

**How many phone calls are made in the US per day?**

- ~330M people in the US.
- Assume like 5-6 calls per person? Some people well rarely or never call (like those without phones) but those who call will call a decent amount probably, like sales reps and similar. Call centers and businesses probably contribute a huge amount in pulling the mean up from individuals.
- Maybe 330M*6 = 1.98B calls?

**What is the probability of drawing two aces consecutively from a standard deck of 52 cards?**

- $4/52$ first pull, $3/51$ second pull.
- Multiply them.

**A man has two ropes that each take exactly one hour to burn. However, the ropes burn at an inconsistent rate. How can he measure exactly 45 minutes?** 

- Ok, easy to measure an hour by burning a rope.
- Light both ends of the first rope and one end of the second rope.
- First rope will burn in 30 minutes, at which time there must be 30 minutes remaining for the second rope to finish burning.
- At this time, burn the other end of the second rope. It will burn in half the time, or 15 minutes.
- 30 + 15 = 45, so we have measured it!

**A car travels at 60 mph for 30 minutes, then 40 mph for another 30 minutes. What is the average speed?**

- First the car travels 30 miles in 30 minutes. Then 20 miles in 30 minutes.
- 30 + 20 = 50, whole trip was an hour, so we get 50 mph.

**You have a bag with 10 balls: 3 red, 4 blue, and 3 green. If you draw two balls without replacement, what is the probability that both balls are the same color?**

- Take the first ball:

  **Red:** $3/10$. Then there's a $2/9$ chance of second ball being red.

  **Blue:** $4/10$. Then there's a $3/9$ chance of the second ball being blue.

  **Green:** $3/10$. Then there's a $2/9$ chance of the second ball being blue.

- You get $(3/10)(2/9) + (4/10)(3/9) + (3/10)(2/9)$.

  - This is $24/90$, I believe.

**You roll two fair dice. What is the probability that the sum of the numbers on the two dice is 7?**

- For every value on the first dice, there is a corresponding value that adds to $7$ on the second dice.
- So across $36$ total possible sums, $6$ of them add up to $7$.
- $6/36 = 1/6$.

**In a game, you roll a fair six-sided die and then draw a card from a standard deck of 52 cards. What is the probability that you roll a 4 and draw a heart?**

- Rolling a $4$ is $1/6$. Drawing a heart is $13/52$. Both events are independent so you just multiply.
- $13/312$ is the probability.

**In a poker game, a player is dealt two cards from a standard deck of 52 cards. What is the probability that both cards are red (hearts or diamonds)?**

- 26 red cards. Without replacement we get $(26/52)*(25/51)$.

**You roll three fair dice. What is the probability that the sum of the numbers rolled is 9?**

- Joint discrete probability distribution.
- Total ways $6^3 = 216$
- So regardless of the first die's number, there's a way to make $9$.
  - If it's $6$ we have to make $3$ with the two remaining dice.
    - There is $2$ ways to do this.
  - If it's $5$ we have to make $4$ with the two remaining.
    - There is $3$ ways to do this.
  - If it's $4$ we have to make $5$ with the two remaining.
    - There is $4$ ways to do this.
  - $3$ ... $6$.
    - There is $5$ ways to do this.
  - $2$ ... $7$.
    - There is $6$ ways to do this.
  - $1$ ... $8$.
    - There is $5$ ways to do this.
    - Can't roll a $1$.
- So we get $2+\dots+6 + 5 = 25$.
- $25/216$ is answer.

**You flip a fair coin 3 times. What is the probability of getting exactly 2 heads?**

- Joint prob. dist. $8$ total outcomes.
- Total ways is $3 \choose 2$.
- $3/8$ is the probability.

**You roll a fair 6-sided die. If the result is even, you win $2$. If the result is odd, you lose $1$. What is your expected value for this game?**

- Half numbers on dice are even; half are odd.
- $(0.5*2) + (0.5*-1) = 0.5$ is EV.

**You’re playing a game where you roll a fair 6-sided die. If you roll a 1, you win $10. If you roll any other number, you win nothing. What is your expected value for this game?**

- $1/6$ chance you get $10$.
- $5/6$ chance you get $0$.
- $\frac{1}{6}*10 + \frac{5}{6} * 0  = 10/6$ EV.

**You have a biased coin that lands on heads with probability 2/3 and tails with probability 1/3. You flip it twice. What is the probability of getting exactly one heads?**

- $2$ choose $1$ for which coin gets the heads.
- ${2 \choose 1} \cdot \frac{2}{3} \cdot \frac{1}{3} = \frac{4}{9}$.

**In a two-player game, each player simultaneously chooses a number between 1 and 10 (inclusive). If the sum of their chosen numbers is odd, Player 1 wins. If the sum is even, Player 2 wins. What is the probability that Player 1 wins if both players choose their numbers randomly and independently?**

- Sum is even when both numbers are same parity.
- Sum is odd when both numbers are different parity.
- Player 1 wins when sum is odd, when numbers are different parity.
- Odd choices: 1, 3, 5, 7, 9.
- Even choices: 2, 4, 6, 8, 10.
- For each choice Player 1 makes, there are 5 choices that let them win.
- So you get $5*5 = 25$ ways. And $100$ outcomes.
- So $25/100 = 1/4$.

**In a game with three players, each player simultaneously chooses a number between 1 and 6 (inclusive). If the sum of the numbers is divisible by 3, Player 1 wins. If the sum is divisible by 2 but not 3, Player 2 wins. If the sum is neither divisible by 2 nor 3, Player 3 wins. What is the probability that Player 1 wins?**

- Player 1 wins: sum is divisible by 3.
- Rest of information doesn't matter if we can find this probability.
- In the span of outcomes, the divisible by 3 numbers are:
  - $3, 6, 9, 12, 15, 18$.
- Obviously only one way to make $3$.
- To make $6$, think about P1's choice.
  - P1 choice is $1$: $4$ ways to make $6 - 1 = 5$.
  - P1 choice is $2$: $3$ ways.
  - P1 choice is $3$: $2$ ways.
  - P1 choice is $4$: $1$ way.
  - $10$ total ways.
- To make $9$, think about P1's choice.
  - P1 choice is $1$: $5$ ways to make $9 - 1 = 8$.
  - P1 choice is $2$: $6$ ways.
  - P1 choice is $3$: $5$ ways.
  - P1 choice is $4$: $4$ ways.
  - P1 choice is $5$: $3$ ways.
  - P1 choice is $6$: $2$ ways.
  - $25$ total ways.
- Symmetry means $25$ ways for $12$.
- Symmetry means $10$ ways for $15$.
- Only one way to make $18$.
- So in total, $1+10+25+25+10+1 = 72$.
- Three die means $216$ total ways.
- $72/216$.

## Game Theory

ChatGPT taught me all of this, but the notes themselves are written by me!

### Introduction

**Game Theory** is the study of strategic decision-making.

- **Players** are the decision makers in the game.
- **Strategies** are the complete plans-of-action for a player in the game.
  - Chess: all one player's moves compose a strategy.
  - Rock-paper-scissors: you have 3 strategies.
- **Payoffs** are the rewards a player gets based on the outcome of a game.
  - Each player aims to maximize their own payoff.
  - In rock-paper-scissors: $1$ if you win, $0$ if you tie, $-1$ if you lose.

Types of games:

1. **Sequential** is when players move one after another; each player is able to see the previous move of the other player(s). Think chess.
2. **Simultaneous** is when players move at the same time. Like rock-paper-scissors or a dice game perhaps.

Zero-sum vs. non-zero sum.

1. A game is **zero-sum** when a player's gain corresponds directly to the loss of other players.
2. A game is **non-zero-sum** when players can cooperate or both benefit from strategies. Example is price-setting.

### Dominant Strategies

A **dominant strategy** is one that is the best for that player to play, regardless of what the other players do. If a player has a dominant strategy, they should always play it.

**Strictly vs. weakly** dominant:

- A **strictly dominant strategy** is always better than another strategy, no matter what the opponent does.
- A **weakly dominant strategy** is at least as good as another strategy in all cases.

Consider a product pricing example:

- Companies **A** and **B** are competitors. Each can choose between two pricing strategies:

  - High price: $\$100$
  - Low price: $\$50$

- **Payoff matrix:**

  |              | B - high   | b - low   |
  | ------------ | ---------- | --------- |
  | **A - HIGH** | $(10, 10)$ | $(3, 12)$ |
  | **A - LOW**  | $(12, 3)$  | $(5, 5)$  |

  - This matrix basically says the profit in millions is $(A, B)$ for each decision by company **A** and **B**, respectively.
  - If both charge a high price, they each make $10$ million.
  - If one charges a high price but the other charges a low price, the high-charging one makes $3$ million, while the low-charging one makes $12$ million.
  - If both charge a low price, both make $5$ million.

- Now, we look for **dominant strategies**.

  - For company **A**.
    - If **B** picks a high price, **A** should pick low price as well. $(12, 3)$ is better significantly than $(10, 10)$ for **A**.
    - If **B** picks a low price, **A** should pick low price as well. $(5, 5)$ is better significantly than $(3, 12)$ for **A**.
  - So, **A** has a **strictly dominant strategy** to pick low price regardless. Based on the matrix, the exact same logic applies to **B**, so picking a low price is strictly dominant for both companies.

- As such, the final outcome is $(5, 5)$.

- What's interesting? If the companies could cooperate and both pick high prices with knowledge that the other would as well, then both would profit certainly more with the $(10, 10)$ outcome. As opposed to ending up with $(5, 5)$ with the strictly dominant competitive strategy.

### Nash Equilibrium

Not all games have dominant strategy. So we need a broader concept.

**Nash Equilibrium** is when no player can improve their expected outcome by changing their strategy, assuming the other player doesn't change theirs.

- More simply, if a game is at Nash Equilibrium, no player has any incentive to change their move because they are already making the best choice given what the others are doing.

Take the following example:

- **Soccer penalty kick** has two players: kicker and goalie.

- Very simply, say the player can kick **left** or **right** and the goalie can then block **left** or **right**.

- Payoffs are dependent on whether the goalie can block the shot or not.

  |                  | Goalie left | goalie right |
  | ---------------- | ----------- | ------------ |
  | **KICKER LEFT**  | $(0, 1)$    | $(1, 0)$     |
  | **KICKER RIGHT** | $(1, 0)$    | $(0, 1)$     |

- This game has **no dominant strategy**. "Optimality" here would be to randomize the decision. As if they didn't the goalie could learn the kicker's strategy and block smartly.

### Mixed NE

In a **mixed Nash equilibrium**, players don't always choose one strategy. Instead, they choose a probability distribution over all the possible strategies.

In other words, they randomize their choices to keep their opponents guessing, preventing them from exploiting any predictability.

A **pure strategy** is one where you always choose a particular action.

A **mixed strategy** is one where you randomize different actions over different probabilities. 

In a **mixed NE**, players choose their mixed strategy in such a way that their expected payoff is maximized given the other player's strategy.

- No player wants to deviate from their current mixed strategy; there is no evidence or incentive to do so.

Take **rock-paper-scissors**.

- A pure strategy is destined to fail here. For instance, if you pick rock every time, eventually your opponent may catch on and your strategy will start consistently failing.
- Here, a mixed NE occurs when every player randomizes their strategy.
- The best mix is $\frac{1}{3}$ rock, $\frac{1}{3}$ scissors, $\frac{1}{3}$ paper.
- *Why is this a Nash equilibrium?*
  - If one person deviates from this rate, starting to pick rock more often for example, then the other player can identify and capitalize on this by starting to pick paper more often.
  - The one who deviates is likely to lose then.
  - Hence, no incentive to change this random strategy.

### Math behind Mixed NE

Take the rock-paper-scissors example. For a given player, the probabilities of picking rock, paper, or scissors obviously sums to $1$ as those are the only options.

Consider the payoff matrix for the game between player **P1** and player **P2**.

|                  | P2: ROCK  | P2: PAPER | P2: SCISSORS |
| ---------------- | --------- | --------- | ------------ |
| **P1: ROCK**     | $(0, 0)$  | $(-1, 1)$ | $(1, -1)$    |
| **P1: PAPER**    | $(1, -1)$ | $(0, 0)$  | $(-1, 1)$    |
| **P1: SCISSORS** | $(-1, 1)$ | $(1, -1)$ | $(0, 0)$     |

The **expected payoff** for **P1** is defined by the sum of the outcomes multiplied by the probability of said outcomes occurring.
$$
\begin{align*}
	E_1 
		&= p_{1_R} [0 (p_{2_R}) + 1 (p_{2_S}) + (-1)(p_{2_P})] \\
		&\quad +\, p_{1_P} [1 (p_{2_R}) + (-1) (p_{2_S}) + 0(p_{2_P})] \\
		&\quad +\, p_{1_S} [(-1) (p_{2_R}) + 0 (p_{2_S}) + 1(p_{2_P})]
\end{align*}
$$
Same idea for **P2**.

For the mixed strategy to be Nash Equilibrium. Each decision of the mixed strategy must have an equal likelihood of occurrence, or else there is predictability. This leaves us with an **indifference condition**
$$
E_{1_R} = E_{1_S} = E_{1_P}.
$$
Since the probabilities must add up to $1$, we solve and eventually get
$$
p_{1_R} = p_{1_S} = p_{1_P} = \frac{1}{3}.
$$
Same idea for **P2**.

### Example games

**You are playing rock-paper-scissors against a friend. Winner takes $\$1$ from the loser. Your friend is banned from playing scissors. What's the EV of the game for you?**

- We start by writing out the payoff matrix. Let's say we are **A** and the friend is **B**. Then,

  |                 | B: Rock   | B: PAPER  |
  | --------------- | --------- | --------- |
  | **A: ROCK**     | $(0, 0)$  | $(-1, 1)$ |
  | **A: PAPER**    | $(1, -1)$ | $(0, 0)$  |
  | **A: SCISSORS** | $(-1, 1)$ | $(1, -1)$ |

- We consider any particularly optimal or suboptimal strategies.

  - For **A**, it is pretty useless to play rock. Since the best outcome is a tie and its impossible to win. (**B** can't play scissors).

- So we have **B** randomly playing rock or paper. And **A** randomly playing paper or scissors.

- Then EV of **A** is $\frac{1}{4}(1 + 0 + (-1) + 1) = \frac{1}{4}$.