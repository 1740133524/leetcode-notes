# 78. 子集

## 题目

给定一组不含重复元素的整数数组 nums，返回该数组所有可能的子集（幂集）。

说明：解集不能包含重复的子集。

## 示例
	
	输入: nums = [1,2,3]
	输出:
	[
	  [3],
	  [1],
	  [2],
	  [1,2,3],
	  [1,3],
	  [2,3],
	  [1,2],
	  []
	]

## 分析

使用dfs即可

## 代码

	class Solution {
	map<vector<int>, int> m;
	public:
	    void dfs(vector<int>& nums, int z, vector<int> v){
	        if(z == nums.size()){
	            m[v] = 1;
	            return;
	        }
	        dfs(nums, z+1, v);
	        v.push_back(nums[z]);
	        dfs(nums, z+1, v);
	        v.push_back(nums[z]);
	    }
	    vector<vector<int>> subsets(vector<int>& nums) {
	        vector<vector<int>> ret;
	        dfs(nums, 0, vector<int>());
	        for(auto a = m.begin(); a != m.end(); a++){
	            ret.push_back(a->first);
	        }
	        return ret;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/subsets/](https://leetcode-cn.com/problems/subsets/)