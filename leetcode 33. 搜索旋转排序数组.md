# 33. 搜索旋转排序数组

## 题目

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2] )。

搜索一个给定的目标值，如果数组中存在这个目标值，则返回它的索引，否则返回 -1 。

你可以假设数组中不存在重复的元素。

你的算法时间复杂度必须是 O(log n) 级别。

## 示例

示例 1:

	输入: nums = [4,5,6,7,0,1,2], target = 0
	输出: 4

示例 2:

	输入: nums = [4,5,6,7,0,1,2], target = 3
	输出: -1

## 分析

通过二分可以将数组分成一个有序和一个无序，每次都判断target是否在有序的数组中：若在，继续二分有序数组；若不在，继续二分无序数组。直到找到或确认target不在数组中。

## 代码

	class Solution {
	public:
	    int search(vector<int>& nums, int target) {
	        int l = 0;
	        int r = nums.size()-1;
	        if(nums.size() == 0) return -1;
	        if(nums[l] == target) return l;
	        if(nums[r] == target) return r;
	        while(l+1 < r){
	            int m = (l+r)/2;
	            if(nums[l] < nums[m]){ // 左有序
	                if(target >= nums[l] && target <= nums[m]) r = m;
	                else l = m;
	            }
	            else{
	                if(target >= nums[m] && target <= nums[r]) l = m;
	                else r = m;
	            }
	            if(nums[l] == target) return l;
	            if(nums[r] == target) return r;
	        }
	        return -1;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/search-in-rotated-sorted-array/](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/)