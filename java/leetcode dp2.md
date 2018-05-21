[Most-consistent-ways-of-dealing-with-the-series-of-stock-problems](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/discuss/108870/Most-consistent-ways-of-dealing-with-the-series-of-stock-problems)<br>
感觉，表示收益的T数组在初始化时候，如果手中没有股票就都是初始化为0，有股票就初始化为负无穷。

看完之后，受益匪浅！曾经看不懂的transaction with cool down，在作者的通用框架下只需小小的改动！非常佩服作者这样找到若干特殊问题背后的一般规律的人。仿佛统一了经典力学和量子力学。（好吧我是物理渣）

[121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/discuss/39038/kadanes-algorithm-since-no-one-has-mentioned-about-this-so-far-in-case-if-interviewer-twists-the-input)<br>
一个121的变体：如果给出的数组不是每天的价格，而是当天价格减去前一天价格的差，那么要怎么求解？<br>
虽然没听过kadane算法。。但这篇的思路还是挺不错的。确实类似最大子数组问题。依次累加当天价格和前一天价格的差。如果小于零了就置零。同时维护最大累加和。
```
public int maxProfit(int[] prices) {
    int maxCur = 0, maxSoFar = 0;
    for(int i = 1; i < prices.length; i++) {
        maxCur = Math.max(0, maxCur += prices[i] - prices[i-1]);
        maxSoFar = Math.max(maxCur, maxSoFar);
    }
    return maxSoFar;
}
```
[213. House Robber II](https://leetcode.com/problems/house-robber-ii)<br>
版本一是房子成一条线，版本二是房子围成圆圈。其他要求不变，不能抢劫相邻房子。

其实，假设房子总数为n，那么就分别对1~(n-1)和2~n的房子看做直线排列看待。

[322. Coin Change](https://leetcode.com/problems/coin-change/description/)<br>
给定一序列硬币面值和一个目标值，求组成目标值需要的最少硬币个数。硬币可以拿无限个。<br>
典型动规。。动规的方程不难想到。但边界条件的处理比较关键。
```
public int coinChange(int[] coins, int amount) {
    if(amount == 0) return 0;
    int [] dp = new int[amount+1];
    for(int i=1; i<=amount; ++i) dp[i]=Integer.MAX_VALUE-1;
    dp[0]=0;
    for(int i=0;i<=amount;++i){
        for(int j=0;j<coins.length;++j){
            if(i>=coins[j]) dp[i] = Math.min(dp[i], dp[i-coins[j]] + 1); 
        }
    }
    if(dp[amount]==Integer.MAX_VALUE-1) return -1;
    else return dp[amount];
}
```
答案中，是把dp数组全部初始化为amount+1，以及dp[0]=0。