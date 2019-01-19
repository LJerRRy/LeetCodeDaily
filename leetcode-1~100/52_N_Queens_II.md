## 52. N-Queens II
Follow up for N-Queens problem.

Now, instead outputting board configurations, return the total number of distinct solutions.
## Solution

### Solution 1

```java
public class Solution {
    int cnt = 0;
    public int totalNQueens(int n) {
        if(n<=1)return 1;
        int[] c = new int[n+1];
        boolean[] f = new boolean[n];
        backtrack(n, c, f, 1);
        return cnt;
    }
    private void backtrack(int n, int[] c, boolean[] f, int cur){
        if(cur == n+1)cnt++;
        else{
            for(int i = 0;i<n;i++){
                if(!f[i]&&valid(c, cur, i+1)){
                    c[cur] = i+1;
                    f[i] = true;
                    backtrack(n, c, f, cur+1);
                    c[cur] = 0;
                    f[i] = false;
                }
            }
        }
    }
    private boolean valid(int[] c, int x, int y){
        for(int i = 1;i<x;i++){
            if(isInLine(x,y, i, c[i])){
                return false;
            }
        }
        return true;
    }
    
    // 判断皇后是否在同一对角线或者在同一行或者同一列上
    private boolean isInLine(int i, int j, int ro, int co) {
        // 其中肯定ro != i，因为i<ro
        return Math.abs(1.0*(ro-i)/(co-j))==1||co==j;
        // return (ro+co) == i+j || ro + j == co + i || co == j;
    }
}
```

### Solution 2

```java
public class Solution { // an even smarter bit manipulation
    public int totalNQueens(int n) {
        if (n <= 0) {return 0;}
        long limit = (1L << n) - 1;
        return dfs(0L, 0L, 0L, limit);
    }
    private int dfs(long col, long dig1, long dig2, long limit) {
        if (col == limit) {
            return 1;
        }
        int cnt = 0;
        long available = limit & ~(col | dig1 | dig2);
        while (available > 0) {
            long pos = available & (~available + 1);
            available -= pos;
            cnt += dfs(col | pos, (dig1 | pos) << 1, (dig2 | pos) >> 1, limit);
        }
        return cnt;
    }
}

```

