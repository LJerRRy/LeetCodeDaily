## 48. Rotate Image
You are given an n x n 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

Follow up:
Could you do this in-place?

## Solution
[[1,2,3],
[4,5,6],
[7,8,9]]
转换为
[[7,4,1],
[8,5,2],
[9,6,3]]

### Solution 1
使用O(n^2)辅助空间来实现

```java
public class Solution {
    public void rotate(int[][] matrix) {
        if(matrix ==null||matrix.length==0||matrix[0].length==0)return;
        int n = matrix.length;
        int[][] tmp = new int[n][n];
        for (int i = 0; i < n; i++) {
            tmp[i]  = Arrays.copyOf(matrix[i], n);
        }
        for(int i = 0, k = n-1;i<n;i++,k--){
            for(int j = 0, l = 0;j<n;j++,l++){
                matrix[l][k] = tmp[i][j];
            }
        }
    }
}
```

### Solution 2(In-place)
1->3->9->7->1这样一个旋转过程

```java
public class Solution {
public void rotate(int[][] matrix) {
    int n=matrix.length;
    for (int i=0; i<n/2; i++) 
        for (int j=i; j<n-i-1; j++) {
            int tmp=matrix[i][j];
            matrix[i][j]=matrix[n-j-1][i];
            matrix[n-j-1][i]=matrix[n-i-1][n-j-1];
            matrix[n-i-1][n-j-1]=matrix[j][n-i-1];
            matrix[j][n-i-1]=tmp;
        }
    }
}
```

### Solution 3
The idea was firstly transpose the matrix and then flip it symmetrically. For instance,

```
1  2  3             
4  5  6
7  8  9
```
after transpose, it will be swap(matrix[i][j], matrix[j][i])

```
1  4  7
2  5  8
3  6  9
```
Then flip the matrix horizontally. (swap(matrix[i][j], matrix[i][matrix.length-1-j])

```
7  4  1
8  5  2
9  6  3
```

```java
public class Solution {
    public void rotate(int[][] matrix) {
        for(int i = 0; i<matrix.length; i++){
            for(int j = i; j<matrix[0].length; j++){
                int temp = 0;
                temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }
        for(int i =0 ; i<matrix.length; i++){
            for(int j = 0; j<matrix.length/2; j++){
                int temp = 0;
                temp = matrix[i][j];
                matrix[i][j] = matrix[i][matrix.length-1-j];
                matrix[i][matrix.length-1-j] = temp;
            }
        }
    }
}
```