# 面试题 17.19. 消失的两个数字

## 题目

给定一个数组，包含从 1 到 N 所有的整数，但其中缺了两个数字。你能在 O(N) 时间内只用 O(1) 的空间找到它们吗？

以任意顺序返回这两个数字均可。

## 示例

示例 1:

	输入: [1]
	输出: [2,3]

示例 2:

	输入: [2,3]
	输出: [1,4]

## 提示

* nums.length <= 30000

## 分析

可以使用原地hash，把每一个数放到和下标相同的位置。

* 还有一种方法：https://leetcode-cn.com/problems/missing-two-lcci/solution/2bian-lei-jia-qiu-jie-bu-pai-xu-by-lxy-29/

		从1到N数组nums中，缺失了2个元素。那么N = nums.size() + 2
		缺失2个数字的和sumOfTwo = sum(1..N) - sum(nums)
		记threshold = sumOfTwo/2。因为缺失的2个数字不相等，所以一个小于等于threshold,一个大于threshold。
		只对小于等于threshold的元素求和，得到第一个缺失的数字:
		sum(1..threshold) - sum(nums中, 小于等于threshold的元素)
		第二个缺失的数字: sumOfTwo - 第一个缺失的数字

## 代码
	
	class Solution {
	public:
	    vector<int> missingTwo(vector<int>& nums) {
	        nums.push_back(-1);
	        nums.push_back(-1);
	        nums.push_back(-1);
	        vector<int> ret;
	        for(int i = 0; i < nums.size(); i++){
	            int j = i;
	            while(nums[j] != j && nums[j] != -1){
	                int k = nums[j];
	                nums[j] = nums[nums[j]];
	                nums[k] = k;
	            }
	        }
	        for(int i = 1; i < nums.size(); i++){
	            if(nums[i] == -1) ret.push_back(i);
	        }
	        return ret;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/missing-two-lcci/](https://leetcode-cn.com/problems/missing-two-lcci/)