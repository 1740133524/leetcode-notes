# 1330. 翻转子数组得到最大的数组值

## 题目

给你一个整数数组 nums 。「数组值」定义为所有满足 0 <= i < nums.length-1 的 |nums[i]-nums[i+1]| 的和。

你可以选择给定数组的任意子数组，并将该子数组翻转。但你只能执行这个操作 一次 。

请你找到可行的最大 数组值 。

## 示例

示例 1：

	输入：nums = [2,3,1,5,4]
	输出：10
	解释：通过翻转子数组 [3,1,5] ，数组变成 [2,5,1,3,4] ，数组值为 10 。

示例 2：

	输入：nums = [2,4,9,24,2,1,10]
	输出：68

## 提示

* 1 <= nums.length <= 3*10^4
* -10^5 <= nums[i] <= 10^5

## 分析

可以画数轴

	交换前：
		nums[l-1]---nums[l]
							 nums[r]-----nums[r+1]
	交换后：
		nums[l-1]------------nums[r]
				    nums[l]--------------nums[r+1]

通过数轴，可以知道交换 nums[l] 和 nums[r] 后值增长了 (nums[r]-nums[l])*2 

> 参考：https://leetcode-cn.com/problems/reverse-subarray-to-maximize-array-value/solution/go-shuang-bai-jie-xi-shu-zhou-biao-shi-by-user8399/

## 代码
	
	class Solution {
	public:
	    int maxValueAfterReverse(vector<int>& nums) {
	        int l = INT_MAX;
	        int r = INT_MIN;
	        int ret = 0;
	        int sum = 0;
	        for(int i = 1; i < nums.size(); i++){
	            sum += abs(nums[i] - nums[i-1]);
	        }
	        for(int i = 1; i < nums.size(); i++){
	            
	            if(nums[i] < nums[i-1]){
	                if(nums[i] > r) r = nums[i];
	            }
	            else{
	                if(nums[i-1] > r) r = nums[i-1];
	            }
	            if(nums[i] > nums[i-1]){
	                if(nums[i] < l) l = nums[i];
	            }
	            else{
	                if(nums[i-1] < l) l = nums[i-1];
	            }
	        }
	        ret = max(sum, sum + (r - l)*2);
	
	        // 交换数组头和末尾时的情况
	        for(int i = 1; i < nums.size()-1; i++){
	            ret = max(ret, sum - abs(nums[i] - nums[i+1]) + abs(nums[0] - nums[i+1]));
	            ret = max(ret, sum - abs(nums[i] - nums[i-1]) + abs(nums[nums.size()-1] - nums[i-1]));
	        }
	        return ret;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/reverse-subarray-to-maximize-array-value/submissions/](https://leetcode-cn.com/problems/reverse-subarray-to-maximize-array-value/submissions/)