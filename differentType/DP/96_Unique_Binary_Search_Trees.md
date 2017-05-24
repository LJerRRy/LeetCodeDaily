## 96. Unique Binary Search Trees
Given n, how many structurally unique BST's (binary search trees) that store values 1...n?

### Solution 1
用dp来解决. 状态方程f(i,n) = G(i-1)*G(n-i) 其中f(i,n)中n代表二叉树总共有n个节点，f(i,n)以i为根结点的个数值。G(i-1)表示i-1个节点二叉搜索树的个数，而G(n-i)代表右子树的二叉搜索树的个数。**因为我们不关心一个二叉搜索树里面的节点值，只关心二叉树中的节点数。**对于右子树的二叉搜索树的种类个数就可以等价于右子树节点个数的二叉搜索树的个数即G(i-1).

最后要求G(n) =  f(1,n) + f(2,n) + ... + f(n,n)。需要注意的是初始化dp时dp[0] = 1;因为如果某一子树为空那么只有一种可能。

```java
public class Solution {
    public int numTrees(int n) {
        // dp相对于G(n)
        int[] dp = new int[n+1];
        dp[0] = 1;
        for (int i = 1; i < n + 1; i++) {
            //这里t相当于f函数
            int t = 0;
            for (int j = 1; j <= i; j++) {
                t += dp[j-1]*dp[i-j];
            }
            dp[i] = t;
        }
        return dp[n];
    }
}
```
