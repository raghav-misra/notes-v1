# <u>cmsc330 / exam02</u>

## <u>operational semantics.</u>

<u>In short, **semantics** are a way to describe the meaning of programming languages.</u>

- <u>**Denotational semantics**, which use mathematical constructs and definitions.</u>
- <u>**Axiomatic semantics**, which describe meaning with axioms (examples).</u>

<u>But we focus on **operational semantics**, which describe meaning based on how something operates.</u>

<u>Take a basic language:</u>
$$
\begin{align*}
	e	&\rightarrow n \\
		&\rightarrow e ? e \\
    n	&\rightarrow 0|1|2|3|\dots
\end{align*}
$$
<u>This defines how we can write out the language, by validating something like $0?1?4$, but how do we define what these statements actually *do*? This is where **opsem** comes in.</u>

<u>Let's use opsem to define the case where some $e$ matches $(n)$. Very easy!</u> 
$$
\frac{}{n \Rightarrow n}
$$
<u>We call the above an axiom of our language, as we don't really need proof to show that it is true. But what about the case where $e$ matches with $(n_1?n_2)$? Let's say that the $?$ operator will add the two elements on its sides:</u>
$$
\frac{e_1 \Rightarrow n_1 \hspace{30px} e_2 \Rightarrow n_2 \hspace{30px} n_3 \text{ is } n_1 + n_2}{e_1 ? e_2 \Rightarrow n_3}
$$
<u>Let's use the above two rules to prove that $4 ? 3 \Rightarrow 7$ in our language:</u>
$$
\frac{4 \Rightarrow 4 \hspace{30px} 3 \Rightarrow 3 \hspace{30px} 7 \text{ is } 4 + 3}{4 ? 3 \Rightarrow 7}
$$
<u>What about something more complicated, like $9?3?2 \Rightarrow 14$?</u>
$$
\frac{9 \Rightarrow 9 \hspace{30px} \frac{3 \Rightarrow 3 \hspace{15px} 2 \Rightarrow 2 \hspace{15px} 5 \text{ is } 3 + 2}{3?2 \Rightarrow 5} \hspace{30px} 14 \text{ is } 9 + 5}{9?3?2 \Rightarrow 14}
$$

## <u>environments with opsem.</u>

<u>How can we represent creating and retrieving variables with operational semantics? This "place" that holds variables is called an **environment**.</u>

## <u>property-based testing.</u>

<u>Three parts to a **PBT**:</u>

1. <u>**Valid property:** does this property hold in the expected outcome?</u>
2. <u>**Valid implementation:** does our test correctly check if the valid property hold?</u>
3. <u>**Check bugs:** does testing for this property help us find bugs in the code?</u>

<u>Example function that removes the first occurrence from the list:</u>

```ocaml
let delete lst el = match lst with
	|[] -> []
	|h::t -> if h = el
		then t
		else h::(delete t el)
		
(* tests the property that el never occurs in lst after running delete *)
let test_delete lst el = not List.mem el (delete lst el)
```

1. <u>**Valid property?** No! Deleting the first occurrence of `el` does not imply that the final list will have no `el`s at all.</u>
2. <u>**Valid implementation?** Yes. The test correctly checks that `el` doesn't occur in `lst` after running `delete`.</u>
3. <u>**Check bugs:** N/A. Since the property is not valid, we can't determine whether it can reliably find issues or not.</u>

<u>Another example that reverses a list:</u>

```ocaml
let reverse lst = fold_left (fun a x -> a @ [x]) [] lst

(* tests the property that the length of lst is equal to length of reverse lst *)
let test_reverse lst = List.length lst = List.length (reverse lst)
```

1. <u>**Valid property?** Yes. A list will have the same length as its reversed version.</u>
2. <u>**Valid implementation?** Yes, the check to ensure the two lengths are same is correct.</u>
3. <u>**Check bugs:** Not in this case. There is a bug that exists in `reverse`, but the output list has the same length as the input, so the bug would never be caught.</u>

## <u>type checking proofs.</u>

<u>Complete the type-checking proof (derivation) for `fun x: int -> x + 2`:</u>
$$
\begin{align*}
\Large\frac{\frac{\frac{}{G, x: \text{int} \vdash x:\text{int}} \frac{}{G, x: \text{int} \vdash 2:\text{int}} \frac{}{\text{optype}(+) = (\text{int}, \text{int}, \text{int})}}{G, x:\text{int} \vdash x + 2: \text{int}}}{G \vdash \text{fun } x: \text{int} \rightarrow x + 2}
\end{align*}
$$

## <u>convert one language to the other.</u>

