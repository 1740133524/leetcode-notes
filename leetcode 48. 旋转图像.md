# 48. 旋转图像

## 题目

给定一个 n × n 的二维矩阵表示一个图像。

将图像顺时针旋转 90 度。

说明：

你必须在原地旋转图像，这意味着你需要直接修改输入的二维矩阵。请不要使用另一个矩阵来旋转图像。

## 示例

示例 1:

	给定 matrix = 
	[
	  [1,2,3],
	  [4,5,6],
	  [7,8,9]
	],
	
	原地旋转输入矩阵，使其变为:
	[
	  [7,4,1],
	  [8,5,2],
	  [9,6,3]
	]

示例 2:

	给定 matrix =
	[
	  [ 5, 1, 9,11],
	  [ 2, 4, 8,10],
	  [13, 3, 6, 7],
	  [15,14,12,16]
	], 
	
	原地旋转输入矩阵，使其变为:
	[
	  [15,13, 2, 5],
	  [14, 3, 4, 1],
	  [12, 6, 8, 9],
	  [16, 7,10,11]
	]

## 分析

从外到内一圈一圈转

## 代码

	class Solution {
	public:
	    void rotate(vector<vector<int>>& matrix) {
	        int n = matrix.size();
	        for(int x = 0, y = 0; x < n/2; x++, y++){
	            int x1 = x; // 左上
	            int y1 = y;
	            int x2 = x; // 右上
	            int y2 = n - y - 1;
	            int x3 = n - x - 1; // 左下
	            int y3 = y;
	            int x4 = n - x - 1; // 右下
	            int y4 = n - y - 1;
	            for(int i = 0; i < n - 1 - x * 2; i++){
	                int z = matrix[x1][y1+i];
	                matrix[x1][y1+i] = matrix[x3-i][y3];
	                matrix[x3-i][y3] = matrix[x4][y4-i];
	                matrix[x4][y4-i] = matrix[x2+i][y2];
	                matrix[x2+i][y2] = z;
	            }
	        }
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/rotate-image/](https://leetcode-cn.com/problems/rotate-image/)