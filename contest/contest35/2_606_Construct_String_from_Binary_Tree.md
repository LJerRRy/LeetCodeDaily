## 606. Construct String from Binary Tree
You need to construct a string consists of parenthesis and integers from a binary tree with the preorder traversing way.

The null node needs to be represented by empty parenthesis pair "()". And you need to omit all the empty parenthesis pairs that don't affect the one-to-one mapping relationship between the string and the original binary tree.
## Summary

## Solution
先序遍历，按照要求遍历即可
### Approach#1

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
    public String tree2str(TreeNode t) {
        if(t==null)return "";
        StringBuilder sb = new StringBuilder();
        preOrder(sb, t, false);
        return sb.substring(1,sb.length()-1);
    }

    private void preOrder(StringBuilder sb, TreeNode r, boolean f){
        if (r==null){
            if(f){
                sb.append("()");
            }
            return;
        }
        sb.append("(");
        sb.append(r.val);
        if(r.left!=null||r.right!=null) {
            preOrder(sb, r.left, true);
            preOrder(sb, r.right, false);
        }
        sb.append(")");
    }
}
```
### Approach#2
同方法一，遍历的顺序变化了。先遍历值，接着遍历括号
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
    public String tree2str(TreeNode t) {
        if(t==null)return "";
        StringBuilder sb = new StringBuilder();
        preOrder(sb, t);
        return sb.toString();
    }

    private void preOrder(StringBuilder sb, TreeNode r){
        if (r==null){
            return;
        }
        sb.append(r.val);
        if(r.left!=null||r.right!=null) {
            sb.append("(");
            preOrder(sb, r.left);
            sb.append(")");
            if(r.right!=null){
                sb.append("(");
                preOrder(sb, r.right);
                sb.append(")");
            }
        }
    }
}
```

### Approach#3

```java
public class Solution {
    public String tree2str(TreeNode t) {
        if (t == null) return "";
        
        String result = t.val + "";
        
        String left = tree2str(t.left);
        String right = tree2str(t.right);
        
        if (left == "" && right == "") return result;
        if (left == "") return result +"()" + "(" + right + ")";
        if (right == "") return result + "(" + left + ")";
        return result + "(" + left + ")" + "(" + right + ")";
    }
}
```