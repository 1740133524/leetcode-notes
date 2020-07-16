# 54. 螺旋矩阵

## 题目

给定一个包含 m x n 个元素的矩阵（m 行, n 列），请按照顺时针螺旋顺序，返回矩阵中的所有元素。

## 示例

示例 1:

	输入:
	[
	 [ 1, 2, 3 ],
	 [ 4, 5, 6 ],
	 [ 7, 8, 9 ]
	]
	输出: [1,2,3,6,9,8,7,4,5]

示例 2:

	输入:
	[
	  [1, 2, 3, 4],
	  [5, 6, 7, 8],
	  [9,10,11,12]
	]
	输出: [1,2,3,4,8,12,11,10,9,5,6,7]

## 分析

声明四个角，每次到角就转向，并且更新角的位置

左上角需要特殊处理，将要遇到时直接转向不输入，别的角输入后转向

使用一个计数器来记录还剩多少没输出

特殊处理宽为1的矩形

## 代码
	
	class Solution {
	public:
	    vector<int> spiralOrder(vector<vector<int>>& matrix) {
	        int m = matrix.size();
	        if(m == 0) return vector<int>();
	        int n = matrix[0].size();
	        vector<vector<int>> v{{0, 0}, {0, n-1}, {m-1, n-1}, {m-1, 0}};
	        vector<vector<int>> v1{{1, 1}, {1, -1}, {-1, -1}, {-1, 1}};
	        int z = m*n;
	        vector<int> ret;
	        if(n == 1){
	            for(int i = 0; i < m; i++){
	                ret.push_back(matrix[i][0]);
	            }
	            return ret;
	        }
	        ret.push_back(matrix[0][0]);
	        z--;
	        for(int x = 0, y = 1, a = 1; z > 0; z--){
	            if(a == 0 && v[a][0] == x && v[a][1] == y){
	                x++;
	                y++;
	                v[a][0] += v1[a][0];
	                v[a][1] += v1[a][1];
	                a = (a + 1) % 4;
	                z++;
	                continue;
	            }
	            ret.push_back(matrix[x][y]);
	            if(v[a][0] == x && v[a][1] == y){
	                v[a][0] += v1[a][0];
	                v[a][1] += v1[a][1];
	                a = (a + 1) % 4;
	            }
	            if(a == 0) x--;
	            else if(a == 1) y++;
	            else if(a == 2) x++;
	            else if(a == 3) y--;
	        }
	        return ret;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/spiral-matrix/](https://leetcode-cn.com/problems/spiral-matrix/)