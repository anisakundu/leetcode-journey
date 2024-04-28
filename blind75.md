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

04/28/24 - after Maximum subarray problem
- is there a dp subproblem here? no i don't think so. you're looking for one particular target in the whole array. you can't break up that array now.
    
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
- 04/28/24 - after Maximum subarray problem
   - is there a dp subproblem here? yes, i think the use of max here to compare between the existing max profit and the new potential profit shows you're creating multiple solutions to the same problem and comparing them for the optimal one. 
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
    04/28/24
    - i don't think this is dp because there's exactly one solution, you don't have to compute multiple potential solutions and compare them. 
</details>

## 5. [Maximum SubArray](https://leetcode.com/problems/maximum-subarray/)
| Time    | Space    | Tags           |
|-------- | -------- | -------------- |
| O(n) | O(n) | Array, Divide&Conquer, Dynamic Programming |
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int currSum = nums[0];
        int maxSum = nums[0];

        for (int i = 1; i < nums.length; i++){
            currSum = Math.max(nums[i], nums[i] + currSum);
            maxSum = Math.max(maxSum, currSum);
        }
        
        return maxSum;
    }
}
```
<details>
<summary>Improvements/Notes</summary>
<br>
Improvements
    - need to watch video on this: [Max Contiguous Subarray Sum - Cubic Time To Kadane's Algorithm ("Maximum Subarray" on LeetCode)](https://www.youtube.com/watch?v=2MmGzdiKR9Y&pp=ygUqbWF4aW11bSBzdWJhcnJheSBsZWV0Y29kZSBiYWNrIHRvIGJhY2sgc3dl)
        - you're dealing with DP when you need to break up a problem into the same type of subproblems (so that you don't repeat your work - you can think about the idea that if you can use recursion to solve this problem, you can use DP) ?? very shaky on this explanation
        - strong takeaway: in this problem, you can identify the subproblem that gets repeated - you need to find the contiguous subarray with max sum in every array in your problem. if your original array had 8 elements, you need to find this max sum contiguous subarray for subarray[0:0], subarray[0:1], subarray[0:2], subarray[0:3]... subarray[0:8]. you only add on the previous sub array max sum to your new subarray sum if its non negative (has to make your current sum bigger.
        - strong takeaway: both in this explanation and in the other explanations, it seems important to start with the most inefficient solution in interviews and work your way up to the efficient solution. maybe you don't code each solution. you just explain it. 
        - array problems usually should have an O(n) solution. look for it.
    - what would you do if they needed you to actually return the array? hashmap? between each sum and the array it's made up of.
</details>

<details>
<summary>Overall Journey/Questions</summary>
<br>
    04/28
    - writing this at paris baguette, after doing leetcode for 30 min, feeling exhausted from realizing how much there is I don't know, and realizing I definitely could benefit from not napping every time this happens. (it takes so long to nap and then disengage and re engage with this when i'm feeling better. I'd rather push the tiredness away directly right now)
- how do i know i'll be able to identify questions like this? and identify when to use this solution? i haven't really come across a repeat solution yet. 
- right now, i'm not afraid of doing too much, like having to do 500 leetcode problems instead of 75 - but eventually I'll start becoming afraid of this. Because it'll seem like there's no end. I think I kind of have to commit to doing both: continuing pursuing the path I chose (like doing a list of 75 problems), and entertaining these opportunities to see if i could be learning this faster (like dedicating additional time to watch videos on the patterns behind these problems). And I still promised myself I'd take a mock interview by the time I'm done with those 75 problems. I don't want to delay getting those problems done because I'm watching tangential videos. I should set a hard deadline for getting through these interviews. 
    - it's taking me approximately 30 min / problem right now (just to categorize, try out a solution, and go back understand how to implement the correct solution. not very able to find patterns within these 30 min). i can handle probably 5 per day if I'm diligent, I'm accomplishing maybe 2-3 on a a daily basis though. If I do 5 per day, it should take 2 weeks. I will aim for booking an interview the week of May 13-17.
    - that being said, I found these videos / articles I want to watch / read to understand more about the patterns before I take the mock interview but maybe not before I'm done with these problems. maybe I can understand patterns for one day after each leet code category. (or perhaps before would also work).
    - also just being reminded of the fact that i think i've been looking for patterns for a while and i didn't want to settle for having to do a 1000 problems and not really knowing what type of intuition was built such that i could now pass interviews. I think the fact that those paid workshops led with that offer of showing you the patterns made me believe i had to pay for it. but i think i just had to trust my instinct that i should be looking for patterns, and look for them for free online. and believe that i'd be able to find the patterns online if these people who were asking for so much money were able to find it. I should pay more attention to why some statements appeal to me, rather than immediately believing that blindly following the people who said them will solve all my problems. 

   Array
     - dp intro: https://www.google.com/search?sca_esv=1d62dda5da21c497&sca_upv=1&sxsrf=ACQVn0_Tp_RrN9n6IveIB4RNM0qIVXkyXg:1714331329032&q=best+introduction+to+dynamic+programming&tbm=vid&source=lnms&prmd=vsibnmt&sa=X&ved=2ahUKEwj_sZPvzeWFAxXMODQIHXoCDHQQ0pQJegQICxAB&biw=1440&bih=813&dpr=1#fpstate=ive&vld=cid:baadfd58,vid:Clp5c7HvLqs,st:0
     - patterns: https://hackernoon.com/14-patterns-to-ace-any-coding-interview-question-c5bb3357f6ed
     - really long course on patterns (?) https://www.educative.io/courses/grokking-coding-interview-patterns-java
      - need to watch video on this: [Max Contiguous Subarray Sum - Cubic Time To Kadane's Algorithm ("Maximum Subarray" on LeetCode)](https://www.youtube.com/watch?v=2MmGzdiKR9Y&pp=ygUqbWF4aW11bSBzdWJhcnJheSBsZWV0Y29kZSBiYWNrIHRvIGJhY2sgc3dl)
        - you're dealing with DP when you need to break up a problem into the same type of subproblems (so that you don't repeat your work - you can think about the idea that if you can use recursion to solve this problem, you can use DP) ?? very shaky on this explanation
        - strong takeaway: in this problem, you can identify the subproblem that gets repeated - you need to find the contiguous subarray with max sum in every array in your problem. if your original array had 8 elements, you need to find this max sum contiguous subarray for subarray[0:0], subarray[0:1], subarray[0:2], subarray[0:3]... subarray[0:8]. you only add on the previous sub array max sum to your new subarray sum if its non negative (has to make your current sum bigger.
        - strong takeaway: both in this explanation and in the other explanations, it seems important to start with the most inefficient solution in interviews and work your way up to the efficient solution. maybe you don't code each solution. you just explain it. 
        - array problems usually should have an O(n) solution. look for it.
</details>


