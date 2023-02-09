09/02/2023
## Here is my iterative solution 

Apparently, it is not as elegant as the recursive one: there's too many mutables and shit. D'youknowaImean?

```Rust
type N = Option<Box<ListNode>>;
use std::mem::replace;
impl Solution {
    pub fn reverse_list(head: N) -> N{
        let (mut prev, mut cur) = (None, head.clone());
        while let Some(mut node) = cur {
            cur = replace(&mut node.next, prev);
            prev = Some(node);
        }
        prev
        
    }
}
```