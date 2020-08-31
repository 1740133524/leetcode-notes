# 面试题 17.21. 直方图的水量

## 题目

给定一个直方图(也称柱状图)，假设有人从上面源源不断地倒水，最后直方图能存多少水量?直方图的宽度为 1。

## 示例

	输入: [0,1,0,2,1,0,1,3,2,1,2,1]
	输出: 6

## 分析

这道题目和之前的 42. 接雨水 一样。

可以用一种新的方法

双指针，记录两侧最大的值，从最大值小的一边往中间移动，同时结算，并且更新最大值

## 代码
	
	class Solution {
	public:
	    int trap(vector<int>& height) {
	        if(height.size() < 3) return 0;
	        int l = 0;
	        int r = height.size()-1;
	        int ret = 0;
	        int l_max = height[l];
	        int r_max = height[r];
	        while(l < r){
	            if(l_max < r_max){
	                ret += l_max - height[l]; // 加上height[l]可以存储的水
	                l++; // 要先++；
	                l_max = max(l_max, height[l]); // 更新新的最大左端点
	            }
	            else{
	                ret += r_max - height[r]; // 加上height[r]可以存储的水
	                r--;
	                r_max = max(r_max, height[r]); // 更新新的最大右端点
	            }
	        }
	        return ret;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/volume-of-histogram-lcci/submissions/](https://leetcode-cn.com/problems/volume-of-histogram-lcci/submissions/)