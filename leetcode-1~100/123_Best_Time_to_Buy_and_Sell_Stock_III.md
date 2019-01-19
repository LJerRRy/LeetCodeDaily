##  123. Best Time to Buy and Sell Stock III
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).


### Solution 1
You may complete at most two transactions.
**至多两次交易**

```java
public class Solution {
    public int maxProfit(int[] prices) {
        if(prices==null||prices.length<=1)return 0;
        else {
            int k = 2;
            int[][] dp = new int[k+1][prices.length];
            int res = 0;
            for (int i = 1; i <= k; i++) {
                int tmpMax = - prices[0];
                for (int j = 1; j < prices.length; j++) {
                    dp[i][j] = Math.max(dp[i][j-1], prices[j] + tmpMax);
                    //i-1次交易的可能为最大值,下面这两行居然是等价的，但dp[i-1][j]比较好理解，在j天卖出后买上买进，而不是在j-1天卖出，j天买进
                    //tmpMax = Math.max(tmpMax, dp[i-1][j] - prices[j]);
                    tmpMax = Math.max(tmpMax, dp[i-1][j-1] - prices[j]);
                    res = Math.max(dp[i][j], res);
                }
            }
            return res;
        }
    }
}
```

### Solution 2

```java
public class Solution {
    public int maxProfit(int[] prices) {
        int hold1 = Integer.MIN_VALUE, hold2 = Integer.MIN_VALUE;
        int release1 = 0, release2 = 0;
        for(int i:prices){                              // Assume we only have 0 money at first
            release2 = Math.max(release2, hold2+i);     // The maximum if we've just sold 2nd stock so far.
            hold2    = Math.max(hold2,    release1-i);  // The maximum if we've just buy  2nd stock so far.
            release1 = Math.max(release1, hold1+i);     // The maximum if we've just sold 1nd stock so far.
            hold1    = Math.max(hold1,    -i);          // The maximum if we've just buy  1st stock so far. 
        }
        return release2; ///Since release1 is initiated as 0, so release2 will always higher than release1.
    }
}
```