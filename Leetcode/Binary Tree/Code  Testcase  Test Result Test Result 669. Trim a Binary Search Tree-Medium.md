## Question:

Given the root of a binary search tree and the lowest and highest boundaries as low and high, trim the tree so that all its elements lies in [low, high]. Trimming the tree should not change the relative structure of the elements that will remain in the tree (i.e., any node's descendant should remain a descendant). It can be proven that there is a unique answer.  

Return the root of the trimmed binary search tree. Note that the root may change depending on the given bounds.  

Example 1:  

Input: root = [1,0,2], low = 1, high = 2  
Output: [1,null,2]  

Example 2:  

Input: root = [3,0,4,null,2,null,null,1], low = 1, high = 3  
Output: [3,2,null,1]   

Constraints:  

The number of nodes in the tree is in the range [1, 104].  
0 <= Node.val <= 104   
The value of each node in the tree is unique.  
root is guaranteed to be a valid binary search tree.  
0 <= low <= high <= 104  

---
## Thought: 
We use recursion to do it.

The trimBST method in the Solution class trims a binary search tree (BST) so that all node values fall within the range [low, high]. Here's how it works:  

Base Case: Return null if root is null, indicating there's nothing to trim.  

Out of Range Elimination:  
If root.val < low, skip the current node and its left subtree (since all would be too low) and recursively trim the right subtree.  
If root.val > high, skip the current node and its right subtree (since all would be too high) and recursively trim the left subtree.  

Recursive Trimming:  
If root.val is within [low, high], recursively trim both the left and right subtrees to ensure they also contain only values within this range.  

Construct and Return Tree: The root node connects to the recursively trimmed left and right subtrees, forming a BST that only includes nodes with values within the specified range.  

This method efficiently prunes nodes outside [low, high] and maintains the BST structure for all remaining nodes, ensuring that every node value is between low and high.  

---
## Solution: 
```Java
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
    public TreeNode trimBST(TreeNode root, int low, int high) {
        if(root == null) return root;

        if(high < root.val) return trimBST(root.left, low, high);
        if(root.val < low) return trimBST(root.right, low, high);

        root.left = trimBST(root.left, low, high);
        root.right = trimBST(root.right, low, high);

        return root;
    }
}
```
Time complexity: O(logn)  
Space complexity: O(1)
