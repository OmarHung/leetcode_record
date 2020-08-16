# leetcode_record
LeetCode 刷題記錄  

# ¤ Arranging Coins
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


# ¤ Binary Tree Level Order Traversal II
Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

#### For example: 
```
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
   
return its bottom-up level order traversal as:
[
  [15,7],
  [9,20],
  [3]
]
```
#### Solution & Thinking
``` PHP
就是走訪
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     public $val = null;
 *     public $left = null;
 *     public $right = null;
 *     function __construct($val = 0, $left = null, $right = null) {
 *         $this->val = $val;
 *         $this->left = $left;
 *         $this->right = $right;
 *     }
 * }
 */
class Solution {
    /**
     * @param TreeNode $root
     * @return Integer[][]
     */
    function levelOrderBottom($root) {
        return $this->find($root, array(), 1);
    }
    
    function find($root, $a, $h) {
        if($root->val !== null) {
            if(count($a)<$h)
                array_unshift($a, [$root->val]);
            else
                $a[count($a)-$h] = array_merge($a[count($a)-$h], [$root->val]);
            
            if($root->left !== null) $a = $this->find($root->left, $a, $h+1);
            if($root->right !== null) $a = $this->find($root->right, $a, $h+1);
        }
        
        return $a;
    }
}
```
#### 網友解法
[LeetCode 107. Binary Tree Level Order Traversal II](https://skyyen999.gitbooks.io/-leetcode-with-javascript/content/questions/107md.html) 
