# 55. 跳跃游戏

## 题目

给定一个非负整数数组，你最初位于数组的第一个位置。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

判断你是否能够到达最后一个位置。

## 示例

示例 1:

	输入: [2,3,1,1,4]
	输出: true
	解释: 我们可以先跳 1 步，从位置 0 到达 位置 1, 然后再从位置 1 跳 3 步到达最后一个位置。

示例 2:

	输入: [3,2,1,0,4]
	输出: false
	解释: 无论怎样，你总会到达索引为 3 的位置。但该位置的最大跳跃长度是 0 ， 所以你永远不可能到达最后一个位置。

## 分析

贪心算法，每次都寻找下次能跳最远的格子

## 代码

	class Solution {
	public:
	    bool canJump(vector<int>& nums) {
	        for(int i = 0; i < nums.size();){
	            if(i + nums[i] >= nums.size()-1) return true;
	            int z = 0;
	            int z1 = 0;
	            for(int j = 0; j <= nums[i]; j++){
	                if(nums[i+j] + i + j > z){
	                    z = nums[i+j] + i + j;
	                    z1 = i+j;
	                }
	            }
	            if(i == z1) return false;
	            i = z1;
	        }
	        return true;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/jump-game/](https://leetcode-cn.com/problems/jump-game/)