## Here is my recursive solution 
```Rust
type N = Option<Box<ListNode>>;
// Give the super long type a shorter name

use std::mem::replace;
//Prev-use the mem func from the namespace

fn one_more_arg(cur: N, prev: N) -> N{
// one more arg means one more arg than the provided reverse_list()
// I needed to pass both head and prev to the call-stack

        if let Some(mut node) = cur {
        // I am getting better at this shit
        // I mean the essential skill of "if let"
            one_more_arg(replace(&mut node.next, prev), Some(node))
        }else{
            prev
        }
    }
impl Solution {
    pub fn reverse_list(head: N) -> N{
        // notice that head passed into one_more_arg and eaten there
        // Dammit! This is too dope, bruv
        one_more_arg(head, None)
    }
}
```

Here is a more idiomatic version with `match`

``` Rust
type T = Option<Box<ListNode>>;
impl Solution {
    pub fn reverse_list(head: T) -> T {
               cur_prev(head, None)
    }
}

fn cur_prev(cur: T, prev: T) -> T{
    match cur{
        Some(mut node) => cur_prev(std::mem::replace(&mut node.next, prev), Some(node)),
        None => prev
    }
}
```