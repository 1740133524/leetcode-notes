# 81. 搜索旋转排序数组 II

## 题目

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 [0,0,1,2,2,5,6] 可能变为 [2,5,6,0,0,1,2] )。

编写一个函数来判断给定的目标值是否存在于数组中。若存在返回 true，否则返回 false。

## 示例
	
示例 1:

	输入: nums = [2,5,6,0,0,1,2], target = 0
	输出: true

示例 2:
	
	输入: nums = [2,5,6,0,0,1,2], target = 3
	输出: false

## 进阶:

* 这是 搜索旋转排序数组 的延伸题目，本题中的 nums  可能包含重复元素。
* 这会影响到程序的时间复杂度吗？会有怎样的影响，为什么？

## 分析

和之前 33. 搜索旋转排序数组 差不多，区别在于nums[l] == nums[m] 的时候无法判断这之间是否有数，只能l++，一个个排除

## 代码

	class Solution {
	public:
	    bool search(vector<int>& nums, int target) {
	        int l = 0;
	        int r = nums.size()-1;
	        while(l <= r){
	            int m = (l+r)/2;
	            if(target == nums[m]) return true;
	            if(nums[l] < nums[m]){
	                if(target < nums[m] && target >= nums[l]) r = m-1;
	                else l = m;
	            }
	            else if(nums[l] == nums[m]){
	                l++;
	            }
	            else{
	                if(target > nums[m] && target <= nums[r]) l = m+1;
	                else r = m;
	            }
	        }
	        return false;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/search-in-rotated-sorted-array-ii/](https://leetcode-cn.com/problems/search-in-rotated-sorted-array-ii/)