# Ownership in Rust

## Here I want to ask:

- What can be an owner in Rust? Thread? Scope? Function? Variable?
- Are there any differences among these ownerships?

## The problem of mem alloc

In most languages without a GC, when mem is not used anymore, programmers should call code to explicitly free it, just as when they requested it. 

This is difficult. If we forget, we’ll waste memory. If we do it too early, we’ll have an invalid variable. If we do it twice, that’s a bug too. We need to pair exactly one allocate with exactly one free.

## The third way (adapted from [rust-lang.org](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html#:~:text=Ownership%20is%20a%20set%20of,a%20computer's%20memory%20while%20running.))

Ownership is **a set of rules** that govern how a Rust program manages memory. 

Some languages use garbage collection, others need the programmer to manually allocate. Rust uses a third approach: memory is managed through ownership that the compiler checks. If any of the rules are violated, the program won’t compile.

## These Rules

- Each value in Rust has an owner (yes but who are these epping owners?).
- There can only be one owner at a time.
- When the owner goes out of scope, the value will be dropped.

## Example 1: Variable and Value
This code here does not compile becuase  s1 was moved into s2: s1 ain't no more.
```
fn main() {
    let s1 = String::from("hello");
    let s2 = s1;
    println!("{}, world!", s1);
}
```
Rephrasing this stuff in terms of ownership, what may we say?

It could be: s1 owned the value of s1 and now s2 owns it. There is only 1 copy of the value through and through, and it was moved from s1 to s2. Post-movement, s1 has left us with nothing but its empty shell. The soul of s1 ain't no more. R.I.P. 

But alas, the dark magic of Lord Voldemort can copy the soul of s1 while breathing life into s2. He can have the soul and eat it too. I don't know if Trump can do the same sorta thing.

## Example 2: Ownership and Functions

The page says: **"Passing a value to a function is like binding a value to a variable"**
I never thought about it that way. Interesting innit? The next thing is naturally: **"Passing a variable to a function will move or copy, just as assignment does"**

Passing a variable to a function will move or copy, just as assignment does

Passing a variable to a function will move or copy, just as assignment does. Listing 4-3 has an example with some annotations showing where variables go into and out of scope.
