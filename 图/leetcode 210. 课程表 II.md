# 210. 课程表 II

## 题目

现在你总共有 n 门课需要选，记为 0 到 n-1。

在选修某些课程之前需要一些先修课程。 例如，想要学习课程 0 ，你需要先完成课程 1 ，我们用一个匹配来表示他们: [0,1]

给定课程总量以及它们的先决条件，返回你为了学完所有课程所安排的学习顺序。

可能会有多个正确的顺序，你只要返回一种就可以了。如果不可能完成所有课程，返回一个空数组。

## 示例

示例 1:

	输入: 2, [[1,0]] 
	输出: [0,1]
	解释: 总共有 2 门课程。要学习课程 1，你需要先完成课程 0。因此，正确的课程顺序为 [0,1] 。

示例 2:

	输入: 4, [[1,0],[2,0],[3,1],[3,2]]
	输出: [0,1,2,3] or [0,2,1,3]
	解释: 总共有 4 门课程。要学习课程 3，你应该先完成课程 1 和课程 2。并且课程 1 和课程 2 都应该排在课程 0 之后。
	     因此，一个正确的课程顺序是 [0,1,2,3] 。另一个正确的排序是 [0,2,1,3] 。

## 分析

和 207. 课程表 差不多，将前置课程和当前课程的关系看做一张有向图。如果有向图中有环就代表无法完成所有课程的学习，如果没环，就用拓扑排序找出一个序列即可

## 代码

	class Solution {
	public:
	    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
	        vector<vector<int>> v(numCourses); // 记录学完当前课程后可以学习的下一课程
	        vector<int> v1(numCourses, 0); // 记录每个课程的前置课程数量
	        vector<int> v2; // 记录前置课程数量为0的课程
	        vector<int> ret;
	        for(int i = 0; i < prerequisites.size(); i++){ // 初始化
	            v[prerequisites[i][1]].push_back(prerequisites[i][0]);
	            v1[prerequisites[i][0]]++;
	        }
	        for(int i = 0; i < numCourses; i++) if(v1[i] == 0) v2.push_back(i); // 找到无前置课程的课程
	        while(v2.size()){
	            int z = v2[v2.size()-1];
	            v2.pop_back();
	            ret.push_back(z);
	            for(int i = 0; i < v[z].size(); i++){ // 学完当前课程后将后置课程的前置课程数量-1
	                v1[v[z][i]]--;
	                if(v1[v[z][i]] == 0) v2.push_back(v[z][i]); // 如果后置课程的前置课程数量为0，加入v2
	            }
	
	        }
	        return ret.size() == numCourses ? ret : vector<int>();
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/course-schedule-ii/](https://leetcode-cn.com/problems/course-schedule-ii/)