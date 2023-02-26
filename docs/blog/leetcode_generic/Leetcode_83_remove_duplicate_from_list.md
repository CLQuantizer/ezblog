26/02/2023

## As title suggests

```Rust 
use std::collections::HashSet;
impl Solution {
    pub fn delete_duplicates(head: Option<Box<ListNode>>) -> Option<Box<ListNode>> {
        match head {
            Some(mut node) => {
                // create a new HashSet to keep track of seen values
                let mut s = HashSet::new(); 
                // add the value of the first node to the HashSet
                s.insert(node.val); 
                // create a mutable reference to the first node
                let mut cur = &mut node; 
                // iterate while there are still nodes to check
                while cur.next.is_some() { 
                    // if there is a next node
                    // this line is hella hard. why do I need to .take()?
                    if let Some(next_node) = cur.next.take() { 
                        // if the next node's value has already been seen
                        if s.contains(&next_node.val) {
                            // skip the next node by setting the current node's 
                            // next pointer to the node after the next node 
                            cur.next = next_node.next; 
                        } else {
                            // add the next node's value to the HashSet
                            s.insert(next_node.val); 
                            // set the current node's next pointer to the next node
                            cur.next = Some(next_node); 
                            // set the current node to the next node
                            //why do I need to unwrap?
                            cur = cur.next.as_mut().unwrap(); 
                        }
                    }
                }
                // return the head of the deduplicated linked list
                Some(node) 
            },
            // if the linked list is empty, return None
            None => None 
        }
    }
}
```

## Weird little programme
I also wrote thie weird shit:

```Rust
fn main() {
    let world = String::from("World");
    let mut opt = Some(String::from("Hello "));
    let r = &mut opt;

    // if I don't do the take here I will be screwed
    match r.take(){
        Some(mut x) =>{
            x=x+&world;
            dbg!(x);},
        None => ()
    }
}
```