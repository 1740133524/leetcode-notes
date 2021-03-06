# 34. 在排序数组中查找元素的第一个和最后一个位置

## 题目

给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置。

你的算法时间复杂度必须是 O(log n) 级别。

如果数组中不存在目标值，返回 [-1, -1]。

## 示例

示例 1:

	输入: nums = [5,7,7,8,8,10], target = 8
	输出: [3,4]

示例 2:

	输入: nums = [5,7,7,8,8,10], target = 6
	输出: [-1,-1]

## 分析

两次二分找边界即可

## 代码

	class Solution {
	public:
	    vector<int> searchRange(vector<int>& nums, int target) {
	        int l = 0;
	        int r = nums.size()-1;
	        vector<int> ret(2, -1);
	        if(nums.size() == 0) return ret;
	        while(l < r){  // 找左边界
	            int m = (l+r)/2;
	            if(nums[m] < target) l = m+1;   
	            else r = m;
	        }
	        if(nums[l] != target) return ret;
	        ret[0] = l;
	        l = 0;
	        r = nums.size()-1;
	        while(l < r){  // 找右边界
	            int m = (l+r+1)/2; // 这里是为了在只剩两个的时候，m为右边那个，不然有可能无限循环
	            if(nums[m] > target) r = m-1;
	            else l = m;
	        }
	        ret[1] = l;
	        return ret;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)