# 689. 三个无重叠子数组的最大和

## 题目

给定数组 nums 由正整数组成，找到三个互不重叠的子数组的最大和。

每个子数组的长度为k，我们要使这3*k个项的和最大化。

返回每个区间起始索引的列表（索引从 0 开始）。如果有多个结果，返回字典序最小的一个。

## 示例

	输入: [1,2,1,2,6,7,5,1], 2
	输出: [0, 3, 5]
	解释: 子数组 [1, 2], [2, 6], [7, 5] 对应的起始索引为 [0, 3, 5]。
	我们也可以取 [2, 1], 但是结果 [1, 3, 5] 在字典序上更大。

### 注意

* nums.length的范围在[1, 20000]之间。
* nums[i]的范围在[1, 65535]之间。
* k的范围在[1, floor(nums.length / 3)]之间。

## 分析

使用动态规划

dp[i][j], 表示到第i个数为止j个子数组的和

dp1[i][j][k]，表示到第i个数为止j个子数组的第k个起始索引

v[i]，表示到第i个数的前缀和

dp[i][j] = max(dp[i-1][j], dp[i-k][1] + v[i] - v[i-k]) 

## 代码
	
	class Solution {
	public:
	    vector<int> maxSumOfThreeSubarrays(vector<int>& nums, int k) {
	        vector<vector<int>> dp(nums.size(), vector<int>(4, 0));
	        vector<vector<vector<int>>> dp1(nums.size(), vector<vector<int>>(4, vector<int>(3, 0)));
	        vector<int> v(nums.size(), 0);
	        v[0] = nums[0];
	        for(int i = 1; i < nums.size(); i++){
	            v[i] = v[i-1] + nums[i];
	        }
	        
	        for(int i = 0; i < nums.size(); i++){
	            if(i-k == -1){
	                dp[i][1] = v[i];
	                dp1[i][1][0] = i-k+1;
	            }
	            else if(i-k >= 0){
	                if(dp[i-1][1] >= v[i] - v[i-k]){
	                    dp[i][1] = dp[i-1][1];
	                    dp1[i][1][0] = dp1[i-1][1][0];
	                }
	                else{
	                    dp[i][1] = v[i] - v[i-k];
	                    dp1[i][1][0] = i-k+1;
	                } 
	            }
	            // 这一部分可以使用循环代替
	            if(i >= k * 2-1 && dp[i-1][2] >= dp[i-k][1] + v[i] - v[i-k]){
	                dp[i][2] = dp[i-1][2];
	                dp1[i][2][0] = dp1[i-1][2][0];
	                dp1[i][2][1] = dp1[i-1][2][1];
	            } 
	            else if(i >= k * 2-1){
	                dp[i][2] = dp[i-k][1] + v[i] - v[i-k];
	                dp1[i][2][0] = dp1[i-k][1][0];
	                dp1[i][2][1] = i-k+1;
	            } 
	            if(i >= k * 3-1 && dp[i-1][3] >= dp[i-k][2] + v[i] - v[i-k]){
	                dp[i][3] = dp[i-1][3];
	                dp1[i][3][0] = dp1[i-1][3][0];
	                dp1[i][3][1] = dp1[i-1][3][1];
	                dp1[i][3][2] = dp1[i-1][3][2];
	            }
	            else if(i >= k * 3-1){
	                dp[i][3] = dp[i-k][2] + v[i] - v[i-k];
	                dp1[i][3][0] = dp1[i-k][2][0];
	                dp1[i][3][1] = dp1[i-k][2][1];
	                dp1[i][3][2] = i-k+1;
	            }
	        }
	        return dp1[nums.size()-1][3];
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/maximum-sum-of-3-non-overlapping-subarrays/](https://leetcode-cn.com/problems/maximum-sum-of-3-non-overlapping-subarrays/)