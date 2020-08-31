# 45. 跳跃游戏 II

## 题目

给定一个非负整数数组，你最初位于数组的第一个位置。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

你的目标是使用最少的跳跃次数到达数组的最后一个位置。

## 示例

	输入: [2,3,1,1,4]
	输出: 2
	解释: 跳到最后一个位置的最小跳跃数是 2。
	     从下标为 0 跳到下标为 1 的位置，跳 1 步，然后跳 3 步到达数组的最后一个位置。

## 分析

贪心算法，每次跳跃到下一次可以跳到的最远的位置

## 代码

	class Solution {
	public:
	    int jump(vector<int>& nums) {
	        int ret = 0;
	        for(int i = 0; i < nums.size()-1;){
	            if(i + nums[i] >= nums.size()-1) return ret+1;
	            int j1 = 0;
	            int m = 0;
	            for(int j = i+1; j < nums.size() && j <= i + nums[i]; j++){
	                if(nums[j] + j > m){
	                    m = nums[j] + j;
	                    j1 = j;
	                }
	            }
	            i = j1;
	            ret++;
	        }
	        return ret;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/jump-game-ii/](https://leetcode-cn.com/problems/jump-game-ii/)