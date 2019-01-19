## 51. N-Queens
The n-queens puzzle is the problem of placing n queens on an n×n chessboard such that no two queens attack each other.

Given an integer n, return all distinct solutions to the n-queens puzzle.

Each solution contains a distinct board configuration of the n-queens' placement, where 'Q' and '.' both indicate a queen and an empty space respectively.

For example,
There exist two distinct solutions to the 4-queens puzzle:

[
 [".Q..",  // Solution 1
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",  // Solution 2
  "Q...",
  "...Q",
  ".Q.."]
]

## Solution

### Solution 1

```java
public List<List<String>> solveNQueens(int n) {
        char[][] c = new char[n][n];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                c[i][j] = '.';
            }
        }
        List<List<String>> res = new LinkedList<>();
        backtrack(res, c, 0);
        return res;
    }

    private void backtrack(List<List<String>> list, char[][] c, int ro){
        if (ro==c.length){
            list.add(makeString(c));
            return;
        }
        for (int i = 0; i < c.length; i++) {
            // 判断当前位置(ro, i) 能否为Queen
            if (valid(c, i, ro)){
                c[ro][i] = 'Q';
                backtrack(list, c, ro+1);
                c[ro][i] = '.';
            }
        }
    }

    private boolean valid(char[][] c, int co, int ro) {
        for (int i = 0; i < ro; i++) {
            for (int j = 0; j < c.length; j++) {
                // 如果之前某一个皇后能攻击到当前位置的皇后，则不合法
                if (c[i][j] == 'Q'&&isInLine(i, j, ro, co)){
                    return false;
                }
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
    
    // 将符合的队列list化
    private List<String> makeString(char[][] c) {
        StringBuilder sb;
        List<String> res = new LinkedList<>();
        for (int i = 0; i < c.length; i++) {
            sb = new StringBuilder();
            for (int j = 0; j < c.length; j++) {
                sb.append(c[i][j]);
            }
            res.add(sb.toString());
        }
        return res;
    }
```

### Solution 2

```java
public class Solution {
    List<List<String>> res=new ArrayList();
    public List<List<String>> solveNQueens(int n) {
        if(n==0) return res;
        char[][] tmp=new char[n][n];
        boolean[] col=new boolean[n];
        boolean[] dia=new boolean[2*n-1];
        boolean[] antidia=new boolean[2*n-1];
        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                tmp[i][j]='.';
            }
        }
        dfs(tmp,n,col,dia,antidia,0);
        return res;
    }
    public void dfs(char[][] tmp,int n,boolean[] col,boolean[] dia,boolean[] antidia,int row){
        if(row==n){
            List<String> cur=new ArrayList();
            for(int i=0;i<n;i++){
                cur.add(String.valueOf(tmp[i]));
            }
            res.add(cur);
            return;
        }
        for(int j=0;j<n;j++){
            if(col[j]||dia[row+j]||antidia[row-j+n-1]) continue;
            col[j]=dia[row+j]=antidia[row-j+n-1]=true;
            tmp[row][j]='Q';
            dfs(tmp,n,col,dia,antidia,row+1);
            tmp[row][j]='.';
            col[j]=dia[row+j]=antidia[row-j+n-1]=false;
        }
    }
}
```