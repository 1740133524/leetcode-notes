# 18. 四数之和

## 题目

给定一个包含 n 个整数的数组 nums 和一个目标值 target，判断 nums 中是否存在四个元素 a，b，c 和 d ，使得 a + b + c + d 的值与 target 相等？找出所有满足条件且不重复的四元组。

注意：

答案中不可以包含重复的四元组。

## 示例

	给定数组 nums = [1, 0, -1, 0, -2, 2]，和 target = 0。
	
	满足要求的四元组集合为：
	[
	  [-1,  0, 0, 1],
	  [-2, -1, 1, 2],
	  [-2,  0, 0, 2]
	]

## 分析

和上次那道三数之和有点像，只要在外层再加一个循环就可以了

> `15. 三数之和`:[https://leetcode-cn.com/problems/3sum/](https://leetcode-cn.com/problems/3sum/)

## 代码

	class Solution {
	public:
	    vector<vector<int>> fourSum(vector<int>& nums, int target) {
	        sort(nums.begin(), nums.end());
	        vector<vector<int>> ret;
	        for(int i = 0; i < nums.size();){
	            for(int j = i+1; j < nums.size();){
	                for(int l = j+1, r = nums.size()-1; l < r;){
	                    int h = nums[i] + nums[j] + nums[l] + nums[r];
	                    if(h == target){
	                        ret.push_back(vector<int>{nums[i], nums[j], nums[l], nums[r]});
	                        l++;
	                        r--;
	                        while(l < r && nums[l] == nums[l-1]) l++;
	                        while(l < r && nums[r] == nums[r+1]) r--;
	                    }
	                    else if(h < target){
	                        l++;
	                        while(l < r && nums[l] == nums[l-1]) l++;
	                    }
	                    else{
	                        r--;
	                        while(l < r && nums[r] == nums[r+1]) r--;
	                    }
	                }
	                j++;
	                while(j < nums.size() && nums[j] == nums[j-1]) j++;
	            }
	            i++;
	            while(i < nums.size() && nums[i] == nums[i-1]) i++;
	        }
	        return ret;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/4sum/](https://leetcode-cn.com/problems/4sum/)