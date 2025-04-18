## Question:  

Given a binary tree, the task is to find the maximum path sum. The path may start and end at any node in the tree.

Example 1:
```
Input:   
     10  
    /  \  
   2   -25  
  / \  /  \  
 20 1  3  4
Output: 32
```

Explanation: Path in the given tree goes
like 10 , 2 , 20 which gives the max
sum as 32.
Example 2:
```
Input:  
     10  
   /    \  
  2      5  
          \  
          -2
Output: 17
```

Explanation: Path in the given tree goes
like 2 , 10 , 5 which gives the max sum
as 17.  

Your Task:
You don't need to take input or print anything. Your task is to complete the function findMaxSum() that takes root as input and returns max sum between any two nodes in the given Binary Tree.

Expected Time Complexity: O(N).
Expected Auxiliary Space: O(Height of the Tree).

---
## Thought:  
At every parent node, there can be tree possible path:  
1.The node itself  
2.The node plus maximum of left/right subtree's path  
3.The node plus left subtree's path and rigth subtree's path  
Pick the maximum out of these 3 possible path, repeat this for every node and keep updating the maxSum.  
Also at every node return the current path sum (maximum of node.val and node.val combined with max of subtree's path) to be considered as one of the 2 subtrees' path for its parent.

In case of null nodes at the end, 0 will be returned as the current pathSum.

---
## Solution:  
```Java
/*
Node defined as
class Node{
    int data;
    Node left,right;
    Node(int d){
        data=d;
        left=right=null;
    }
}
*/

class Solution
{
    //Function to return maximum path sum from any node in a tree.
    int maxSum = Integer.MIN_VALUE;
    int findMaxSum(Node node)
    {
        //your code goes here
        int sum = traverse(node);
        return maxSum;
    }
    
    public int traverse(Node node){
        if(node == null){
            return 0;
        }
        
        int leftSum = traverse(node.left);
        int rightSum = traverse(node.right);
        
        int maxChildSum = Math.max(leftSum, rightSum);
        
        int pathSum = Math.max(node.data, node.data + maxChildSum);
        
        pathSum = Math.max(pathSum, node.data + leftSum + rightSum);
        
        maxSum = Math.max(maxSum, pathSum);
        
        return Math.max(node.data, node.data + maxChildSum);
    }
}
```
Time complexity: O(N)  
Space complexity: O(Height of the tree)
