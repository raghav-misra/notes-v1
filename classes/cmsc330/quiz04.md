# cmsc330 / exam04

## lambda calculus.

### luh basics.

Variables in lambda calculus are just letters, like $y$. Wow!

Functions in lambda calculus take the form $\lambda x.e$, where $x$ is the parameter of the function and $e$ is the function body.

Take $\lambda x. \lambda y. y$. In OCaml, this would look like:

```ocaml
fun x -> fun y -> y
```

We read this left to right, i.e., $\lambda x. \lambda y. \lambda z. \lambda j j$. That is, $\lambda y$ is in body of $\lambda x$, $\lambda z$ is in body of $\lambda x$, etc. 

### function application.

Consider that $(\lambda x. x) a \Rightarrow a$. Here, we are taking the function $\lambda x. x$ and passing the value $a$ to it. Clearly, we get back the value of $a$, as $\lambda x. x$​ just returns whatever is passed to it.

Consider the statement $a b$. Here, $a$ has not been defined as a function. So we cannot pass $b$ to it. Since, we can't really do anything, this is simplified to $a b$, or can't be simplified to anything else.

### ambiguous statements.

Take $\lambda x. x y$. Here, either $x y$ is the body of $\lambda x$, or $y$ is being applied to $\lambda x. x$.

Consider $a b c$. Are we passing $c$ into the result of $ab$, or the result of $bc$ into $a$?

Both statements are very ambiguous. As such, lambda calculus has the following rules:

1. Expressions are **left associative**.
2. The scope of a function extends until the end of the expression or when an *unmatched parenthesis* is reached.

With the above rules, $\lambda x. xy$ is a function that takes parameter $x$ and returns $xy$.

### left associative.

When an expression is **left associative**, it means that given three (or more) expressions, we group the first two together and evaluate. 

As such, $abc$ would evaluate to $(a b) c$, or passing in $c$ to the result of $ab$​.

### function scope.

A function's body extends until it meets an ending parenthesis that was not started inside the function body.

For example, $(\lambda x. (\lambda y. (\lambda z (x y z))))$. The body of $\lambda x$ would stop right before the last parenthesis.

### reduction.

A lambda expression that cannot be reduced further is in **beta-normal form**. Performing a function call to reduce an expression is called a **beta-reduction**.
$$
\begin{align*}
	(\lambda x. \lambda y. y) a b 
	&\Rightarrow ((\lambda x. \lambda y. y) a) b &\text{group first two} \\
	&\Rightarrow (\lambda y. y) b &\text{reduced $x$ function} \\
	&\Rightarrow b &\text{reduced $y$; beta-normal form}
	
\end{align*}
$$
In the above example, it took *two beta-reductions* to get to beta-normal form.

Consider the statement $(\lambda x. a x a) ((\lambda y. y y) z).$ We have two ways to reduce this. Either we reduce $((\lambda y. y y) z) \Rightarrow (zz)$ and then pass it into $\lambda x$, or we pass $((\lambda y. y y) z)$ into $\lambda x$ and then reduce the entire expression.

- **Eager evaluation** is when we reduce arguments before passing them into functions.
- **Lazy evaluation** is when we pass un-reduced arguments into functions, reducing them only where they are used in the function body.

### variables.

A **bound variable** is a parameter of a lambda function. The $x$ in ($\lambda x. x) y$ is a bound variable. A **free variable** is not *bound* to a parameter. The $y$ in $(\lambda x. x) y$​​ is a free variable.

Since variables can be shadowed in lambda calculus, it is good to remember which ones are free or bound when performing reductions. For example,
$$
\begin{align*}
	(\lambda y. (\lambda x. xx) y x) a
	&= (\lambda y_{b}. (\lambda x_{b}. x_{b}x_{b}) y_{b} x) a &\text{mark bound} \\
	&\Rightarrow (\lambda x_b. x_bx_b) a x &\text{reduce $y$ fn} \\
	&\Rightarrow ((\lambda x_b. x_bx_b) a) x &\text{group left two} \\
	&\Rightarrow (a a) x &\text{reduce $x$ fn}
	
\end{align*}
$$
An **alpha conversion** is the process of renaming all of the same bound variables to a different name. Essentially changing the parameter name of the function. In the above example, when we marked the variables as bound with the subscript, that was *sort of like* alpha conversion.

### church encodings.

In lambda calculus,

- **true** is represented by $\lambda x. \lambda y. x$
- **false** is represented by $\lambda x. \lambda y. y$
- To say **if $a$ then $b$ else $c$**, we simply write $a b c$​.
- This works due to our encodings. 

## rust!

### a language.

```rust
fn main() {
    println!("hello") // prints hello
    
    let x = 3; // let statements.
    let twizz = {
		let a = 4;
    	let b = 6;
        a - b
    }; // this is kinda like let ... in syntax from ocaml.
    
    let meow = if true {
        a + b // return this cuz true always true
    } else {
        a - b // never here cuz true
    };
}

fn test(x: i32) { // no need for return type cuz its "unit" aka void
    println!("{}", x + y);
}

fn add(a: i32, b: i32) -> i32 { // needs return type cuz not unit
    a + b
}
```

