# 84. 柱状图中最大的矩形

## 题目

给定 n 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1 。

求在该柱状图中，能够勾勒出来的矩形的最大面积。

## 示例

	输入: [2,1,5,6,2,3]
	输出: 10

## 分析

使用单调栈，设栈顶柱子高度为g，从左向右遍历，设遍历到第i个柱子

* 遇到比g高或者相等的柱子入栈
* 遇到比g低的，就开始出栈，直到栈空或者栈顶高度小于g，设栈中第二个柱子高度为g1
	* g1 < g，那么表明高度为g的矩形为的宽为`i-栈中第二个柱子的位置-1
	* g1 == g，可以和上面处理方式相同，也可以跳过

可以通过给数组最后添加一个0来遍历完后计算栈中剩下的矩形

## 代码

	class Solution {
	public:
	    int largestRectangleArea(vector<int>& heights) {
	        vector<int> vi;
	        int ret = 0;
	        heights.push_back(0);
	        for(int i = 0; i < heights.size(); i++){
	            for(int j = vi.size()-1; j >= 0 && heights[vi[j]] > heights[i]; j--){
	                if(j > 0) ret = max(ret, heights[vi[j]] * (i - vi[j-1] - 1));
	                else ret = max(ret, heights[vi[j]] * i);
	                vi.pop_back();
	            }
	            vi.push_back(i);
	        }
	        return ret;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/largest-rectangle-in-histogram/](https://leetcode-cn.com/problems/largest-rectangle-in-histogram/)