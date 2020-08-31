# 16. 最接近的三数之和

## 题目

给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

## 示例

	输入：nums = [-1,2,1,-4], target = 1
	输出：2
	解释：与 target 最接近的和是 2 (-1 + 2 + 1 = 2) 。

### 提示：

* 3 <= nums.length <= 10^3
* -10^3 <= nums[i] <= 10^3
* -10^4 <= target <= 10^4

## 分析

排序

遍历时可以先确定一个数i

剩下两个数可以用双指针的方式求出

l指向i+1, r指向最后一个数

* 三数相加小于target，l++
* 三数相加大于target，r--
* 相等直接返回
* 中途记录离target最近的值

> 和 leetcode 11. 盛最多水的容器、leetcode 15. 三数之和 有点像

## 代码

	class Solution {
	public:
	    int threeSumClosest(vector<int>& nums, int target) {
	        sort(nums.begin(), nums.end());
	        int ret = 1000000;
	        for(int i = 0; i < nums.size(); i++){
	            int l = i+1;
	            int r = nums.size()-1;
	            while(l < r){
	                int h = nums[i] + nums[l] + nums[r];
	                int q = ret - target > 0 ? ret - target : target - ret;
	                int q1 = h - target > 0 ? h - target : target - h;
	                if(q1 < q) ret = h;
	                if(h == target) return h;
	                else if(h > target) r--;
	                else l++;
	            }
	        }
	        return ret;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/3sum-closest/](https://leetcode-cn.com/problems/3sum-closest/)