# 154. 寻找旋转排序数组中的最小值 II

## 题目

	假设按照升序排序的数组在预先未知的某个点上进行了旋转。
	
	( 例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2] )。
	
	请找出其中最小的元素。
	
	注意数组中可能存在重复的元素。

## 示例

示例 1：

	输入: [1,3,5]
	输出: 1

示例 2：

	输入: [2,2,2,0,1]
	输出: 0

## 分析

使用二分法

l表示数组的最左端，m表示中间，r表示数组最右端

* 当 l > m 时，表示最小数位于 (l, m]
* 当 m > r 时，表示最小数位于 (m, r]
* 当 l < r 时，最最小数就是l（这种可加可不加，因为在不少时候判断这个反而会加长时间）
* 还有种情况，就是遇到 l = m = r 的时候，这时只能 r--，一点点缩小范围 

## 代码
	
	class Solution {
	public:
	    int findMin(vector<int>& nums) {
	        int l = 0;
	        int r = nums.size()-1;
	        while(l < r){
	            int m = (l+r)/2;
				if(nums[l] < nums[r]) return nums[l]; // 可加可不加
	            if(nums[l] > nums[m]) r = m;
	            else if(nums[m] > nums[r]) l = m+1;
	            else r--;
	        }
	        return nums[l];
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/)