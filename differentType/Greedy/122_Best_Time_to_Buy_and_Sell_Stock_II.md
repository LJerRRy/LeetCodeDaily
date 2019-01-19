##  122. Best Time to Buy and Sell Stock II
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).


### Solution 1
**任意次数，但只能卖掉之后买进**，注意到其实交易次数k只要大于princes.length的话就是任意次数了（就是每次买进后第二天卖出，然后马上买进），这样理解有助于解决[188题](./leetcode-1~100/188_Best_Time_to_Buy_and_Sell_Stock_IV)。

```java
public class Solution {
    public int maxProfit(int[] prices) {
       int len = prices.length, profit = 0;
        for (int i = 1; i < len; i++)
            if (prices[i] > prices[i - 1]) profit += prices[i] - prices[i - 1];
        return profit; 
    }
}
```