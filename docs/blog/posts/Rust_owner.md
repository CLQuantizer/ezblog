# Ownership in Rust

## Here I want to ask:

- What can be an owner in Rust? Thread? Scope? Function? Variable?
- Are there any differences among these ownerships?

## The third way

### Below is adapted from [rust-lang.org](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html#:~:text=Ownership%20is%20a%20set%20of,a%20computer's%20memory%20while%20running.)

Ownership is **a set of rules** that govern how a Rust program manages memory. 

Some languages use garbage collection, others need the programmer to manually allocate. Rust uses a third approach: memory is managed through ownership that the compiler checks. If any of the rules are violated, the program won’t compile.