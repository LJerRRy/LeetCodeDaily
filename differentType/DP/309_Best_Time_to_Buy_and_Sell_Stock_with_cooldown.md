## 309. Best Time to Buy and Sell Stock with Cooldown
Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times) with the following restrictions:

- You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
- After you sell your stock, you cannot buy stock on next day. (ie, cooldown 1 day)

**给你任意次交易次数，但是不能买进后立即买进，要休息一天后才能买进**

### Solution 1

```java
public class Solution {
    public int maxProfit(int[] prices) {
        if (prices==null||prices.length<=1)return 0;
        int k = (prices.length+1)/3;
        int[][] dp = new int[k+1][prices.length];
        for (int i = 1; i < k + 1; i++) {
            int tmpMax = - prices[0];
            for (int j = 1; j < prices.length; j++) {
                // 要么第j次cooldownday，或者就卖出
                dp[i][j] = Math.max(dp[i][j-1], tmpMax+prices[j]);
                //第j次卖出，如果前面j>1，不能用dp[i-1][j-1]，因为这样就违反规定
                if(j>1)
                    tmpMax = Math.max(tmpMax, dp[i-1][j-2]-prices[j]);
                else
                    tmpMax = Math.max(tmpMax,dp[i-1][j-1] - prices[j]);
            }
        }
        return dp[k][prices.length-1];
    }
}
```
### Solution 2

```java
public class Solution {
    public int maxProfit(int[] prices) {
        if(prices == null || prices.length < 2){
            return 0;
        }
        int len = prices.length;
        int[] sell = new int[len]; //sell[i] means must sell at day i
        int[] cooldown = new int[len]; //cooldown[i] means day i is cooldown day
        sell[1] = prices[1] - prices[0];
        for(int i = 2; i < prices.length; ++i){
            cooldown[i] = Math.max(sell[i - 1], cooldown[i - 1]);
            sell[i] = prices[i] - prices[i - 1] + Math.max(sell[i - 1], cooldown[i - 2]);
        }
        return Math.max(sell[len - 1], cooldown[len - 1]);
    }
}
```
### Solution 3
[具体解释见discuss](https://discuss.leetcode.com/topic/30421/share-my-thinking-process)

```java
public int maxProfit(int[] prices) {
    int sell = 0, prev_sell = 0, buy = Integer.MIN_VALUE, prev_buy;
    for (int price : prices) {
        prev_buy = buy;
        buy = Math.max(prev_sell - price, prev_buy);
        prev_sell = sell;
        sell = Math.max(prev_buy + price, prev_sell);
    }
    return sell;
}
```