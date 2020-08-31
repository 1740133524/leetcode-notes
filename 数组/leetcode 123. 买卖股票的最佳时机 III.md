# 123. 买卖股票的最佳时机 III

## 题目

给定一个数组，它的第 i 个元素是一支给定的股票在第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你最多可以完成 两笔 交易。

注意: 你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

## 示例

示例 1:

	输入: [3,3,5,0,0,3,1,4]
	输出: 6
	解释: 在第 4 天（股票价格 = 0）的时候买入，在第 6 天（股票价格 = 3）的时候卖出，这笔交易所能获得利润 = 3-0 = 3 。
	     随后，在第 7 天（股票价格 = 1）的时候买入，在第 8 天 （股票价格 = 4）的时候卖出，这笔交易所能获得利润 = 4-1 = 3 。

示例 2:

	输入: [1,2,3,4,5]
	输出: 4
	解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。   
	     注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。   
	     因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。

示例 3:

	输入: [7,6,4,3,1] 
	输出: 0 
	解释: 在这个情况下, 没有交易完成, 所以最大利润为 0。

## 分析

### 第一种

正面反面各遍历一次找出各自交易最高的收益

再遍历得到的正反最高收益获得整体最佳收益

### 第二种

动态规划

dp[i][j][k]，各种状态下的利润

* i表示第i天进行的交易
* j表示还有j次交易
* k有两种状态
	* k == 0，手中没有股票
	* k == 1，手中有股票

状态转移：

	dp[i][j][0] = max(dp[i-1][j][0], dp[i-1][j][1] + prices[i]);
	解释：今天手中没有股票，有两种可能：
		昨天我没有持有，今天没有购买
		昨天我持有，今天卖掉了

	dp[i][j][1] = max(dp[i-1][j][1], dp[i-1][j-1][0] - prices[i])
	解释：今天手中有股票，有两种可能：
		昨天我有持有，今天没有出售
		昨天我没有持有，今天购买了股票

因为每次只和昨天有关系，所以可以只存储相邻的状态即可

> 别人写的解释：一个通用方法团灭 6 道股票问题：https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iii/solution/yi-ge-tong-yong-fang-fa-tuan-mie-6-dao-gu-piao-wen/

## 代码

### 第一种

	class Solution {
	public:
	    int maxProfit(vector<int>& prices) {
	        vector<int> v1(prices.size());
	        vector<int> v2(prices.size());
	        int ret = 0;
	        for(int i = 0, m = INT_MAX; i < v1.size(); i++){
	            if(prices[i] < m) m = prices[i];
	            v1[i] = max(i > 0 ? v1[i-1] : 0, prices[i] - m);
	        }
	        for(int i = v1.size()-1, m = 0; i >= 0; i--){
	            if(prices[i] > m) m = prices[i];
	            v2[i] = max(i < v2.size()-1 ? v2[i+1] : 0, m - prices[i]);
	        }
	        for(int i = 0; i < prices.size(); i++){
	            ret = max(ret, v1[i] + v2[i]);
	        }
	        return ret;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iii/](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iii/)