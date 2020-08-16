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
Runtime: 240 ms
Memory Usage: 15 MB

class Solution {
    /**
     * @param Integer $n
     * @return Integer
     */
    function arrangeCoins($n) {
        $count = 0; //總硬幣數
        $i = 0; //第幾階
        $last_i = $i; //上一階
        while($count<$n) { //總硬幣數少於給定硬幣數
            $count += ++$i; //總硬幣數加上該階硬幣數
            if($count<=$n) $last_i = $i; //若總硬幣數<=給定硬幣數則紀錄上一階有幾個硬幣
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
就是走訪：
先從root開始往左走再往右走，走到最底紀錄值與階層，一直遞迴下去
Runtime: 12 ms
Memory Usage: 16 MB

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
    public $a = array(); //最終陣列
    function levelOrderBottom($root) {
        $this->find($root, 1);
        return $this->a;
    }
    
    /**
     * @param TreeNode $root (當前節點)
     * @param Integer $h (第幾階)
     * @return Integer[][]
     */
    function find($root, $h) {
        if($root->val !== null) { //若有值再處理
            if(count($this->a)<$h) //最終陣列內元素數<當前階層 (最終陣列內還沒有此階層的陣列)
                array_unshift($this->a, [$root->val]); //把當前節點的值以陣列形式放入最終陣列的頭
            else
                $a[count($this->a)-$h] = array_merge($a[count($this->a)-$h], [$root->val]); //把當前節點的值以陣列形式放入最終陣列同階層位置
            
            if($root->left !== null) $this->find($root->left, $h+1);
            if($root->right !== null) $this->find($root->right, $h+1);
        }
    }
}

後來存入陣列方式改成先push後反轉陣列
Runtime: 4 ms
Memory Usage: 15.8 MB

class Solution {
    /**
     * @param TreeNode $root
     * @return Integer[][]
     */
    public $a = array();
    function levelOrderBottom($root) {
        $this->find($root, 1);
        return array_reverse($this->a);
    }
    
    function find($root, $h) {
        if($root->val !== null) {
            if(count($this->a)<$h)
                array_push($this->a, [$root->val]);
            else
                $this->a[$h-1] = array_merge($this->a[$h-1], [$root->val]);
            
            if($root->left !== null) $this->find($root->left, $h+1);
            if($root->right !== null) $this->find($root->right, $h+1);
        }
    }
}
```
#### 網友解法
[LeetCode 107. Binary Tree Level Order Traversal II](https://skyyen999.gitbooks.io/-leetcode-with-javascript/content/questions/107md.html) 
