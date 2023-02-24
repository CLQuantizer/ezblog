24/02/2023

# 🔥 iter().fold() but into_iter().reduce().unwrap()

This problem ask you to find the single number in a list where other numbers are all duplicated exactly once.

### Bit operation
The elegant solution is bit operation:

### 1. iter().fold()

```Rust
impl Solution {
    pub fn single_number(nums: Vec<i32>) -> i32 {
        nums.iter().fold(0, |acc, x| acc ^ x)
    }
}
```

### 2. into_iter().reduce()

```Rust
impl Solution {
    pub fn single_number(nums: Vec<i32>) -> i32 {
        nums.into_iter().reduce(|acc, x| acc ^ x).unwrap()
    }
}
```


## This is fascinating.
So, iter().fold() or into_iter().reduce().unwrap()?

Why?

Here is why:

```Rust
fn main() {

    let a = vec![1, 2, 3];

    // the sum of all of the elements of the array
    let sum = a.iter().fold(0, |acc, x| acc + x);
    let m = a.iter().fold(0, |acc, x| acc + x);

    let n = a.into_iter().reduce(|acc, x| acc + x).unwrap();
    // let q = a.into_iter().reduce(|acc, x| acc + x).unwrap();
    // we cannot let q =... because a has been consumed at this point
    // if a = [1,2,3], then it is a different story.

    assert_eq!(sum, 6);
    assert_eq!(m, 6);
    
    assert_eq!(n, 6);
    // assert_eq!(q, 6);
}
```

Bascially, we can use reference to vec (produced by .iter()) for .fold().
This is because we are just folding refs to elements of the vec on a value that we initialized: 0

However, when we go with .reduce(), we are folding values of elements on each other, consuming them one by one.
We must not use a reference to vec here... dayum..

I feel so stupid.
