#  Problem Statement: maximum path sum between any two nodes number binary tree
Given a binary tree where each node contains an integer value, find the maximum path sum
between any two nodes.
• The path must go through at least one node.
• The path does not need to pass through the root.
• A path is a sequence of nodes connected by edges, and each node can appear only
once.
###  Given this binary tree:
-10
/ \
9 20
/ \
15 7
Output: 42
Explanation: The path is 15 → 20 → 7 which has a sum of 42.
###  Approach : we did it by recursion.
-> First we create a helper function which is heart of this code.
-> As a parameter we pass tree's node for helper function and declare a global varible **res** for storing maximum path among all answers.
-> we maintain a base case condition to prevent infinte looping. condtions as when our root is null exits.
-> Now in helper function we create two varibel **left** and **right** they hold the right and left parts of the tree. 
-> now then we compare right + left + root value with res var and store it in res.
-> At the end of function we return the the maximum b/w right and left + root value; (Bcoz when we call ecah part it return their maximum part with it value added them so thats why
we add root value + maximum of right / left at return statement.)
###  Code :
```java
class Solution {
    private int res = Integer.MIN_VALUE;
    public int help(TreeNode r){
        if(r==null) return 0;
        int ri = Math.max(0, help(r.right));
        int left = Math.max(0,help(r.left));
        res = Math.max(res, ri + left +r.val);
        return r.val + Math.max(ri, left);
    }
    public int maxPathSum(TreeNode root) {
        res = Integer.MIN_VALUE;
        int ans = help(root);
        return res;
    }
}
```
###  Time compl : O(N) bcoz of the every node is visited exactly once.
