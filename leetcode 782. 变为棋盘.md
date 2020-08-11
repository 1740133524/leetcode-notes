# 782. 变为棋盘

## 题目

一个 N x N的 board 仅由 0 和 1 组成 。每次移动，你能任意交换两列或是两行的位置。

输出将这个矩阵变为 “棋盘” 所需的最小移动次数。“棋盘” 是指任意一格的上下左右四个方向的值均与本身不同的矩阵。如果不存在可行的变换，输出 -1。

## 示例

	输入: board = [[0,1,1,0],[0,1,1,0],[1,0,0,1],[1,0,0,1]]
	输出: 2
	解释:
	一种可行的变换方式如下，从左到右：
	
	0110     1010     1010
	0110 --> 1010 --> 0101
	1001     0101     1010
	1001     0101     0101
	
	第一次移动交换了第一列和第二列。
	第二次移动交换了第二行和第三行。
	
	
	输入: board = [[0, 1], [1, 0]]
	输出: 0
	解释:
	注意左上角的格值为0时也是合法的棋盘，如：
	
	01
	10
	
	也是合法的棋盘.
	
	输入: board = [[1, 0], [1, 0]]
	输出: -1
	解释:
	任意的变换都不能使这个输入变为合法的棋盘。

## 提示

* board 是方阵，且行列数的范围是[2, 30]。
* board[i][j] 将只包含 0或 1。

## 分析

先判断是否可以组成棋盘

* 每一行或每一列0和1的数量差不能超过1
* 行或列只有两种形式，比如第一行为001，那么之后的行只能为001或110 (倒着想，合格的棋盘本身只有两种行。交换行不影响行内的排序，交换列，只会影响顺序但因为交换列是所有的行顺序一起改变，所以行还是  只有两种形式)

因为移动行对行内的数据无影响，列同理，所以可以分开先移动列再移动行

## 代码
	
	class Solution {
	public:
	    int movesToChessboard(vector<vector<int>>& board) {
	        int n = board.size();
	        vector<int> h(n, 0); // 可以用一个int代替
	
	        int z = 0; 
	        for(int i = 0; i < n; i++){
	            if(board[0][i] == 1) z++;
	            else z--;
	        }
	        if(z > 1 || z < -1) return -1;
	
	        int z1 = 0;
	        for(int i = 0; i < n; i++){
	            if(board[i][0] == 1) z1++;
	            else z1--;
	        }
	        if(z1 > 1 || z1 < -1) return -1;
	
	
	        int q = 0;
	        int q1 = 0;
	        for(int j = 0; j < n; j++){
	            q = q*2+board[0][j];
	            q1 = q1*2+(board[0][j] == 1 ? 0:1);
	        }
	        h[0] = q;
	        for(int i = 1; i < n; i++){
	            for(int j = 0; j < n; j++){
	                h[i] = h[i]*2+board[i][j];
	            }
	            if(h[i] != q && h[i] != q1) return -1;
	        }
	
	        int a = INT_MAX;
	        int b = INT_MAX;
	        if(z > 0){
	            a = 0;
	            for(int i = 0; i < n; i++){
	                if(i % 2 == 0 && board[0][i] != 1) a++;
	            }
	        }
	        else if(z < 0){
	            b = 0;
	            for(int i = 0; i < n; i++){
	                if(i % 2 == 0 && board[0][i] != 0) b++;
	            }
	        }
	        else if(z == 0){
	            a = 0;
	            b = 0;
	            for(int i = 0; i < n; i++){
	                if(i % 2 == 0 && board[0][i] != 1) a++;
	            }
	            for(int i = 0; i < n; i++){
	                if(i % 2 == 0 && board[0][i] != 0) b++;
	            }
	        }
	        
	        int c = INT_MAX;
	        int d = INT_MAX;
	        if(z1 > 0){
	            c = 0;
	            for(int i = 0; i < n; i++){
	                if(i % 2 == 0 && board[i][0] != 1) c++;
	            }
	        }
	        else if(z1 < 0){
	            d = 0;
	            for(int i = 0; i < n; i++){
	                if(i % 2 == 0 && board[i][0] != 0) d++;
	            }
	        }
	        else if(z1 == 0){
	            c = 0;
	            d = 0;
	            for(int i = 0; i < n; i++){
	                if(i % 2 == 0 && board[i][0] != 1) c++;
	            }
	            for(int i = 0; i < n; i++){
	                if(i % 2 == 0 && board[i][0] != 0) d++;
	            }
	        }
	        return min(a, b) + min(c, d);
	
	
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/transform-to-chessboard/submissions/](https://leetcode-cn.com/problems/transform-to-chessboard/submissions/)