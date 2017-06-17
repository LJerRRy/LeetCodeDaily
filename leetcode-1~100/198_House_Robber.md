## 198. House Robber
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.
### Solution 1
用动态规划进行解答，dp[i]表示到第i个为止最大的值（第i个恰好被rob），dp[i+1] = max(dp[i-2]+A[i], dp[i-1])

```java
public class Solution {
    public int rob(int[] A) {
        if(A==null||A.length==0)return 0;
        if(A.length==1)return A[0];
        int[] dp = new int[A.length];
        dp[0] = A[0];
        dp[1] = Math.max(A[0],A[1]);
        for(int i = 2;i<A.length;i++){
            dp[i] = Math.max(dp[i-2]+A[i], dp[i-1]);
        }
        return dp[A.length-1];
    }
}
```

### Solution 2
奇数和偶数相加比较大小。

```java
public class Solution {
    public int rob(int[] num) {
        if(num==null||num.length==0)return 0;
        int a = 0;
        int b = 0;
        int n = num.length;
        for (int i=0; i<n; i++){
            if (i%2==0){
                a = Math.max(a+num[i], b);
            }
            else{
                b = Math.max(a, b+num[i]);
            }
        }
        return Math.max(a,b);
    }
}
```
