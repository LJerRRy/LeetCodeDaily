## 95. Unique Binary Search Trees II
Given an integer n, generate all structurally unique BST's (binary search trees) that store values 1...n.

### Solution 1
这题和96题不同的地方在于，是求出所有BST树，但也可以用和96题中一样的dp算法。

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public List<TreeNode> generateTrees(int n) {
        if(n<=0)return new LinkedList<TreeNode>();
        //相当于t()用于保存有i项的时候的所有BST树
        List<TreeNode>[] dp = new List[n+1];
        dp[0] = new LinkedList<>();
        dp[0].add(null);
        for (int i = 1; i <= n; i++) {
            dp[i] = new LinkedList<>();
            for (int j = 1; j <= i ; j++) {
                for(TreeNode nodeL : dp[j-1]){
                    for(TreeNode nodeR : dp[i-j]){
                        TreeNode node = new TreeNode(j);
                        node.left = nodeL;
                        //右子树需要在原来基础上加上j，因为右子树都比根结点大j。
                        node.right = cloneNode(nodeR, j);
                        dp[i].add(node);
                    }
                }
            }
        }
        return dp[n];
    }

    private TreeNode cloneNode(TreeNode r, int j) {
        if(r == null)return null;
        TreeNode node = new TreeNode(r.val+j);
        node.left = cloneNode(r.left, j);
        node.right = cloneNode(r.right,j);
        return node;
    }
}
```

### Solution 2
用递归

```java
public class Solution {
    public List<TreeNode> generateTrees(int n) {
        if(n<=0)return new LinkedList<TreeNode>();
        else return backtrack(1,n);
    }

    public List<TreeNode> backtrack(int start, int end){
        List<TreeNode> res = new LinkedList<>();
        //start>end说明当前节点为空，直接添加到list里，返回。
        if(start>end){
            res.add(null);
            return res;
        }
        for (int i = start; i <= end; i++) {
            List<TreeNode> left, right;
            left = backtrack(start,i-1);
            right = backtrack(i+1, end);
            for (TreeNode l : left){
                for (TreeNode r : right){
                    TreeNode node = new TreeNode(i);
                    node.left = l;
                    node.right = r;
                    res.add(node);
                }
            }
        }
        return res;
    }
}
```