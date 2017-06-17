## 221. Maximal Square
Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

For example, given the following matrix:

```
1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0
```
Return 4.

### Solution 1
动态规划，状态方程为
- i == 0|| j == 0 代表只有一行（不可能为长度大于2的正方形），所以`dp[i][j] = matrix[i][j] - '0'`就等于matrix的值
- matrix[i][j] = '1'时 `dp[i][j] =  Math.min(Math.min(dp[i][j-1],dp[i-1][j]),dp[i-1][j-1]) + 1;` 
- matrix[i][j] = '0'时 `dp[i][j] = 0`

```java
public class Solution {
    public int maximalSquare(char[][] matrix) {
        if(matrix == null|| matrix.length==0||matrix[0].length==0)return 0;
        int m = matrix.length, n = matrix[0].length;
        int[][] dp = new int[m][n];
        int maxsize = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if(i==0||j==0)dp[i][j] = matrix[i][j] - '0';
                else if(matrix[i][j] == '0'){
                    dp[i][j] = 0;
                }else {
                    dp[i][j] = Math.min(Math.min(dp[i][j-1],dp[i-1][j]),dp[i-1][j-1]) + 1;
                }
                maxsize = Math.max(dp[i][j], maxsize);
            }
        }
        return maxsize*maxsize;
    }
}
```

### Solution 2
由于只需要用到dp[i-1][j-1]、dp[i-1][j]和dp[i][j-1]，所以可以直接保存前一行的操作记录，空间复杂度将变为O(n)

```java
public class Solution {
    public int maximalSquare(char[][] matrix) {
        if(matrix == null|| matrix.length==0||matrix[0].length==0)return 0;
        int m = matrix.length, n = matrix[0].length;
        int maxsize = 0;
        int[] pre = new int[n], cur = new int[n];
        for (int i = 0; i < n; i++) {
            pre[i] = matrix[0][i] - '0';
            maxsize = Math.max(pre[i],maxsize);
        }
        for (int i = 1; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if(j==0)cur[j] = matrix[i][j] -'0';
                else if(matrix[i][j]=='1'){
                    cur[j] = Math.min(Math.min(pre[j-1],pre[j]),cur[j-1])+1;
                }else{
                    cur[j] = 0;
                }
                maxsize = Math.max(cur[j],maxsize);
                
            }
            pre = Arrays.copyOf(cur, n);
        }
        return maxsize*maxsize;
    }
}
```

### Solution 3
直接在上一行中修改，记得保存(i-1,j-1)的值，不懂的话，可以在草稿纸上模拟下，应该就能明白。

```java
public class Solution {
    public int maximalSquare(char[][] matrix) {
        if(matrix == null|| matrix.length==0||matrix[0].length==0)return 0;
        int m = matrix.length, n = matrix[0].length;
        int maxsize = 0;
        int[] dp = new int[n+1];
        int pre = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 1; j <= n; j++) {
                int tmp = dp[j];
                if (matrix[i][j-1] == '1') {
                    dp[j] = Math.min(Math.min(dp[j - 1], dp[j]), pre) + 1;
                }else{
                    dp[j] = 0;
                }
                maxsize = Math.max(dp[j], maxsize);
                pre = tmp;
            }
        }
        return maxsize*maxsize;
    }
}
```