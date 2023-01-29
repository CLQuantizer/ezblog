---
    date: 2023-01-28
---
### [MokuHazushi the humble starter](https://leetcode.com/problems/reverse-linked-list/solutions/1980282/rust-iterative/)

```rust
impl Solution {
    pub fn reverse_list(head: Option<Box<ListNode>>) -> Option<Box<ListNode>> {
        let mut cur_node = None;
        let mut iter = head.as_ref();
        while iter != None {
            if let Some(ref node) = iter {
                let mut new_node = ListNode::new(node.val);
                if cur_node != None {
                    if let Some(cur_box) = cur_node {
                        new_node.next = Some(cur_box);
                    }
                }
                cur_node = Some(Box::new(new_node));
                iter = node.next.as_ref();
            }
        }
        cur_node
    }
}
```
Ok. line by line: 

        let mut cur_node = None;

current node has to be mutable because we later re-assign a value to it.

        let mut iter = head.as_ref();

What is iter doing here? Why do we need it? What is .as_ref()? 
Is it brought by a trait?

         if let Some(ref node) = iter {...}

1. what does ref mean? 
2. On what occasion is it false? When iter refers to a thing that is None?
3. & vs ref, what are the differences? 
   1. & denotes that your pattern expects a reference to an object. Hence & is a part of said pattern: &Foo matches different objects than Foo does. 
   2. ref indicates that you want a reference to an unpacked value.
         It is not matched against: Foo(ref foo) matches the same objects as Foo(foo).
4. Looks like there is no difference between ref and &. I'll just stick to &


### Conclusion
I did not understand how the code works.
The naming is not easy to understand. Maybe I'll come back to this in the future
