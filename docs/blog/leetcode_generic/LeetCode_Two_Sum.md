10/02/2023


**Map takes &Q**: this is what I have learned from LeetCode 1 Two Sum

```Rust
use std::collections::HashMap;
impl Solution {
    pub fn two_sum(nums: Vec<i32>, target: i32) -> Vec<i32> {
        let mut map = HashMap::new();
        for i in 0..nums.len(){
            
            // You have to pass &Q into map.contains_key(&Q)
            if map.contains_key(&nums[i]){
            
                // Similarly, you have to pass &Q into map[&Q]
                return vec![i as i32, map[&nums[i]]];
            }
            map.insert(target-nums[i], i as i32);       
        }
        vec![]
    }
}
```