# 41. 缺失的第一个正数

## 题目

给你一个未排序的整数数组，请你找出其中没有出现的最小的正整数。

## 示例

示例 1:
	
	输入: [1,2,0]
	输出: 3

示例 2:
	
	输入: [3,4,-1,1]
	输出: 2

示例 3:

	输入: [7,8,9,11,12]
	输出: 1

## 分析

可以将每个数放到对应的位置上，比如说整数5，就将5和位置5上的数互换。直到将所有的数放到正确的位置，遍历一遍，但凡遇到数字和位置不匹配的，就说明缺少的最小正整数就是当前位置的序号。

## 代码

	class Solution {
	public:
	    int firstMissingPositive(vector<int>& nums) {
	        int l = 0;
	        if(nums.size() == 0) return 1;
	        for(int i = 0; i < nums.size(); i++){
	            if(nums[i] <= nums.size() && nums[i] > 0){
	                if(nums[nums[i]-1] != nums[i]){
	                    int z = nums[nums[i]-1];
	                    nums[nums[i]-1] = nums[i];
	                    nums[i] = z;
	                    i--;
	                }
	            }
	        }
	        for(int i = 0; i < nums.size(); i++){
	            if(nums[i] != i+1) return i+1;
	        }
	        return nums.size()+1;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/first-missing-positive/](https://leetcode-cn.com/problems/first-missing-positive/)