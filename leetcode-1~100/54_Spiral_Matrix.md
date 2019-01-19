## 54. Spiral Matrix
Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

For example,
Given the following matrix:

[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
You should return [1,2,3,6,9,8,7,4,5].

### Solution1(DFS)

```java
public class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        if(matrix==null||matrix.length==0||matrix[0].length==0)
            return new LinkedList<>();
        List<Integer> list = new ArrayList<>();
        int[][] direction = new int[][]{{0,1},{1,0},{0,-1},{-1,0}};
        int ro = matrix.length, col = matrix[0].length, n = 1, d = 0;
        int i = 0, j = 0;
        list.add(matrix[0][0]);
        boolean[][] flag = new boolean[ro][col];
        flag[0][0] = true;
        while(n<ro*col){
            i += direction[d][0];
            j += direction[d][1];
            //边界，上下左右，以及是否被访问过
            if (i<0||i>=ro||j<0||j>=col||flag[i][j]){
                i -= direction[d][0];
                j -= direction[d][1];
                d = (d+1)%4;
            }else {
                list.add(matrix[i][j]);
                flag[i][j] = true;
                n++;
            }
        }
        return list;
    }

}
```

### Solution2

```java
public class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        
        List<Integer> res = new ArrayList<Integer>();
        
        if (matrix.length == 0) {
            return res;
        }
        
        int rowBegin = 0;
        int rowEnd = matrix.length-1;
        int colBegin = 0;
        int colEnd = matrix[0].length - 1;
        
        while (rowBegin <= rowEnd && colBegin <= colEnd) {
            // Traverse Right(向右边办理)
            for (int j = colBegin; j <= colEnd; j ++) {
                res.add(matrix[rowBegin][j]);
            }
            rowBegin++;
            
            // Traverse Down
            for (int j = rowBegin; j <= rowEnd; j ++) {
                res.add(matrix[j][colEnd]);
            }
            colEnd--;
            
            if (rowBegin <= rowEnd) {
                // Traverse Left
                for (int j = colEnd; j >= colBegin; j --) {
                    res.add(matrix[rowEnd][j]);
                }
            }
            rowEnd--;
            
            if (colBegin <= colEnd) {
                // Traver Up
                for (int j = rowEnd; j >= rowBegin; j --) {
                    res.add(matrix[j][colBegin]);
                }
            }
            colBegin ++;
        }
        
        return res;
    }
}
```
