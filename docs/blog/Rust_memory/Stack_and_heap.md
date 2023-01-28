---
draft: true 
date: 2023-01-26
categories:
  - Rust
---

# The Stack and the Heap

### This blog is adapted from [rust-lang](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html#:~:text=Ownership%20is%20a%20set%20of,a%20computer's%20memory%20while%20running.)

Both the stack and the heap are parts of memory available to your code to use at runtime.

## Stack
The stack stores values LIFO. All data stored on the stack must have a known, fixed size. Data with an unknown size at compile time or a size that might change must be stored on the heap instead.

Pushing to the stack is faster than allocating on the heap because this process does not have to search for a place to store new data: that location is always at the top of the stack. 

## Heap
When you put data on the heap, you request a certain amount of space. The memory allocator finds an empty spot in the heap that is big enough, marks it as being in use, and returns a pointer to that location. This process is called allocating on the heap and is sometimes abbreviated as just allocating.

Comparatively, allocating space on the heap requires more work because the allocator must first find a big enough space to hold the data and then perform bookkeeping to prepare for the next allocation.

Accessing data in the heap is slower than accessing data on the stack because you have to follow a pointer to get there. Contemporary processors **are faster if they jump around less in memory**. 

## Owenership x stack & heap 
Once you understand [ownership](/Ownership_in_Rust), you won’t need to think about the stack and the heap very often, but knowing that the main purpose of ownership is to manage heap data can help explain why it works the way it does.