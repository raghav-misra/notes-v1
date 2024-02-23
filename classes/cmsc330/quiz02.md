# cmsc330 / quiz 02

## quiz topics.

1. Higher-order functions, i.e. `map` and `fold`.
2. Variants, records, and data types.
3. Imperative OCaml, i.e. `ref`, `for/while`, etc.
4. Regular expressions.

## hofs ~ `map`.

Consider the definition of `map`:

```ocaml
let rec map f l = match l with
	|[] -> []
	|h::t -> (f h)::(map f t)
```

OCaml would likely infer the type of the above function to be something like the following:

```ocaml
('a -> 'b) -> 'a list -> 'b list
```

Essentially, it is converting an  `'a list` to a `'b list` by transforming each element of the list with a function of type `('a -> 'b)`.

Consider the following code:

```ocaml
map (fun a -> a + 1) [1; 2; 3; 4; 5] 
(* returns [2; 3; 4; 5; 6] *)
```

Each element of the initial list `a` is transformed by the function into `a + 1`.

**Fire!** :fire:

## hofs ~ `fold`.

The `fold` function comes in two varieties, `fold_left` and `fold_right`. Both do similar things, but have important distinctions.

Let's first consider the definition of `fold_left`:

```ocaml
let rec fold_left f l a = match l with
	|[] -> a
	|h::t -> fold_left f t (f h a) 
```

OCaml would likely infer the type of the above function to be something like:

```ocaml
('a -> 'b -> 'b) -> 'a list -> 'b -> 'b
```

Essentially, `fold_left` accumulates some value `a` over the course of the list `l`. Don't confuse parameter `a` with generic type `'a`.

Consider the following code:

```ocaml
fold_left (fun e a -> a + e) [1; 2; 3; 4] 0
(* returns 10 *)
```

This function essentially sums up all the values in the `int list` that is passed in.

**Huge!** :blowfish:

Next, let's look at the implementation of `fold_right`:
```ocaml
let rec fold_right f a l = match l with
	|[] -> a
	|h::t -> f (fold_right f a t) h
```

OCaml would likely infer the above function's type to be:

```ocaml
('a -> 'b -> 'a) -> 'a -> 'b list -> 'a
```

**Wow!** :sparkle:

## variants.

OCaml **variants** are quite literally `enum`s from every other language that has those.

Let's make a Pokemon type variant:

```ocaml
type ptype = TFire | TWater | TGhost | TIce | TDark | TPsychic
```

We can pattern match variants:

```ocaml
let is_fire t = match t with
	|TFire -> "yesss"
	|_ -> "nahhhh"
	
is_fire TFire (* "yesss" *)
is_fire TDark (* "nahhhh" *)
```

We can also have more complex variants:

```ocaml
type shape =
	|Rect of float * float (*width * length*)
	|Circle of float (* radius *)
	
let area s = match s with
	| Rect(w, h) -> w *. h
	| Circle(r) -> r *. r *. 3.14
	
area Circle(1.0) (* 3.14 *)
area Rect(2.0, 5.0) (* 10.0 *)
```

We can also have **polymorphic types**, which are sort of like generics.

Consider the custom linked list type:

```ocaml
type 'a luhlist = 
	|Nil
	|Cons of ('a * 'a luhlist)
```

## records.

A **record** is a user-defined type. Take the following `pokemon` record type for instance:

```ocaml
type pokemon = {name: string; hp: int; ptype: ptype}
```

We can then consume the type as follows:

```ocaml
let char = {name = "Charmander"; hp = 39; ptype = TFire}
```

When defining a type, we use a colon between properties and types, but when declaring a variable of that type, we use equal signs to assign properties their values.

We can destructure record fields in pattern matching:

```ocaml
let char_hp = match char with
	|{name=n; hp=h; ptype=t} -> h
	
char_hp = 39 (* true *)
```

The above example is pretty stupid. We can directly access the members of a record:

```ocaml
char.ptype (* TFire *)
```





