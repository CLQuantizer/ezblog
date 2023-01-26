# Borrows and References

First up, here are some Casses-tête chinois from [rust-lang](https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html):
The Rules of References

- At any given time, you can have either one mutable reference or many immutable references.
- References must always be valid.

We'll return to these later, or not.

## I ask two questions here:

- What is mutable in a mutable reference?
- What is immutable in an immutable reference?
- What does it mean to borrow?

## Related to Example 3 in [here](/blog/Rust_memory/Rust_owner/)

Borrowing is demostrated [here](/blog/Rust_memory/Rust_owner/), but there is more. 

In short, in Rust world, borrowing is the action of creating a reference. The real life analogy of borrowing a pen from a colleague does not work here. This is because in Rust, a borrowed value cannot be modified.

When Sam Bankman-Fried, creator of FTX, sun of Jeseph Bankman from the land of freedom and prosperity the United States of America, borrowed the money from its users, did he not modify the money? Hell yeh he did, and in the wildest **[dactylic hexameter](https://en.wikipedia.org/wiki/Dactylic_hexameter)** you can imagine.

## Mutable reference by example

Compilation failures are always the best for learning:
```
fn main() {
    let s = String::from("hello");

    change(&s);
}

fn change(some_string: &String) {
    some_string.push_str(", world");
}
```
The help message from the compiler is:
    ------- help: consider changing this to be a mutable reference: `&mut String`


