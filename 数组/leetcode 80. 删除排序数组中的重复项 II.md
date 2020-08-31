# 80. 删除排序数组中的重复项 II

## 题目

给定一个排序数组，你需要在原地删除重复出现的元素，使得每个元素最多出现两次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。

## 示例
	
示例 1:

	给定 nums = [1,1,1,2,2,3],
	
	函数应返回新长度 length = 5, 并且原数组的前五个元素被修改为 1, 1, 2, 2, 3 。
	
	你不需要考虑数组中超出新长度后面的元素。

示例 2:

	给定 nums = [0,0,1,1,1,1,2,3,3],
	
	函数应返回新长度 length = 7, 并且原数组的前五个元素被修改为 0, 0, 1, 1, 2, 3, 3 。
	
	你不需要考虑数组中超出新长度后面的元素。

## 分析

使用双指针，快指针遍历数组，慢指针指向可以复写数据的区域，使用一个变量记录同字母出现次数即可

## 代码

	class Solution {
	public:
	    int removeDuplicates(vector<int>& nums) {
	        if(nums.size() == 0) return 0;
	        int l = 1;
	        int r = 1;
	        int z = 1;
	        int ret = 1;
	        while(r < nums.size()){
	            if(nums[r] == nums[r-1]) z++;
	            else z = 1;
	            if(z <= 2){
	                nums[l] = nums[r];
	                l++;
	                ret++;
	            }
	            r++;
	        }
	        return ret;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array-ii/](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array-ii/)