# 79. 单词搜索

## 题目

给定一个二维网格和一个单词，找出该单词是否存在于网格中。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

## 示例
	
	board =
	[
	  ['A','B','C','E'],
	  ['S','F','C','S'],
	  ['A','D','E','E']
	]
	
	给定 word = "ABCCED", 返回 true
	给定 word = "SEE", 返回 true
	给定 word = "ABCB", 返回 false

## 分析

使用dfs对以每一个字母为起点遍历一遍即可

注意使用引用节约时间

## 代码

	class Solution {
	public:
	    bool dfs(vector<vector<char>>& board, string word, int z, int x, int y){
	        if(board[x][y] != word[z]) return false; 
	        if(z == word.size()-1) return true;
	        char c = board[x][y];
	        board[x][y] = '!';
	        if(x-1 >= 0 && board[x-1][y] != '!'){
	            if(dfs(board, word, z+1, x-1, y)) return true;
	        }
	        if(x+1 < board.size() && board[x+1][y] != '!'){
	            if(dfs(board, word, z+1, x+1, y)) return true;
	        }
	        if(y-1 >= 0 && board[x][y-1] != '!'){
	            if(dfs(board, word, z+1, x, y-1)) return true;
	        }
	        if(y+1 < board[0].size() && board[x][y+1] != '!'){
	            if(dfs(board, word, z+1, x, y+1)) return true;
	        }
	        board[x][y] = c;
	        return false;
	    }
	    bool exist(vector<vector<char>>& board, string word) {
	        for(int i = 0; i < board.size(); i++){
	            for(int j = 0; j < board[0].size(); j++){
	                if(dfs(board, word, 0, i, j)) return true;
	            }
	        }
	        return false;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/word-search/](https://leetcode-cn.com/problems/word-search/)