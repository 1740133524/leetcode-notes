# 31. 下一个排列

## 题目

实现获取下一个排列的函数，算法需要将给定数字序列重新排列成字典序中下一个更大的排列。

如果不存在下一个更大的排列，则将数字重新排列成最小的排列（即升序排列）。

必须原地修改，只允许使用额外常数空间。

以下是一些例子，输入位于左侧列，其相应输出位于右侧列。
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1

## 分析

可以从后往前找，找到第一个不是递增的数，从后面遍历过的数中找到刚好比此数大的数交换，再将后面的数变为升序即可

## 代码

	class Solution {
	public:
	    void nextPermutation(vector<int>& nums) {
	        for(int i = nums.size()-2; i >= 0; i--){
	            if(nums[i] < nums[i+1]){
	                for(int j = nums.size()-1; j > i; j--){
	                    if(nums[i] < nums[j]){
	                        int z = nums[i];
	                        nums[i] = nums[j];
	                        nums[j] = z;
	                        sort(nums.begin()+i+1, nums.end());
	                        return;
	                    }
	                }
	            }
	        }
	        sort(nums.begin(), nums.end());
	        return;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/next-permutation/](https://leetcode-cn.com/problems/next-permutation/)