# 57. 插入区间

## 题目

给出一个无重叠的 ，按照区间起始端点排序的区间列表。

在列表中插入一个新的区间，你需要确保列表中的区间仍然有序且不重叠（如果有必要的话，可以合并区间）。

## 示例

示例 1:

	输入: intervals = [[1,3],[6,9]], newInterval = [2,5]
	输出: [[1,5],[6,9]]

示例 2:

	输入: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
	输出: [[1,2],[3,10],[12,16]]
	解释: 这是因为新的区间 [4,8] 与 [3,5],[6,7],[8,10] 重叠。

## 分析

将区间列表拆开组成一个新的数组，格式为`[值，左侧（0）或右侧（1）]`

加入新区间，根据值排序

排序时注意如果有两个值相同，将左区间排在右区间前

使用栈

遍历数组：

* 遇到左区间，入栈
* 遇到右区间
	* 如果栈中只有一个值，将栈中左区间和当前右区间组成一个区间加入返回数组
	* 如果栈中有两个值，将栈顶pop

## 代码

	bool bj(pair<int, int> a, pair<int, int> b){
	    if(a.first == b.first) return a.second < b.second;
	    return a.first < b.first;
	}
	class Solution {
	public:
	    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
	        vector<pair<int, int>> v;
	        vector<vector<int>> ret;
	        vector<int> vi;
	        for(int i = 0; i < intervals.size(); i++){
	            v.push_back(pair<int, int>{intervals[i][0], 0});
	            v.push_back(pair<int, int>{intervals[i][1], 1});
	        }
	        v.push_back(pair<int, int>{newInterval[0], 0});
	        v.push_back(pair<int, int>{newInterval[1], 1});
	        sort(v.begin(), v.end(), bj);
	        for(int i = 0; i < v.size(); i++){
	            if(v[i].second == 0) vi.push_back(v[i].first);
	            else{
	                if(vi.size() == 1){
	                    vi.push_back(v[i].first);
	                    ret.push_back(vi);
	                    vi.clear();
	                }
	                else{
	                    vi.pop_back();
	                }
	            }
	        }
	        return ret;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/insert-interval/](https://leetcode-cn.com/problems/insert-interval/)