# 41. 缺失的第一个正数

## 题目

给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有满足条件且不重复的三元组。

注意：答案中不可以包含重复的三元组。

## 示例

	给定数组 nums = [-1, 0, 1, 2, -1, -4]，
	
	满足要求的三元组集合为：
	[
	  [-1, 0, 1],
	  [-1, -1, 2]
	]

## 分析

先排序

遍历数组：

* 三个数，其中一个为当前遍历到的数i，另外两个通过双指针的方式得到：
	* 左指针l = i+1，右指针r = nums.size()-1
	* 如果数相加大于0，r--
	* 如果数相加小于0，l++
	* 这里跳掉的数原理和 leetcode 11. 盛最多水的容器 一样，跳掉的可能同样不满足条件
* 在此过程中跳掉所有相邻重复的数，可以避免出现重复三元组

## 代码

	class Solution {
	public:
	    vector<vector<int>> threeSum(vector<int>& nums) {
	        vector<vector<int>> ret;
	        sort(nums.begin(), nums.end());
	        for(int i = 0; i < nums.size();){
	            for(int l = i+1, r = nums.size()-1; l < r;){
	                int h = nums[i] + nums[r] + nums[l];
	                if(h > 0){
	                    r--;
	                    while(l < r && nums[r] == nums[r+1]) r--;
	                }
	                else if(h < 0){
	                    l++;
	                    while(l < r && nums[l] == nums[l-1]) l++;
	                }
	                else{
	                    ret.push_back(vector<int>{nums[i], nums[l], nums[r]});
	                    l++;
	                    r--;
	                    while(l < r && nums[r] == nums[r+1]) r--;
	                    while(l < r && nums[l] == nums[l-1]) l++;
	                }
	            }
	            i++;
	            while(i < nums.size() && nums[i] == nums[i-1]) i++;
	        }
	        return ret;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/3sum/](https://leetcode-cn.com/problems/3sum/)