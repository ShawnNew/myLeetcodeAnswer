## Best Time to Buy and Sell Stock(DP)
Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

<pre><code>
class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null) {
            return 0;
        }
        if (prices.length == 1) {
            return 0;
        }
        
        int profitToday = 0, profitTotal = 0;
        for (int i = 1; i < prices.length; i++) {
            profitToday = Math.max(profitToday + prices[i] - prices[i - 1], 0);
            profitTotal = Math.max(profitToday, profitTotal);
        }
        return profitTotal;
    }
}
</code></pre>

* 动态规划问题
* 维护两个变量，profitToday和profitTotal。一个表示当天卖出的最大利润，另一个表示到目前为止的最大利润。
* 基本思想：将问题转换为总利润为前一天买入当天卖出获取的利润与前一天卖出（必须包括前一天，但是不限制买入时间。）获取的利润比较得到的最大利润。