---
    date: 2023-01-28
---
28/01/2023

## A favourite of mine
LeetCode[No.1 MokuHazushi.md](No.1%20MokuHazushi.md) 206 is my all-time favourite algo problem, much more than 2sum.
In this section, I lay all the 0ms-beats-100% answers together, compare them, and comment on their code, in order to learn a thing or two while having fun.

### The settings for Rust
```
Definition for singly-linked list.
#[derive(PartialEq, Eq, Clone, Debug)]
pub struct ListNode {
  pub val: i32,
  pub next: Option<Box<ListNode>>
}
 
impl ListNode {
  #[inline] 
  // first of al I don't understand what this #[inline] thing is
  fn new(val: i32) -> Self {
    ListNode {
      next: None,
      val
    }
  }
}
```