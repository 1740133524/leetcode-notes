# 73. 矩阵置零

## 题目

给定一个 m x n 的矩阵，如果一个元素为 0，则将其所在行和列的所有元素都设为 0。请使用原地算法。

## 示例

示例 1:

	输入: 
	[
	  [1,1,1],
	  [1,0,1],
	  [1,1,1]
	]
	输出: 
	[
	  [1,0,1],
	  [0,0,0],
	  [1,0,1]
	]

示例 2:

	输入: 
	[
	  [0,1,2,0],
	  [3,4,5,2],
	  [1,3,1,5]
	]
	输出: 
	[
	  [0,0,0,0],
	  [0,4,5,0],
	  [0,3,1,0]
	]

## 分析

使用第一行第一列来记录本行（列）是否需要设置为0， 对于第一行和第一列中的0，另外使用两个标记记录是否需要设置为0

## 代码

	class Solution {
	public:
	    void setZeroes(vector<vector<int>>& matrix) {
	        int a1 = 0;
	        int a2 = 0;
	        for(int i = 0; i < matrix.size(); i++){
	            for(int j = 0; j < matrix[0].size(); j++){
	                if(matrix[i][j] == 0){
	                    if(i == 0) a1 = 1;
	                    if(j == 0) a2 = 1; 
	                    matrix[0][j] = -1;
	                    matrix[i][0] = -1;
	                }
	            }
	        }
	        for(int i = 1; i < matrix.size(); i++){
	            if(matrix[i][0] == -1){
	                for(int j = 0; j < matrix[0].size(); j++){
	                    matrix[i][j] = 0;
	                }
	            }
	        }
	        for(int i = 1; i < matrix[0].size(); i++){
	            if(matrix[0][i] == -1){
	                for(int j = 0; j < matrix.size(); j++){
	                    matrix[j][i] = 0;
	                }
	            }
	        }
	        if(a2){
	            for(int i = 0; i < matrix.size(); i++){
	                matrix[i][0] = 0;
	            }
	        }
	        if(a1){
	            for(int i = 0; i < matrix[0].size(); i++){
	                matrix[0][i] = 0;
	            }
	        }
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/set-matrix-zeroes/](https://leetcode-cn.com/problems/set-matrix-zeroes/)