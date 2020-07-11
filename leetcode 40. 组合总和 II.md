# 40. 组合总和 II

## 题目

给定一个数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

candidates 中的每个数字在每个组合中只能使用一次。

说明：

* 所有数字（包括目标数）都是正整数。
* 解集不能包含重复的组合。 

## 示例

示例 1:
	
	输入: candidates = [10,1,2,7,6,1,5], target = 8,
	所求解集为:
	[
	  [1, 7],
	  [1, 2, 5],
	  [2, 6],
	  [1, 1, 6]
	]

示例 2:

	输入: candidates = [2,5,2,1,2], target = 5,
	所求解集为:
	[
	  [1,2,2],
	  [5]
	]

## 分析

使用dfs

需要解决解集不能包含重复的组合的问题。先排序，在dfs的时候 每层 如果遇到相邻的同样的数，只传递一次，这样就不会重复了

》 避免重复可看： https://leetcode-cn.com/problems/combination-sum-ii/solution/xiang-xi-jiang-jie-ru-he-bi-mian-zhong-fu-by-allen/

## 代码

	class Solution {
	private:
	    vector<vector<int>> ret;
	    //map<vector<int>, int> m;
	public:
	    void dfs(vector<int>& candidates, int target, int a, vector<int> vi, int h){
	        if(h > target) return;
	        if(h == target){
	            //if(m.count(vi) == 0) 
	            ret.push_back(vi);
	            //m[vi] = 1;
	        }
	        for(int i = a+1; i < candidates.size(); i++){
	            if(i != a+1 && candidates[i] == candidates[i-1]) continue; // 每层只传递第一个数
	            vi.push_back(candidates[i]);
	            dfs(candidates, target, i, vi, h + candidates[i]);
	            vi.pop_back();
	        }
	    }
	    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
	        sort(candidates.begin(), candidates.end());
	        dfs(candidates, target, -1, vector<int>(), 0);
	        return ret;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/combination-sum-ii/](https://leetcode-cn.com/problems/combination-sum-ii/)