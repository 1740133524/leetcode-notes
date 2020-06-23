# 11. 盛最多水的容器

## 题目

给你 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0)。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。

说明：你不能倾斜容器，且 n 的值至少为 2。

图中垂直线代表输入数组 [1,8,6,2,5,4,8,3,7]。在此情况下，容器能够容纳水（表示为蓝色部分）的最大值为 49。

## 示例

	输入：[1,8,6,2,5,4,8,3,7]
	输出：49

## 分析

一看到题目第一反应动态规划，仔细一想好像没啥用。

最后还是瞅了眼标签，才想到用双指针。

定义两个指针l，r，从两侧开始向内移动

每次移动有两种可能：

* 移动长的板，盛水只会变少
* 移动短的板，盛水有可能不变或变多

所以很显而易见了，每次移动短的那块板

现在问题是怎么知道这样子移动不会漏掉一些更大的可能性

假设当前两块板为l和r，l板比较小，那我们移动l板。移动l板会消除一部分可能性，比如l到r-1，l到r-2...r到r+1。这些可能中可以看出短板最长也就是l板的长度，而宽一定是在减小的，所以可以得出结论，被消除的可能一定小于l到r所组成的容器

## 代码

	class Solution {
	public:
	    int maxArea(vector<int>& height) {
	        int l = 0;
	        int r = height.size()-1;
	        int ret = 0;
	        while(l != r){
	            ret = max(ret, min(height[l], height[r]) * (r-l));
	            if(height[l] < height[r]) l++;
	            else r--;
	        }
	        return ret;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/container-with-most-water/](https://leetcode-cn.com/problems/container-with-most-water/)
