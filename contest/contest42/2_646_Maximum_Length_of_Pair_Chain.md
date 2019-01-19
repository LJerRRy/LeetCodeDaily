## 646. Maximum Length of Pair Chain
You are given n pairs of numbers. In every pair, the first number is always smaller than the second number.

Now, we define a pair (c, d) can follow another pair (a, b) if and only if b < c. Chain of pairs can be formed in this fashion.

Given a set of pairs, find the length longest chain which can be formed. You needn't use up all the given pairs. You can select pairs in any order.

Example 1:
Input: [[1,2], [2,3], [3,4]]
Output: 2
Explanation: The longest chain is [1,2] -> [3,4]
Note:
1. The number of given pairs will be in the range [1, 1000].
## Summary

## Solution

### Approach#1
按照数组第二列进行排序。动态规划，进行求解

```java
public class Solution {
    public int findLongestChain(int[][] pairs) {
        Arrays.sort(pairs, (a,b)->(a[1]-b[1]));
        int res = 1;
        int[] dp = new int[pairs.length];
        dp[0] = 1;
        for (int i = 1; i < pairs.length; i++) {
            for (int j = 0; j < i; j++) {
                if (pairs[i][0]>pairs[j][1]){
                    dp[i] = Math.max(dp[j] + 1, dp[i]);
                }
            }
            res = Math.max(res, dp[i]);
        }
        return res;
    }

}
```
### Approach#2
利用第二列进行排序

```java
public class Solution {
    public int findLongestChain(int[][] e) {
        Arrays.sort(e, (a, b) -> a[0] - b[0]);
        int n = e.length;
        int[] dp = new int[n];
        int max = 0;
		Arrays.fill(dp, 1);
        for(int i = 0; i < n; i++){
            for(int j = 0; j < i; j++){
                if(e[i][0] > e[j][1]){
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
            max = Math.max(max, dp[i]);
        }
        return max;
    }
}
```