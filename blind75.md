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

## 2. [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
| Time    | Space    | Tags           |
|-------- | -------- | -------------- |
| O(n) | O(n) | Array, Dynamic Programming |

```java
class Solution {
    public int maxProfit(int[] prices) {
        int maxProfit = 0;
        int lowestPrice = prices[0];
        for (int i = 1; i < prices.length; i++){
            if (prices[i] < lowestPrice){
                lowestPrice = prices[i];
            } else {
                maxProfit = Math.max(maxProfit, prices[i]-lowestPrice);
            }
        }
        return maxProfit;
    }
}
```

<details>
<summary>Improvements/Notes</summary>
<br>
Background 
    - you need to find the lowest number and the highest number in the array such that the lowest number is to the left of the highest number.
    - this is a specific target, you don't need to iterate through the array twice
    - you iterate left to right in the array, starting from the second element (assuming your first element is the lowest)
    - if your new element is smaller than the lowest, replace it
    - otherwise check if your new maxprofit is bigger than your odl max profit and replace if necessary. 

Improvements
- edge cases maybe? look up how to improve this?
- why is this dynamic programming? we didn't really brute force every solution did we?
</details>


## 3. [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)
| Time    | Space    | Tags           |
|-------- | -------- | -------------- |
| O(n) | O(n) | Array, Hash Table, Sorting |

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Set<Integer> set = new HashSet<>();
        for (int i = 0 ; i < nums.length; i++){
            set.add(nums[i]);
            if (set.size() <= i){
                return true;
            }
        }
        return false;
    }
}
```

<details>
<summary>Improvements/Notes</summary>
<br>
Improvements
- you can sort the array first if your solution requires less memory
- you can use a hashtable if you need to keep track of exactly how many occurrences came up
- brute force, not exactly sure why youd' need this. maybe if time complexity wasn't a big deal, space complexity was a big deal and you needed easily understandable code. 
</details>

## 4. [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)
| Time    | Space    | Tags           |
|-------- | -------- | -------------- |
| O(n) | O(n) | Array, Prefix Sum |
```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int[] products = new int[nums.length];

        // prep products array for having other numbers multiplied onto it
        for (int i=0; i < products.length; i++){
            products[i] = 1;
        }

        // add prefices into product array
        int prefix = 1;       
        for (int i = 0; i < products.length; i++){
            products[i] *= prefix;
            prefix *= nums[i];
        }

        // add suffices into product array
        int suffix = 1;
        for (int i = products.length-1; i >= 0; i--){
            products[i] *= suffix;
            suffix *= nums[i];
        } 

        return products;
    }
}
```
<details>
<summary>Improvements/Notes</summary>
<br>
Improvements
    - the separate initialization of the prefix and suffix makes the code run slower, but it makes the code more readable so i left it in. 
    - if you want easier to understand code and don't have problems with space complexity, you could have 2 arrays - one for prefix, one for suffix. 
    - if you could remove the zero from your input set, you could likely just find the product once and then divide by each nums[i] - this would make the runtime O(2n) instead of O(3n)
</details>

## 4. [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)
| Time    | Space    | Tags           |
|-------- | -------- | -------------- |
| O(n) | O(n) | Array, Prefix Sum |



