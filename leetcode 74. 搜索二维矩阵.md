# 74. 搜索二维矩阵

## 题目

编写一个高效的算法来判断 m x n 矩阵中，是否存在一个目标值。该矩阵具有如下特性：

* 每行中的整数从左到右按升序排列。
* 每行的第一个整数大于前一行的最后一个整数。

## 示例

示例 1:

	输入:
	matrix = [
	  [1,   3,  5,  7],
	  [10, 11, 16, 20],
	  [23, 30, 34, 50]
	]
	target = 3
	输出: true

示例 2:

	输入:
	matrix = [
	  [1,   3,  5,  7],
	  [10, 11, 16, 20],
	  [23, 30, 34, 50]
	]
	target = 13
	输出: false

## 分析

使用正常的二分只不过每次取中间的值的时候转换成坐标形式

## 代码
	
	class Solution {
	public:
	    bool searchMatrix(vector<vector<int>>& matrix, int target) {
	        int m = matrix.size();
	        if(m == 0) return false;
	        int n = matrix[0].size();
	        int l = 0;
	        int r = m*n-1;
	        while(l <= r){
	            int mid = (l + r) / 2;
	            int x = mid / n;
	            int y = mid % n;
	            if(matrix[x][y] < target) l = mid+1;
	            else if(matrix[x][y] > target) r = mid-1;
	            else return true; 
	        }
	        return false;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/search-a-2d-matrix/](https://leetcode-cn.com/problems/search-a-2d-matrix/)