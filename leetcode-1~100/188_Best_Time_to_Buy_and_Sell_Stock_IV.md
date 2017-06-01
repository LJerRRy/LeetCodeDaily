##  123. Best Time to Buy and Sell Stock III
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most k transactions.

**至多k次交易**

### Solution 1 （Memory Limit Exceeded）
超时或者内存超出的原因在于当k>=prices.length/2的时候，那么就相对于可以任意交易次数，直接求出最大利润即可。见方法二
```java
public class Solution {
    public int maxProfit(int k, int[] prices) {
        if(prices==null||prices.length<=1)return 0;
        else {
            int[][] dp = new int[k+1][prices.length];
            int res = 0;
            for (int i = 1; i <= k; i++) {
                int tmpMax = - prices[0];
                for (int j = 1; j < prices.length; j++) {
                    dp[i][j] = Math.max(dp[i][j-1], prices[j] + tmpMax);
                    //i-1次交易的可能为最大值
                    tmpMax = Math.max(tmpMax, dp[i-1][j] - prices[j]);
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
    public int maxProfit(int k, int[] prices) {
        if(prices==null||prices.length<=1)return 0;
        int len = prices.length;
        if (k >= len / 2) return quickSolve(prices);
        int[][] t = new int[k + 1][len];
        for (int i = 1; i <= k; i++) {
            int tmpMax =  -prices[0];
            for (int j = 1; j < len; j++) {
                t[i][j] = Math.max(t[i][j - 1], prices[j] + tmpMax);
                tmpMax =  Math.max(tmpMax, t[i - 1][j - 1] - prices[j]);
            }
        }
        return t[k][len - 1];
    }
    private int quickSolve(int[] prices) {
        int len = prices.length, profit = 0;
        for (int i = 1; i < len; i++)
            // as long as there is a price gap, we gain a profit.
            if (prices[i] > prices[i - 1]) profit += prices[i] - prices[i - 1];
        return profit;
    }
}
```