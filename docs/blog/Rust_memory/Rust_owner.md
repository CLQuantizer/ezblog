# Ownership in Rust

## Here I want to ask:

- What can be an owner in Rust? Thread? Scope? Function? Variable?
- Are there any differences among these ownerships?

## Short answers to our questions

- Owners include functions and variables. They own values (but what are values?)
- Ownership is ownership. It is memroy talk. 

## The problem of mem alloc

In most languages without a GC, when a chunk of memory ain't used anymore, programmers should call code to explicitly free it, just as when they requested it.

This is difficult: if we forget to free, we’ll waste memory. If we do it too early, we’ll have an invalid variable. If we do it twice, that’s a bug too. We need to pair exactly one **allocate** with exactly one **free**.
## The third way (adapted from [rust-lang.org](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html#:~:text=Ownership%20is%20a%20set%20of,a%20computer's%20memory%20while%20running.))

Ownership is **a set of rules** that govern how a Rust program manages memory. 

Some languages use garbage collection, others need the programmer to manually allocate. Rust uses a third approach: memory is managed through ownership that the compiler checks. If any of the rules are violated, the program won’t compile.

## These Rules

- Each value in Rust has an owner (yes but who are these epping owners?).
- There can only be one owner at a time.
- When the owner goes out of scope, the value will be dropped.

## Example 1: Ownership x Variables

**A variable can own a value** --Albert Einstein

First, look at this code which ain't compiling. The error is **"s1 has been moved."**
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

## Example 2: Ownership x Functions

The page says: **"Passing a value to a function is like binding a value to a variable"**
I never thought about it that way. Interesting innit? The next thing is naturally: **"Passing a variable to a function will move or copy, just as assignment does"**

**A function can own a value** --Ludwig Von Neumann
Take a look at the next bit of code which ain't compiling because:  **"value borrowed after move"**
```
fn main() {
    let s1 = String::from("Kaggle");
    take_soul_of_prey(s1);
    println!("I am {}", s1);
}

fn take_soul_of_prey(prey: String){
    println!("I own the soul of {}", prey);
}
```
It is quite clear that the soul of the prey ("Kaggle" of type String) is taken. But if the prey ain't got a soul, that is, if they are a integer of a cxxxxnist who do not live on the heap with normal people, they are fine.

## Example 3: Ownership x Return values
Take a look at the next bit of code which compiles like butter:

```
fn main() {
    let s1 = String::from("Kaggle");
    let s1 = takes_and_returns(s1);
    println!("I am {}", s1);
}

fn takes_and_returns(prey: String) -> String{
    println!("I lowkey possess the soul of {}", prey);
    prey
}
```

It is simple as that: the soul of the prey was returned and bound to s1 again. This resurrection is epic and deeply personal. 

You should always look for the Rust in other people. How is Rust talking to you? What does ownership mean to you? How can you realize yourself in Rust. Join our Rust reading group to get closer to Rust. We have free pizza afterwards as well.

But heck, what about **thread**?
Is a thread a function? A variable? What is a thread? 
In Java, it is an instance of the **[Thread](https://docs.oracle.com/en/java/javase/19/docs/api/java.base/java/lang/Thread.html)** class which implements the **[Runnable](https://docs.oracle.com/en/java/javase/19/docs/api/java.base/java/lang/Runnable.html)** interface