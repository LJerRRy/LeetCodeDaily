## 59. Spiral Matrix II
Given an integer n, generate a square matrix filled with elements from 1 to n2 in spiral order.

For example,
Given n = 3,

You should return the following matrix:
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]

### Solution1
恰好和第54题反过来。

```java
public class Solution {
    public int[][] generateMatrix(int n) {
        if (n == 0) return new int[][]{};
        int[][] direction = new int[][]{{0,1},{1,0},{0,-1},{-1,0}};
        int d = 0, cnt = 1;
        int i = 0, j = 0;
        int[][] res = new int[n][n];
        res[0][0] = 1;
        while(cnt< n * n){
            i += direction[d][0];
            j += direction[d][1];
            if (i<0||i>= n ||j<0||j>= n ||res[i][j]>0){
                i -= direction[d][0];
                j -= direction[d][1];
                d = (d+1)%4;
            }else {
                res[i][j] = ++cnt;
            }
        }
        return res;
    }
}
```

### Solution2

```java
public class Solution {
    
    public int[][] generateMatrix(int n) {
        // Declaration
        int[][] matrix = new int[n][n];
        
        // Edge Case
        if (n == 0) return matrix;
        
        // Normal Case
        int rowStart = 0;
        int rowEnd = n - 1;
        int colStart = 0;
        int colEnd = n - 1;
        int number = 1;
        
        while (rowStart <= rowEnd && colStart <= colEnd) {
            for (int i = colStart; i <= colEnd; i++) {
                matrix[rowStart][i] = number++;
            }
            rowStart ++;
            
            for (int i = rowStart; i <= rowEnd; i++) {
                matrix[i][colEnd] = number++;
            }
            colEnd --;
            
            for (int i = colEnd; i >= colStart; i--) {
                if (rowStart <= rowEnd) matrix[rowEnd][i] = number++;
            }
            rowEnd --;
            
            for (int i = rowEnd; i >= rowStart; i --) {
                if (colStart <= colEnd) matrix[i][colStart] = number++;
            }
            colStart ++;
        }
        
        return matrix;
    }
}
```
