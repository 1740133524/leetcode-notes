# 85. 最大矩形

## 题目

给定一个仅包含 0 和 1 的二维二进制矩阵，找出只包含 1 的最大矩形，并返回其面积。

## 示例

	输入:
	[
	  ["1","0","1","0","0"],
	  ["1","0","1","1","1"],
	  ["1","1","1","1","1"],
	  ["1","0","0","1","0"]
	]
	输出: 6

## 分析

### 第一种

使用动态规划

dp[i][j][k]，表示在右下角坐标为i，j的时候，高为k的最大矩形的宽

dp[i][j][k] = min(dp[i][j][k-1], dp[i-1][j][k-1]);

### 第二种

将题目变形成一层层的 `84. 柱状图中最大的矩形` 即可

## 代码

### 第一种

	class Solution {
	public:
	    int maximalRectangle(vector<vector<char>>& matrix) {
	        if(matrix.size() == 0) return 0;
	        vector<vector<vector<int>>> dp(matrix.size(), vector<vector<int>> (matrix[0].size(), vector<int>(matrix.size(), 0)));
	        int ret = 0;;
	        for(int x = 0; x < matrix.size(); x++){
	            for(int y = 0; y < matrix[0].size(); y++){
	                if(matrix[x][y] == '1'){
	                    dp[x][y][0] = y-1 >= 0 ? dp[x][y-1][0]+1 : 1;
	                    ret = max(ret, dp[x][y][0]);
	                    for(int h = 1; x-h >= 0; h++){
	                        if(dp[x-1][y][h-1] == 0) break;
	                        dp[x][y][h] = min(dp[x][y][h-1], dp[x-1][y][h-1]);
	                        ret = max(ret, dp[x][y][h] * (h+1));
	                    }
	                }
	            }
	        }
	        return ret;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/maximal-rectangle/](https://leetcode-cn.com/problems/maximal-rectangle/)