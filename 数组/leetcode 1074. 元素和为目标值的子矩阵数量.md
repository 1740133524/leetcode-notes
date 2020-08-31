# 1074. 元素和为目标值的子矩阵数量

## 题目

给出矩阵 matrix 和目标值 target，返回元素总和等于目标值的非空子矩阵的数量。

子矩阵 x1, y1, x2, y2 是满足 x1 <= x <= x2 且 y1 <= y <= y2 的所有单元 matrix[x][y] 的集合。

如果 (x1, y1, x2, y2) 和 (x1', y1', x2', y2') 两个子矩阵中部分坐标不同（如：x1 != x1'），那么这两个子矩阵也不同。

## 示例

示例 1：

	输入：matrix = [[0,1,0],[1,1,1],[0,1,0]], target = 0
	输出：4
	解释：四个只含 0 的 1x1 子矩阵。

示例 2：

	输入：matrix = [[1,-1],[-1,1]], target = 0
	输出：5
	解释：两个 1x2 子矩阵，加上两个 2x1 子矩阵，再加上一个 2x2 子矩阵。

## 提示

* 1 <= matrix.length <= 300
* 1 <= matrix[0].length <= 300
* -1000 <= matrix[i] <= 1000
* -10^8 <= target <= 10^8

## 分析

将一维的前缀和的思路代进来

vvi[i][j] 表示从 target[0][j] 加到 target[i][j] 的和

遍历时锁定矩阵的左上角和左下角（ i 和 j ），右侧一列列添加( k )，同时记录已经遍历过的矩阵的和出现过的次数

这样可以将复杂度控制在`O(n*n*m)`，否则暴力遍历的话复杂度为`O(n*n*m*m)`

具体看代码

## 代码
	
	class Solution {
	public:
	    int numSubmatrixSumTarget(vector<vector<int>>& matrix, int target) {
	        vector<vector<int>> vvi(matrix.size(), vector<int>(matrix[0].size(), 0));
	        int ret = 0;
	        // vvi[i][j] 表示从 target[0][j] 加到 target[i][j] 的和
	        for(int j = 0; j < matrix[0].size(); j++){ 
	            int total = 0;
	            for(int i = 0; i < matrix.size(); i++){
	                total += matrix[i][j];
	                vvi[i][j] = total;
	            }
	        }
	        for(int i = 0; i < matrix.size(); i++){
	            for(int j = i; j < matrix.size(); j++){
	                // 用来存储所有出现过的矩阵的和的次数
	                unordered_map<int, int> m;
	                // 用来存遍历过的矩阵的和
	                int total = 0;
	                for(int k = 0; k < matrix[0].size(); k++){
	                    total += vvi[j][k] - (i == 0 ? 0 : vvi[i-1][k]);
	                    // 如果当前矩阵的和正好是target，返回值+1
	                    if(total == target) ret++;
	                    // 如果当前矩阵减去target的值正好在之前的矩阵出现过，那么这两个矩阵相加就刚好是target，之前出现几次这种矩阵就可以组成几个target大的矩阵
	                    if(m.count(total - target)) ret += m[total - target];
	                    m[total]++;
	                }
	            }
	        }
	        return ret;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/number-of-submatrices-that-sum-to-target/](https://leetcode-cn.com/problems/number-of-submatrices-that-sum-to-target/)