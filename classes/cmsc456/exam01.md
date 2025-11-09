# cmsc456 / exam01

## 1-introduction

### 1.2-setting of private key encryption

**Private key cryptography** useful for sharing information securely over a *space* (two people know a key beforehand and securely communicate) and over *time* (someone revisits a piece of information overtime; like disk encryption).

A **private-key encryption scheme** is defined by:

- $\mathcal{M}$, a message space.
- $\texttt{Gen}$, the key generational algorithm which outputs a key $k$ according to some distribution.
- $\texttt{Enc}$ takes in $k$ and message $m$ and outputs ciphertext $c$.
- $\texttt{Dec}$ takes in $k$ and ciphertext $c$ and outputs message $m$.

The correctness requirement for such a scheme, is that for all $k$ outputted by $\texttt{Gen}$ and $m \in \mathcal{M}$,
$$
\texttt{Dec}_{k} (\texttt{Enc}_{k}(m)) == m.
$$
Letting $\mathcal{K}$ be the "key space," we assume that $\texttt{Gen}$ uniformly returns a key $k \in \mathcal{K}$.

**Kerckhoff's principle** says that any component of the encryption scheme, except for the key $k$ itself, should be allowed to fall into bad actors' hands with no impact on a ciphertext's security. That is, *security relies solely on the secrecy of the key.*

### 1.3-historical ciphers (they suck)

**Caesar cipher** is done by shifting all plaintext letters by a constant $3$.  **Shift cipher** is a generalized version for $k$.

**Shift cipher scheme.**

- $M$ comprises all alphabetical strings.
- $\texttt{Gen}$ returns an integer from $0$ to $25$ uniformly.
- $\texttt{Enc}$ shifts the input $k$ chars right.
- $\texttt{Dec}$ shifts the input $k$ chars left.

*A secure encryption scheme should have a key space that is large enough to not be susceptible to brute-force attacks.* Shift cipher clearly fails there.

