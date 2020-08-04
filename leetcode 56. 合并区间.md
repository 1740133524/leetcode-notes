# 56. 合并区间

## 题目

给出一个区间的集合，请合并所有重叠的区间。

## 示例

示例 1:

	输入: [[1,3],[2,6],[8,10],[15,18]]
	输出: [[1,6],[8,10],[15,18]]
	解释: 区间 [1,3] 和 [2,6] 重叠, 将它们合并为 [1,6].

示例 2:

	输入: [[1,4],[4,5]]
	输出: [[1,5]]
	解释: 区间 [1,4] 和 [4,5] 可被视为重叠区间。

## 分析

将数组拆分成左右边界的情况，排序

使用栈找到最外层的两个边界加入返回数组即可

> 还可以使用双指针

## 代码
	
	bool bj(vector<int> a, vector<int> b){
	    if(a[0] == b[0]) return a[1] < b[1]; // 注意遇到相同的值右括号要放在左括号前
	    return a[0] < b[0];
	}
	class Solution {
	public:
	    vector<vector<int>> merge(vector<vector<int>>& intervals) {
	        vector<vector<int>> v;
	        vector<vector<int>> ret;
	        for(int i = 0; i < intervals.size(); i++){ // 拆分成左括号，右括号的形式
	             v.push_back(vector<int>{intervals[i][0], 0});
	             v.push_back(vector<int>{intervals[i][1], 1});
	        }
	        sort(v.begin(), v.end(), bj);
	        vector<int> v1;
	        for(int i = 0; i < v.size(); i++){ 
	            if(v[i][1] == 0) v1.push_back(v[i][0]); // 遇到左括号入栈
	            else{ // 遇到右括号出栈，直到栈中只剩一个左括号时将左右括号的值返回
	                if(v1.size() == 1){
	                    ret.push_back(vector<int>{v1[0], v[i][0]});
	                }
	                v1.pop_back();
	            }
	        }
	        return ret;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/merge-intervals/](https://leetcode-cn.com/problems/merge-intervals/)