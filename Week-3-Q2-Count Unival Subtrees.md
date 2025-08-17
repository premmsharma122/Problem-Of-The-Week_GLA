# Problem : Count Unival Subtrees.
In many systems, especially in distributed trees or replicated data structures, it's important to
find substructures that are uniform. A unival tree (short for universal value tree) is a subtree
where all the nodes have the same value.
You are given the root of a binary tree, and your task is to count the number of unival
subtrees present in the tree.
##  Input Format:
You will be given the root of a binary tree. Each node contains:
• An integer value
• Left and right children
For coding practice, you may build the tree manually or from helper functions.
##  Output Format:
• Print a single integer: the number of unival subtrees.
##  Approach : By using recursion.
###  -> First we know that is root is null we should return true (base case) null is also a univalue.
###  -> now we check in left and right of the given root recursivly untill root != null with this check if left & right nodes value is equal to their curr parent root or not,
###  -> If they are not equal then return false immediatly, if not then incremant count value and return true, that's every left and right recursive tree build with each call.

```java
class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) {
        this.val = val;
        this.left = null;
        this.right = null;
    }
}

class Solution {
    private int count = 0;

    public int countUnivalSubtrees(TreeNode root) {
        if (root == null) return 0;
        isUnival(root);
        return count;
    }

    private boolean isUnival(TreeNode node) {
        if (node == null) return true;

        boolean leftUnival = isUnival(node.left);
        boolean rightUnival = isUnival(node.right);

        if (!leftUnival || !rightUnival) return false;

        if (node.left != null && node.left.val != node.val) return false;        
        if (node.right != null && node.right.val != node.val) return false;
        
        count++;
        return true;
    }
}

```
## Time Comp : O(N) bcoz At each node, we do constant-time work: **No node is processed more than once → total work is proportional to the number of nodes.**
