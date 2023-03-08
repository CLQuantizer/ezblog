08/03/2023

## Nothing makes any sense.

Here I write a few snippets and show how ridiculous everything is.

```Rust
fn main() {
    let a = String::from("hello");
    let b = &a;
    let c = *b; // Error!
}
```

This does not work. Same happens for mutable ref.

## What does * do then?

Indeed if it is not deref, what the fuck does it do?
[Micouy](https://micouy.github.io/rust-dereferencing/) here talks about it: 
> dereferencing acutally isn’t the opposite of referencing in Rust

> The opposite of referencing is dropping a reference, and the deref operator **is totally unrelated** to the ref operator. 

> In Rust the meaning of & and * depend on the context.

> Given a struct ```Thing```,

```Rust
struct Thing {
    field: String,
}
```

```Rust
// Compiles. Straight and simple.
fn f1(thing: &Thing) -> &String {
    &thing.field
}

// Doesn't compile...
fn f2(thing: &Thing) -> &String {
    let tmp = thing.field;

    &tmp
}

// Compiles?!
fn f3(thing: &Thing) -> &String {
    &(thing.field)
}
```