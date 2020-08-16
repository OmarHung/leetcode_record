# leetcode_record
LeetCode 刷題記錄

# Arranging Coins
You have a total of n coins that you want to form in a staircase shape, where every k-th row must have exactly k coins.

Given n, find the total number of full staircase rows that can be formed.

n is a non-negative integer and fits within the range of a 32-bit signed integer.

#### Example 1:
```
n = 5

The coins can form the following rows:
¤
¤ ¤
¤ ¤

Because the 3rd row is incomplete, we return 2.
```
#### Example 2:
```
n = 8

The coins can form the following rows:
¤
¤ ¤
¤ ¤ ¤
¤ ¤

Because the 4th row is incomplete, we return 3.
```
#### Solution & Thinking
``` PHP
直接暴力，雖然通過了，但當N很大效率一定很差

class Solution {
    /**
     * @param Integer $n
     * @return Integer
     */
    function arrangeCoins($n) {
        $count = 0;
        $i = 0;
        $last_i = $i;
        while($count<$n) {
            $count += ++$i;
            if($count<=$n) $last_i = $i;
        }
        return $last_i;
    }
}
```
#### 網友解法
[[LeetCode] Arranging Coins 排列硬币](https://www.cnblogs.com/grandyang/p/6026066.html) 
