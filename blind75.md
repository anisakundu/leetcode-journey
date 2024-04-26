## 1. [Two Sums](https://leetcode.com/problems/two-sum/)

| Time    | Space    | Tags           |
|-------- | -------- | -------------- |
| O(n) | O(n) | Graph |

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
