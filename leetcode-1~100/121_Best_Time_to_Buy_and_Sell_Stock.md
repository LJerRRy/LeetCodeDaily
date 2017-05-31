## 121.Best Time to Buy and Sell Stock
Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

### Solution 1
题目给定股市的每天价格，判断哪天买进哪天卖出能挣最多。先将价格转换为与之前一天的差值然后只需要求最大连续子数组。

```java
public class Solution {
    public int maxProfit(int[] prices) {
        if(prices==null||prices.length==1||prices.length==0)return 0;
        int[] a = new int[prices.length-1];
        for (int i = 0; i < a.length; i++) {
            a[i]=prices[i+1]-prices[i];
        }
        int max = 0;
        int cur = 0;
        for (int i = 0; i < a.length; i++) {
            cur = Math.max(0, cur+a[i]);
            max = Math.max(max, cur);
        }
        return max;
    }
}
```

### Solution2
该解法来自discuss，思路和我的一样，代码非常简洁。常数的空间复杂度

```java
public class Solution {
    public int maxProfit(int[] prices) {
        int maxCur = 0, maxSoFar = 0;
        for(int i = 1; i < prices.length; i++) {
            maxCur = Math.max(0, maxCur += prices[i] - prices[i-1]);
            maxSoFar = Math.max(maxCur, maxSoFar);
        }
        return maxSoFar;
    }
}
```