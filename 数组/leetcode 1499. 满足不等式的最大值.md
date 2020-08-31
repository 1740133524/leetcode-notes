# 1499. 满足不等式的最大值

## 题目

给你一个数组 points 和一个整数 k 。数组中每个元素都表示二维平面上的点的坐标，并按照横坐标 x 的值从小到大排序。也就是说 points[i] = [xi, yi] ，并且在 1 <= i < j <= points.length 的前提下， xi < xj 总成立。

请你找出 yi + yj + |xi - xj| 的 最大值，其中 |xi - xj| <= k 且 1 <= i < j <= points.length。

题目测试数据保证至少存在一对能够满足 |xi - xj| <= k 的点。

## 示例

示例 1：

	输入：points = [[1,3],[2,0],[5,10],[6,-10]], k = 1
	输出：4
	解释：前两个点满足 |xi - xj| <= 1 ，带入方程计算，则得到值 3 + 0 + |1 - 2| = 4 。第三个和第四个点也满足条件，得到值 10 + -10 + |5 - 6| = 1 。
	没有其他满足条件的点，所以返回 4 和 1 中最大的那个。

示例 2：

	输入：points = [[0,0],[3,0],[9,2]], k = 3
	输出：3
	解释：只有前两个点满足 |xi - xj| <= 3 ，带入方程后得到值 0 + 0 + |0 - 3| = 3 。


## 提示

* 2 <= points.length <= 10^5
* points[i].length == 2
* -10^8 <= points[i][0], points[i][1] <= 10^8
* 0 <= k <= 2 * 10^8
* 对于所有的1 <= i < j <= points.length ，points[i][0] < points[j][0] 都成立。也就是说，xi 是严格递增的。


## 分析

可以用滑动窗口+单调队列

x本身就是有序的，根据k的大小维护一个滑动窗口[i, j]

将原表达式处理成 （yj + xj） + （yi - xi）

在单调队列中存储（yj + xj）和 xj 的值

## 代码
	
	class Solution {
	public:
	    int findMaxValueOfEquation(vector<vector<int>>& points, int k) {
	        priority_queue<pair<int, int>> q;
	        int j = 0;
	        int ret = INT_MIN;
	        for(int i = 0; i < points.size(); i++){
	            // 将k范围内的点加入单调队列
	            while(j < points.size() && points[j][0] - points[i][0] <= k){
	                q.push(pair<int, int>{points[j][0] + points[j][1], points[j][0]});
	                j++;
	            }
	            // 如果队列头的x值小于等于xi的值，就出队列
	            while(q.size() > 0 && q.top().second <= points[i][0]){
	                q.pop();
	            }
	            // 如果队列不为空，更新解
	            if(q.size() > 0){
	                ret = ret > q.top().first + points[i][1] - points[i][0] ? ret : q.top().first + points[i][1] - points[i][0];
	            }
	        }
	        return ret;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/max-value-of-equation/](https://leetcode-cn.com/problems/max-value-of-equation/)