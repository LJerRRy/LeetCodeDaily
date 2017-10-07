## 652. Find Duplicate Subtrees
Given a binary tree, return all duplicate subtrees. For each kind of duplicate subtrees, you only need to return the root node of any one of them.

Two trees are duplicate if they have the same structure with same node values.

Example 1: 

```
        1
       / \
      2   3
     /   / \
    4   2   4
       /
      4
```
The following are two duplicate subtrees:

```
      2
     /
    4
```
and

```
    4
```
Therefore, you need to return above trees' root in the form of a list.

## Summary

## Solution

### Approach#1
通过遍历二叉树，生成字符串，来判断是否相等。

- 时间复杂度：O(n)
- 空间复杂度：O(n)

```java
public class Solution {
    public List<TreeNode> findDuplicateSubtrees(TreeNode root) {
        List<TreeNode> l = new LinkedList<>();
        postOrder(root, new HashMap<String, Integer>(), l);
        return l;
    }
    
    String postOrder(TreeNode t, Map<String, Integer> map, List<TreeNode> res){
        if(t==null)return "#";
        String s = "("+t.val+" "+postOrder(t.left, map, res)+" "+postOrder(t.right, map, res)+")";
        map.put(s, map.getOrDefault(s, 0)+1);
        //这里必须为等于，不能是大于1，否则就会出现重复的节点。
        if(map.getOrDefault(s,0)==2)res.add(t);
        return s;
    }
}
```
### Approach#2

- 时间复杂度：O(nlogn)
- 空间复杂度：O(n)

```java

```