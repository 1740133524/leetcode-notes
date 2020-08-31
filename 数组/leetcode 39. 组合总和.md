# 39. 组合总和

## 题目

给定一个无重复元素的数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

candidates 中的数字可以无限制重复被选取。

说明：

* 所有数字（包括 target）都是正整数。
* 解集不能包含重复的组合。 

## 示例

示例 1:

	输入: candidates = [2,3,6,7], target = 7,
	所求解集为:
	[
	  [7],
	  [2,2,3]
	]

示例 2:

	输入: candidates = [2,3,5], target = 8,
	所求解集为:
	[
	  [2,2,2,2],
	  [2,3,3],
	  [3,5]
	]

## 分析

使用dfs递归遍历一遍，遇到大于target就剪枝

## 代码

	class Solution {
	private:
	    vector<vector<int>> vvi;
	public:
	    void dfs(vector<int>& candidates, int target, int n, int h, vector<int> vi){
	        if(h == target) vvi.push_back(vi);
	        if(h > target) return;
	        for(int i = n; i < candidates.size(); i++){
	            vi.push_back(candidates[i]);
	            dfs(candidates, target, i, h+candidates[i], vi);
	            vi.pop_back();
	        }
	    }
	    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
	        dfs(candidates, target, 0, 0, vector<int>());
	        return vvi;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/combination-sum/](https://leetcode-cn.com/problems/combination-sum/)