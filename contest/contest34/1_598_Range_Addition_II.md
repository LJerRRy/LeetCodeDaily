## 598. Range Addition II
Given an m * n matrix M initialized with all 0's and several update operations.

Operations are represented by a 2D array, and each operation is represented by an array with two positive integers a and b, which means M[i][j] should be added by one for all 0 <= i < a and 0 <= j < b.

You need to count and return the number of maximum integers in the matrix after performing all the operations.

## Summary
题意要求求出矩阵中最大的数的个数。
## Solution

### Approach#1
只需要求出每次操作的最小的长和宽，最后返回`长*宽`.
- 时间复杂度：O(n)
- 空间复杂度：O(1)

```java
public class Solution {
    public int maxCount(int m, int n, int[][] ops) {
        //判断对举证的操作是否为空，为空的话，那么在矩阵中最大值就是默认的零，所有最大的个数为矩阵中的数的个数
        if(ops==null||ops.length==0||ops[0].length==0)return m*n;
        int[][] res  = new int[1][2];
        res[0][0] = ops[0][0];
        res[0][1] = ops[0][1];
        for (int i = 1; i < ops.length; i++) {
            if(res[0][0]>ops[i][0]){
                res[0][0] = ops[i][0];
            }
            if(res[0][1]>ops[i][1]){
                res[0][1] = ops[i][1];
            }
        }
        return res[0][1]*res[0][0];
    }
}
```
### Approach#2
更简洁的代码。Copy from the Board。

```java
public class Solution {
    public int maxCount(int m, int n, int[][] ops) {
        int m0 = m;
        int n0 = n;
        for (int[] op : ops) {
            m0 = Math.min(m0, op[0]);
            n0 = Math.min(n0, op[1]);
        }
        return m0 * n0;
    }
}
```