# cmsc330 / quiz03

## speedrun.

A **grammar** is a way to represent a set of strings. We can check if a string is part of a grammar using **substitution**. There are two ways to substitute, **left-hand** and **right-hand** derivation.

**Left-hand derivation** is where we keep transforming the leftmost terminal until all terminals are non-terminals. **Right-hand derivation** is where we keep transforming the *rightmost* termination until all terminals are non-terminals.

A grammar is **ambiguous** when there are multiple ways to derive it on one side. For example, if it has **two or more** left-hand derivations. It usually arises when you can take multiple paths. So to reduce ambiguity, you can restrict the paths a string can take.

---

To create **precedence**, where certain transformations take priority over others, we can offload them onto new terminals. Note that precedence is bottom-up, so the further away a transformation is from the initial transform, the higher its precedence.

To make meaning of language, we need an **interpreter**. An interpreter has three parts: **lexer**, **parser**, and **evaluator**.

First, our **lexer** takes in a string and returns a token list. For example, `+ 1 * 2 3` might get converted to the token list `[Add; Int 1; Mult; Int 2; Int 3]`. The lexer does not care if the input is grammatically correct or not. $1* + 3$​ would still be converted to `[Int 1, Mult, Plus, Int 3]`.

Next, our **parser** actually verifies grammatical correctness. It does so by building a tree to ensure the token list follows the grammar. Some parsers generate the parse tree, which looks like the grammar derivation trees, but we will use **abstract syntax trees (ASTs)**, which care more about the content being parsed. 

Two functions to keep in mind for many parsers in this class are `lookahead`, which returns the element ahead of the current position, and `match_tok`, which matches the current position with some parameter and returns the remainder of the list. We use these functions to conditionally determine how we want to parse according to the grammar.

Lastly, the **evaluator** will actually evaluate the determine output for the AST that was built by the parser. It does this by performing a traversal of the abstract syntax tree, evaluating the leaves and bubbling back to the root.

## grammars.

A **language** is just a set of strings that conform to some specification. The specification that defines this set, a language, is called a **grammar**.

We will look at **context-free grammars (CFGs)** as opposed to context-sensitive grammars. Let's make a limited CFG for regular expressions "here we literally mean the regex string itself":
$$
\begin{align*}
	S \rightarrow 
	&|\epsilon \\
	&|\sigma \\
	&|S S \\
	&|S | S \\
	&|S^* \\
	&|(S)
\end{align*}
$$
This grammar will describe all strings that represent a (limited) regular expression. We can take a string and match it to a grammar **by substitution**. Let's show that $ab^*$ is in the set $S$:
$$
\begin{align*}
	S &\rightarrow SS \\
	&\rightarrow aS \\
	&\rightarrow aS^* \\
	&\rightarrow ab^*
\end{align*}
$$
How does this work? We start with $S$ and convert and substitute as needed:

1. Recognize that $SS$ is an example of $S$.
2. The first $S$ can be a member of $\sigma$, in this case $a$, leaving us with $aS$.
3. We can substitute $S^*$ for the second $S$, leaving us with $aS^*$.
4. For the only $S$ left, substitute a member of $\sigma$, in this case $b$, leaving us with $ab^*$.

Let's take the following CFG of a simplified English sentence:
$$
\begin{align*}
S \rightarrow &| NP \hspace{15px} VP \\
NP \rightarrow &|\text{pronoun} \\
            &|\text{proper\_noun} \\
            &|\text{det } AN \\
AN \rightarrow &|\text{adj } AN \\
			&|\text{noun} \\
VP \rightarrow &|\text{verb} \\
			&|\text{verb } NP
\end{align*}
$$
Does the sentence "$\text{You ate bro.}$" match the above grammar?
$$
\begin{align*}
	S \rightarrow &| NP \hspace{15px} VP \\
	\rightarrow &|\text{You } VP \\
	\rightarrow &|\text{You ate } NP \\
    \rightarrow &|\text{You ate bro.}
\end{align*}
$$
Yes, it does!

