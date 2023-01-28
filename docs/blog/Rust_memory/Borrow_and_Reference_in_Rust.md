---
draft: true 
date: 2023-01-26
categories:
  - Rust
---
## Borrows and References

First up, here are some Casses-tête chinois from [rust-lang](https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html):
The Rules of References

- At any given time, you can have either one mutable reference or many immutable references.
- References must always be valid.

We'll return to these later, or not.

## I ask three questions here:

- What is mutable in a mutable reference?
- What is immutable in an immutable reference?
- What does it mean to borrow?

## Borrowing has been shown [here](/blog/Rust_memory/Ownership_in_Rust)

In short, in Rust world, **borrowing is the action of creating a reference**.

The real life analogy of borrowing a pen from a colleague does not seem work here. This is because in Rust, a borrowed value cannot be modified. By writing with the pen, you modify the amount of ink in it. By borrowing the Mona List, you take away 1/3 of the revenue of the Louvre according to some study of Harvard University in 1876.

When Sam Bankman-Fried, creator of FTX, son of Jeseph Bankman from the land of freedom and prosperity the United States of America, borrowed the money from its users, did he not modify the money? Hell yeh he did, and in the wildest **[dactylic hexameter](https://en.wikipedia.org/wiki/Dactylic_hexameter)** you can imagine.

And, there are two types of borrowing/referencing in Rust: mut ref and immut ref  

## Mutable reference by example

Compilation failures are always the best for learning:
```
fn main() {
    let s1 = String::from("Kaggle");
    borrows(&s1);
    println!("{}", s1);
}

fn borrows(prey: &String){
    prey.push_str(" is so dead");
}

```
The help message from the compiler is:
    ------- help: consider changing this to be a mutable reference: `&mut String`

So that is what I did to turn it into the program below. Note that s1 has to be declared **mut** too. Otherwise it ain't compile.

```
fn main() {
    let mut s1 = String::from("Kaggle");
    borrows(&mut s1);
    println!("{}", s1);

}

fn borrows(prey: &mut String){
    prey.push_str(" is so dead");
}
```

It compiles and says Kaggle is so dead.

Up to this point, it seems that a mutable reference is **a mutable reference to a mutable variable**. 

Let's table these babies shall we?

|           | mut var          | immu var      |
|-----------|------------------|---------------|
| mut ref   | ✔️ one and only ❤️ | ⛌             |
| immut ref | ✔️ promiscuous    | ✔️ promiscuous |

I'm not even sure if this correct. Lol.

## Answers to questions:
- To borrow is to refer
- What is mutable in a mutable reference is the value borrowed from a poor mutable variable.
- What is immutable in a immutable reference is, well, I don't care.