# 56. 合并区间

## 题目

给定一个正整数 n，生成一个包含 1 到 n2 所有元素，且元素按顺时针顺序螺旋排列的正方形矩阵。

## 示例

输入: 3
输出:
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]

## 分析

和 [54. 螺旋矩阵](https://leetcode-cn.com/problems/spiral-matrix/) 一样，只要设定四个角转向的位置即可

## 代码
	
	class Solution {
	public:
	    vector<vector<int>> generateMatrix(int n) {
	        vector<vector<int>> ret(n, vector<int>(n, 0));
	        vector<vector<int>> v{{1, 0}, {0, n-1}, {n-1, n-1}, {n-1, 0}};
	        vector<vector<int>> v1{{1, 1}, {1, -1}, {-1, -1}, {-1, 1}};
	        int a = 1;
	        int b = 1;
	        int x = 0;
	        int y = 0;
	        while(a <= n*n){ 
	            ret[x][y] = a;
	            a++;
	            if(x == v[b][0] && y == v[b][1]){
	                v[b][0] += v1[b][0];
	                v[b][1] += v1[b][1];
	                b = (b+1)%4;
	            }
	            if(b == 0) x--;
	            else if(b == 1) y++;
	            else if(b == 2) x++;
	            else if(b == 3) y--;
	            
	        }
	        return ret;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/spiral-matrix-ii/](https://leetcode-cn.com/problems/spiral-matrix-ii/)