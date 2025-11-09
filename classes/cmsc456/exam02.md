# cmsc456 / exam02

## lecture 09

### modular arithmetic

**Modular arithmetic** involves cyclic number systems. Form a new number system mod $N$ for each integer $N$. Convert from integer to mod $N$ by taking the remainder when dividing by $N$.

*Addition:* $(35 + 58) + 15 \ \text{mod} \ 71 = 35 + (58 + 15)  \ \text{mod} \ 71 = 37$.

*Subtraction:* $35 - 58 \ \text{mod} \ 71 = 71 - 23 \ \text{mod} \ 71 = 48$.

*Multiplication:* $35 \cdot 58 \ \text{mod} \ 71 = 2030 \ \text{mod} \ 71 = 42 \ \text{mod} \ 71$.

*Division* is weird. Since it is the inverse of multiplication,

- If $ab = c \ \text{mod} \ N$, then $c/a = b \ \text{mod} \ N$. Then, $35 / 58 \ \text{mod} \ 60 = \, ?$ can rewritten as $58(?) = 35 \ \text{mod} \ 60$. How do we solve this?
- Note $c/a = b \ \text{mod} \ N \Leftrightarrow c= ab + kN$, for some integer $k$. Suppose some $p$ exists such that $p \mid a$ and $p \mid N$. Then, $p \mid (ab + kN)$ and $p \mid c$.
- Division by $a$ is possible only if $c$ is divisible by $p$ (common factor of $a$ and $N$).
- 

