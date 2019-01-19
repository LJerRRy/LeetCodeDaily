## 120. Triangle
Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

For example, given the following triangle

```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```
最小的是2+3+5+1 = 11

### Solution 1
对于三角形中某个数下标为(i,j)，只能是该数的头顶两个(i-1,j-1)、(i-1,j)这两个数之一，可能只存在一个结点。dp过程为从第一层开始，一层一层向后迭代，选择最小的。

```java
public class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        if(triangle==null||triangle.size()==0)return 0;
        int m = triangle.size(), n = triangle.get(m-1).size();
        int[][] dp = new int[m][n];
        //k用来控制每层的个数，因为每一层数的个数是递增的
        int k = 2;
        dp[0][0] = triangle.get(0).get(0);
        for (int i = 1; i < m; i++) {
            for (int j = 0; j < k; j++) {
                int min = Integer.MAX_VALUE;
                //(i-1, j-1)
                min = j-1>=0?Math.min(min,dp[i-1][j-1]):min;
                //(i-1, j)
                min = j+1<k?Math.min(min,dp[i-1][j]):min;
                dp[i][j] = triangle.get(i).get(j) + min;
            }
            k++;
        }
        Arrays.sort(dp[m-1]);
        return dp[m-1][0];
    }
}
```
### Solution 2
discuss上有个简单的方法，就是从最后一层往上迭代，dp中保存的是前一层的最小值的列表，到最后dp中只有一个结点，因为第一层只有一个结点。

```java
public class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int[] dp = new int[triangle.get(triangle.size() - 1).size()];
        for (int i = 0; i < dp.length; ++i) {
             dp[i] = triangle.get(triangle.size() - 1).get(i);
        }
        for (int i = triangle.size() - 2; i >= 0; --i) {
            List<Integer> row = triangle.get(i);
            for (int j = 0; j < row.size(); ++j) {
                dp[j] = Math.min(dp[j], dp[j + 1]) + row.get(j);
            }
        }
        return dp[0];
    }
}
```