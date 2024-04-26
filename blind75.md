## 1. [Two Sums](https://leetcode.com/problems/two-sum/)

| Time    | Space    | Tags           |
|-------- | -------- | -------------- |
| O(n) | O(n) | Array, HashTable |

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length; i++){
            if (map.containsKey(target-nums[i])) {
                return new int[]{i, map.get(target-nums[i])};
            }
            map.put(nums[i], i);
        }
        return new int[]{};
    }
}
```

<details>
<summary>Improvements/Notes</summary>
<br>
- could be helpful to sort the input array first and then find the indices. this would work if we had a lot of different targets but the same input array everytime.
- could use brute force if memory is a problem (not necessarily iterating through the array twice, but maybe using the contains method). 
- this is pretty hard to understand just from the code. could add descriptive comments or code ?
    
</details>
