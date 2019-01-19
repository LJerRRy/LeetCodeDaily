## 617. Merge Two Binary Trees
Given two binary trees and imagine that when you put one of them to cover the other, some nodes of the two trees are overlapped while the others are not.

You need to merge them into a new binary tree. The merge rule is that if two nodes overlap, then sum node values up as the new value of the merged node. Otherwise, the NOT null node will be used as the node of new tree.
## Summary
合并两个二叉树，从根节点开始合并
## Solution
只需遍历二叉树，这里就用先序遍历
### Approach#1
下面这方法当t1和t2中有一个节点为空的时候就会使用原来的节点，最好改为新建一个节点，见方法二
- 时间复杂度：O(n)
- 空间复杂度：O(n)

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
    public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
        if(t1==null&&t2==null)return null;
        if(t1==null||t2==null)return t1==null?t2:t1;
        TreeNode r = new TreeNode(t1.val+t2.val);
        r.left = mergeTrees(t1.left, t2.left);
        r.right = mergeTrees(t1.right, t2.right);
        return r;
    }
}
```
### Approach#2

- 时间复杂度：O(nlogn)
- 空间复杂度：O(n)

```java
public class Solution {
    public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
        if (t1 == null && t2 == null) return null;
        
        int val = (t1 == null ? 0 : t1.val) + (t2 == null ? 0 : t2.val);
        TreeNode newNode = new TreeNode(val);
        
        newNode.left = mergeTrees(t1 == null ? null : t1.left, t2 == null ? null : t2.left);
        newNode.right = mergeTrees(t1 == null ? null : t1.right, t2 == null ? null : t2.right);
        
        return newNode;
    }
}
```