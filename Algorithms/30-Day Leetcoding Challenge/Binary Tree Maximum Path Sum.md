##Binary Tree Maximum Path Sum

Given a non-empty binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain at least one node and does not need to go through the root.

**Example 1:**
```
Input: [1,2,3]

       1
      / \
     2   3

Output: 6
```
**Example 2:**
```
Input: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7

Output: 42
```

##Java Solution
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    int maxSum = Integer.MIN_VALUE;
    
    public int maxPathSum(TreeNode root) {
        findMaxSum(root);
        return maxSum;
    }
    
    public int findMaxSum(TreeNode root) {
        if (root == null) return 0;
        int leftPathSum = Math.max(0, findMaxSum(root.left));
        int rightPathSum = Math.max(0, findMaxSum(root.right));
        maxSum = Math.max(maxSum, leftPathSum + rightPathSum + root.val);
        return Math.max(leftPathSum, rightPathSum) + root.val;
    }
}
```

**Complexity Analysis::**
* Time: O(n) where n is the num of nodes in the tree - traversing the tree once
* Space: O(n) - n stack frames