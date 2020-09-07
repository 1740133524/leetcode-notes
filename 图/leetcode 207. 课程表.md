# 207. 课程表

## 题目

你这个学期必须选修 numCourse 门课程，记为 0 到 numCourse-1 。

在选修某些课程之前需要一些先修课程。 例如，想要学习课程 0 ，你需要先完成课程 1 ，我们用一个匹配来表示他们：[0,1]

给定课程总量以及它们的先决条件，请你判断是否可能完成所有课程的学习？

## 示例

示例 1:
	
	输入: 2, [[1,0]] 
	输出: true
	解释: 总共有 2 门课程。学习课程 1 之前，你需要完成课程 0。所以这是可能的。

示例 2:

	输入: 2, [[1,0],[0,1]]
	输出: false
	解释: 总共有 2 门课程。学习课程 1 之前，你需要先完成​课程 0；并且学习课程 0 之前，你还应先完成课程 1。这是不可能的。

## 分析

将前置课程和当前课程的关系看做一张有向图，如果有向图中有环就代表无法完成所有课程的学习

可以使用拓扑排序来完成

## 代码
	
	class Solution {
	public:
	    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
	        vector<vector<int>> v(numCourses); // 记录学完当前课程后可以学习的下一课程
	        vector<int> v1(numCourses, 0); // 记录每个课程的前置课程数量
	        vector<int> v2; // 记录前置课程数量为0的课程
	        int n = 0;
	        for(int i = 0; i < prerequisites.size(); i++){ // 初始化
	            v[prerequisites[i][1]].push_back(prerequisites[i][0]);
	            v1[prerequisites[i][0]]++;
	        }
	        for(int i = 0; i < numCourses; i++) if(v1[i] == 0) v2.push_back(i); // 找到无前置课程的课程
	        while(v2.size()){
	            n++;
	            int z = v2[v2.size()-1];
	            v2.pop_back();
	            for(int i = 0; i < v[z].size(); i++){ // 学完当前课程后将后置课程的前置课程数量-1
	                v1[v[z][i]]--;
	                if(v1[v[z][i]] == 0) v2.push_back(v[z][i]); // 如果后置课程的前置课程数量为0，加入v2
	            }
	        }
	        return n == numCourses ? true : false;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/course-schedule/](https://leetcode-cn.com/problems/course-schedule/)