# cmsc330 / final

## rust ownership.

Consider the following code:
```rust
let a: i32 = 100;
let b: i32 = a;

println!("a: {}, b: {}", a, b); // a: 100, b: 100
```

In the above example, the value in $a$ was *copied* into $b$. Primitives like `i32` are stored on the stack, which makes copying them cheaper. They implement the `Copy` trait, which allows this.

Now, consider the same thing with `String`s:
```rust
let a: String = "twizz";
let b: String = a;

println!("a: {}, b: {}", a, b); // ERROR!
```

`String` does not implement the `Copy` trait, so it errors. After the assignment to $b$​, the value of $a$​ is now *owned* by $b$​, so $a$​ is no longer accessible at the print. Know that complex types, like `String` and unlike primitives, are not copied but *moved*, in this case from $a$​ to $b$​.

We look at another example:

```rust
let x: String = "meow";

// x is in scope:
println!("x: {}", x); // meow

{
	let y: String = x; // moved! y now owns "meow"
    
    // x is no longer in scope:
    println!("y: {}", y); // meow
}

// y is out of scope, the value has been dropped:
println!("x: {}", x); // ERROR!
```

This errors, because $y$ is now out of scope, alongside its value. At the end, $x$ has no value since it got moved, so print fails.

We can use copying to avoid errors:

```rust
let x: String = "meow";

// x is in scope:
println!("x: {}", x); // meow

{
	let y: String = x.copy(); // babe wake up new "meow" dropped.
   	
    println!("y: {}", y); // meow
}

// y is out of scope, but it was a copy, so x is fine:
println!("x: {}", x); // meow
```

## rust borrowing.

Instead of copying, we can have $b$ reference $a$:

```rust
let a: String = "rust";
let b: &String = &a; // b is a reference to a

println!("a: {}, b: {}", a, b); // a: rust, b: rust
```

In the above case, $a$ is immutable. What if we wanted to change a mutable $a$ by changing $b$?

```rust
let mut a: String = "moot";
let b: &mut String = &mut a; // mutable reference

b.push_str("MEOW"); // wow we mutated.
println!("b: {}", b); // mootMEOW
```

$b$ can read and write to $a$! However, we cannot write to $a$ directly as it is borrowed. 

- If $a$ has a mutable reference, it cannot have any other references (mutable or not).
- If $a$ only has immutable references, it can have as many as possible.

A function cannot return a reference to something declared in its body, as that value will get dropped when the function call completes.

### rust lifetimes.

Something "lives" as long as it exists / is in scope / is not dropped.

```rust
let r: &i32;

{
    let x: i32 = 5;
    r = &x; // ERROR: x is bouta die.
};

println!("{}", r); // r doesn't reference anything!
```

Consider the following function:

```rust
// ERROR!
fn longest(x: &str, y: &str) -> &str {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```

This doesn't work! Why? Because Rust borrow checker can't guarantee that both $x$ and $y$​ will be alive for the body of the function.

To solve this, we introduce lifetime generics:

```rust
// MEOW!
fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```

Now we know that $x$, $y$, and the return value all have the same lifetime.

Consider the use of lifetimes in `struct`s:

```rust
struct Person<'a> {
    name: &'a str,
    age: i32,
}

fn print_struct<'a>(s: &'a Person<'a>) {
    println!("Name: {}", s.name);
    println!("Age: {}", s.age);
}

fn main() {
    let name: &str = "John";
    let s: Person = Person { name: &name, age: 30 };
    print_struct(&s);
}
```

Okay! So, `name` has the lifetime of the main method. This is passed into the lifetime generic parameter when assigning `s`. Then, when calling `print_struct`, this is again passed into that lifetime generic parameter because `s` is passed in.

Saying the lifetime is `'static`, means we assume the value is alive for the entire program. Static lifetimes do not need generic parameters to be passed in, as Rust thinks they'll never die.