**Substitution cipher** swaps every letter with a corresponding letter defined by the key which is a one-to-one map. *Huge key space! Must be secure right? No :(*

**Frequency analysis** maps frequent letters, bigrams, and trigrams in English to those in the ciphertext, to assist with deciphering it. Substitution ciphers are obviously vulnerable to these.

**Vigenere cipher** is a shift cipher where the shift is defined by a repeated key. The goal is to make frequency analysis less useful since there is no longer a 1:1 mapping.

## 2-perfectly secret encryption

### 2.1-definitions

A scheme is **perfectly secret** iff for all $m \in \mathcal{M}$ and $c \in \mathcal{C}$,
$$
P(M = m \mid C = c) = P(M = m).
$$
That is, the probability of a message being some string is independent of whether the ciphertext is known or not.

Another formulation of the above is
$$
P(\texttt{Enc}_k(M) = c) = P(\texttt{Enc}_k(m') = c),
$$
or that any two messages are equally likely to be represented by the same ciphertext.

A scheme is **perfectly indistinguishable** if *any attacker*, when presented with two messages in $\mathcal{M}$ and the ciphertext for *one* of them, has a probability no greater than $0.5$ of guessing which one was encrypted. It is somewhat obvious how this connects to the previous formulation of perfect secrecy.

### 2.2-one time pad

The **one time pad** is a *perfectly secret*, *private key encryption scheme* defined as follows:

- $M = \{\text{all bitstrings}\}$
- $\texttt{Enc}_k(m)$ returns XOR of $m$ and $k$.
- $\texttt{Dec}_{k}(c)$ returns XOR of $c$ and $k$.

This scheme relies on the symmetry of the XOR operation, that is $k \oplus (k \oplus m) = m$.

Disadvantages: Requires a key of the same length as the message, which is cumbersome for long messages. In addition, if the same key is used for multiple messages, attackers can compute
$$
c \oplus c' = (m \oplus k) \oplus (m' \oplus k) = m \oplus m',
$$
which tells the attacker exactly how two messages differ.

### 2.3-limitations of perfect secrecy

*Important.* For a scheme to perfectly secret, its key space must be at least as large as its message space.

### 2.4-shannon's theorem

**Shannon's Theorem** states that an encryption scheme is perfectly secret if and only if:

1. Every key in the space is chosen with equal probability.
2. For every $m \in \mathcal{M}$ and $c \in \mathcal{C}$, there is a unique key $k \in \mathcal{K}$ such that $\texttt{Enc}_k(m) = c$.

## 3-private key encryption

### 3.1-computational security

A function $f: \mathbb{N} \rightarrow (\mathbb{R}^{+} \cup \{0\})$ is **negligible** if for every polynomial $p$, there is an $N$ such that for all $n > N$, $f(n) < \frac{1}{p(n)}$.

Using this definition, a scheme is **secure** if for every *probabilistic polynomial time* adversary $A$ carrying out an attack, the probability that $A$ succeeds is negligible.

*Computational secrecy introduces two relaxations of perfect secrecy.* Regardless of how the scheme is constructed,

1. Given a ciphertext $c$, an adversary can decrypt $c$ using all keys $k \in \mathcal{K}$. Brute force attacks like this allow an adversary to "succeed" in time $O(|\mathcal{K}|)$.
2. The adversary can "guess" a uniform key $k \in \mathcal{K}$ and has a $1/|\mathcal{K}|$ of "success."

### 3.2-defining computational security

Let the message space be $\mathcal{M} = \{0, 1\}^*$, the set of all finite-length binary strings. $\texttt{Gen}$, $\texttt{Enc}$, and $\texttt{Dec}$ are *probabilistic polynomial time algorithms*. In addition, $\texttt{Dec}$ can output an error. In most cases, $\texttt{Gen}$ outputs a uniform $n$-bit string as the key, so we omit it and define a private-key encryption scheme to be $(\texttt{Enc}, \texttt{Dec})$.

**Adversarial indistinguishability experiment** $\texttt{PrivK}^{\texttt{eav}}_{A, \Pi}$:

1. Adversary $A$ is given input $1^n$ and outputs a pair of messages $m_0$ and $m_1$ of same length.
2. A key $k$ is generated and one of the two messages is encrypted with $k$, yielding ciphertext $c$. We call $c$ the **challenge ciphertext**.
3. $A$ guesses which message $c$ corresponds to.
4. If $A$ guesses correctly, we say that it succeeded. 

A private key encryption scheme $\Pi$ is **EAV-secure** if for all *probabilistic polynomial-time adversaries* $A$ there is a negligible function $g$ such that for all $n$, 
$$
P(\texttt{PrivK}^{\texttt{eav}}_{A, \Pi}(n) = 1) \leq \frac{1}{2} + g(n).
$$
That is, the probability of the indistinguishability experiment is not better than random chance by a non-negligible amount.

### 3.3-constructing an eav-secure thingy

A **PRG** $G$ is an efficient, deterministic algorithm for transforming a short, uniform *seed* into a longer, "uniform-looking" output string. Uses a bit of true randomness to generate a large amount of pseudorandomness.

For a **PRG** $G$ to be sound, a the probability that any distinguisher (probabilistic polynomial time algorithm which guesses if a string is pseudorandom) $D$ returns $1$ for its output should be close to $D$'s output when given truly uniform strings. That is,
$$
P[D(G(U_n)) = 1] - P[D(U_m)] \leq g(n),
$$
where $G$ is our $n \rightarrow m$ PRG candidate, $U_k$ refers to any $k$-length uniformly random string, and $m > n$. 

$G$ **is a pseudorandom generator** if no *efficient distinguisher* can detect whether its output is pseudorandom with probability greater than that of a uniformly random string.

Steps to prove computational security with **reduction.**

- Say we wish to prove that scheme $\Pi$ is secure.
- We will rely on pre-existing knowledge that a problem $X$ is "hard." 
- Then, we assume that attacker $A$ can solve $X$, and aim to construct attacker $A'$ to solve $\Pi$ using $A$ as a subroutine.

In the context of PRGs, we may want to show that an efficient attack on $G$ can be turned into an efficient attack on $H$.

- We assume that we have access to an efficient attacker for $H$.
- A pattern for doing this is to consider an output string from $G$. We want to consistently convert this into an output string for $H$ in a way that is consistent with the relationship between the definitions of $G$ and $H$.
- Then, we pass this input to $H$'s attacker, and decide to return yes or no, depending on its result, due to the relationship between the input strings and $G$ and $H$.

### 3.3-cpa security

**Chosen plaintext attacks** are when the adversary manipulates someone into encrypting a specific plaintext.

**CPA-security** gives the adversary $A$ access to an *encryption oracle* that encrypts any plaintext $A$ wants using an unknown key $k$, giving $A$ the associated ciphertext. If $\texttt{Enc}$ is randomized, then the oracle also yields the randomized result. $A$ can query the oracle however much they like. If the adversary has no advantage when given this oracle, we say that the scheme is **CPA-secure**. That is,
$$
P[\texttt{PrivK}^{\texttt{cpa}}_{A,\Pi}] \leq \frac{1}{2} + \texttt{negl}(n).
$$

### 3.5-constructing cpa secure schemes

$F: \{0,1\}^* \times \{0,1\}^* \rightarrow \{0,1\}^*$ takes in a key $k$ is *efficient* if $F(k, x)$ is computable in polynomial time. $F$ is a **PRF** if for all efficient distinguishers $D$,
$$
|P[D^{F_k}(1^n) = 1] - P[D^{f}(1^n) = 1]| \leq \texttt{negl}(n).
$$
It is important to note that $D$ is not given the key $k$, as it is not given the seed in the case of a PRG.

The size of $\texttt{Func}_n$ is $2^{n \cdot 2^n}$. The size of $\texttt{Perm}_n$ is $(2^n)!$, which is the set of all bijections in $\texttt{Func}_n$.

### 3.6-modes of operation in practice

A **stream cipher** is a pair of deterministic algorithms $(\texttt{Init}, \texttt{Next})$ where $\texttt{Init}$ takes in a seed $s$ and optional initialization vector $IV$, and outputs some initial state $st$. $\texttt{Next}$ takes in a current state and outputs a bit $y$ and a new state $st'$.

A stream cipher without an IV is just a more flexible PRG. Without an IV, when we call $\texttt{Init}$ with just a seed and call $\texttt{Next}$ to generate any number of pseudorandom bits.

**Synchronized mode.** Stream ciphers used to encrypt two-way online communication.

A **block cipher** is just a (strong) pseudorandom permutation. That is, a block cipher is a keyed function such that for all $k$, $F_k(x)$ is a bijection. $n$ is the key length of $F$ and $l$ is the block length.

**ECB (Electronic Code Book) Mode.** When the ciphertext is obtained by direct application of the block cipher to each plaintext block. Since $F^{-1}$ is computable, decryption is trivial. This is deterministic and therefore NOT CPA-secure.

**CBC (Cipher Block Chaining) Mode.** Sequential on block-after-block, so not parallelizable (possibly less efficient as a result). XOR the current plaintext and previous ciphertext blocks and apply the block cipher to its result. Set $c_0$ to the initialization vector.

## 7-practical constructions

### 7.1-stream ciphers

**RC4** is an old stream cipher which is not used anymore. It takes no IV, and can take a seed of up to $255$ bytes.

- **Init.** Initialize `S[i] = i` for all `0...a...255`

  Let `j = 0` and for `0...i...255`,

  ​	`j += S[i] + k_i mod 256`

  ​	Swap `S[i]` and `S[j]`

  Reset `i = j = 0`

- **Next.**

  `i += i`, `j += S[i]`

  `t = S[i] + S[j]`, `y = S[t]`

  `output y`

It is hard to prove security, but there are biases in RC4, some values show up more than others, for example. Not recommended.

### 7.2-block ciphers

**Confusion** aims to make the relationship between a key and ciphertext as complex and convoluted as possible. **Diffusion** aims to spread the influence of one plaintext bit across many ciphertext bits. As such, small changes to keys and/or plaintexts should result in significantly different ciphertexts.

**Substitution-permutation network** applies these principles to generate output of a cipher. A round consists of three steps.

1. *Key mixing.* Set $x = x \oplus k$, where $k$ is the round subkey.
2. *Substitution.* Set $x = S_1(x_1)\|\cdots\|S_8(x_8)$, where $x_i$ is the $i$th byte of $x$.
3. *Permutation.* Permute the bits of $x$ to obtain the output of the round.

After the last round, key mixing occurs one last time to yield the output of the cipher. The round subkeys are derived from a *master key* using a *key schedule*, which may define something as simple as subsets of the master key.

**Avalanche effect** is the property that a small change to the input should "affect" every bit of the output. Two properties:

1. $S$-boxes are designed such that a single bit of the input to an $S$-box should change at least two bits of the output.
2. The mixing is designed such that the bits output by any $S$-box affect the input to multiple $S$-boxes of a subsequent round.

**Feistel networks** are another way to make block ciphers. Unlike SPNs, the functions it needs are do not need to be invertible. Every round, the $l$-bit input is divided into two halves, $L$ and $R$ and then
$$
L_i = R_{i - 1} \qquad R_i = L_{i - 1} \oplus f_i (R_{i - 1})
$$
**DES** is a 16-round Feistel network: key length of 56 bits and block length of 64 bits. The same round function $f$ is used for each of the 16 rounds. It takes in a 48-bit sub key and a 32-bit input (half of the total block length, as expected).

**3DES** solves the brute force vulnerability by running **DES** three times with different keys.

**AES** has much longer key length (128, 192, 256 bits). It is a substitution-permutation network. State is initialized to the 128-bit input viewed as a 4-by-4 byte array.

- **AddRoundKey**. Subkey derived from master key, viewed as a 4-by-4 array of bytes. The state array is updated by XORing it with this subkey.
- **SubBytes**. Each byte of the state array is replaced by another byte according to a fixed lookup table $S$ (this is an $S$-box or a permutation).
- **ShiftRows**. The bytes in each row are shuffled. First row untouched. Second row shifted left 1, third row 2, fourth row 3.
- **MixColumn**. Invertible linear transformation is applied to the four bytes in each column. It has the property that if two inputs differ in $b > 0$ bytes, their outputs differ in at least $5 - b$ bytes.

In the last round, **MixColumns** is replaced with **AddRoundKey**.