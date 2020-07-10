# 126. 单词接龙 II

## 题目

给定两个单词（beginWord 和 endWord）和一个字典 wordList，找出所有从 beginWord 到 endWord 的最短转换序列。转换需遵循如下规则：

* 每次转换只能改变一个字母。
* 转换后得到的单词必须是字典中的单词。

说明:

* 如果不存在这样的转换序列，返回一个空列表。
* 所有单词具有相同的长度。
* 所有单词只由小写字母组成。
* 字典中不存在重复的单词。
* 你可以假设 beginWord 和 endWord 是非空的，且二者不相同。

## 示例

示例 1:
	
	输入:
	beginWord = "hit",
	endWord = "cog",
	wordList = ["hot","dot","dog","lot","log","cog"]
	
	输出:
	[
	  ["hit","hot","dot","dog","cog"],
	  ["hit","hot","lot","log","cog"]
	]

示例 2:
	
	输入:
	beginWord = "hit"
	endWord = "cog"
	wordList = ["hot","dot","dog","lot","log"]
	
	输出: []
	
	解释: endWord "cog" 不在字典中，所以不存在符合要求的转换序列。

## 分析

可以将每个字典中的单词看做一个结点，根据只修改一个字母来连成图

如果字典中没有 beginWord ，可以自己加一个

如果每两个单词比较过来复杂度过高。将单词存入map。将要找的节点单词的每个位置换一个字符，然后看更改后的单词在不在 map 中会快很多。

之后使用dfs就可以找到最短路径，但我们还需要找出所有路径。

所以声明一个数组，用来存储到达每个结点的上一个结点（只记录步数最少的一些结点，可以再申明一个数组用来存储到达各结点的最少步数）

最后从终点倒着dfs找出所有路径

## 代码

	class Solution {
	private:
	    vector<vector<string>> ret;
	public:
	    void dfs(unordered_map<string, vector<string>>& m2, string& beginWord, string str, vector<string> vs){
	        vs.push_back(str);
	        if(str == beginWord){
	            vector<string> v;
	            for(int i = vs.size()-1; i >= 0; i--){
	                v.push_back(vs[i]);
	            }
	            ret.push_back(v);
	            return;
	        }
	        for(int i = 0; i < m2[str].size(); i++){
	            dfs(m2, beginWord, m2[str][i], vs);
	        }
	    }
	    vector<vector<string>> findLadders(string beginWord, string endWord, vector<string>& wordList) {
	        unordered_map<string, vector<string>> m;
	        unordered_map<string, int> m1;
	        unordered_map<string, vector<string>> m2;
	        queue<string> q;
	        q.push(beginWord);
	        int z = INT_MAX;
	        for(int i = 0; i < wordList.size(); i++){
	            m[wordList[i]];
	        }
	        if(m.count(beginWord) == 0){ // 得注意要数组中没有再添加，不然会重复
	            wordList.push_back(beginWord);
	            m[beginWord];
	        }
	        for(int i = 0; i < wordList.size(); i++){
	            for(int j = 0; j < wordList[i].size(); j++){
	                string s = wordList[i];
	                for(int k = 0; k < 26; k++){
	                    if(wordList[i][j] == 'a' + k) continue;
	                    s[j] = 'a' + k;
	                    if(m.count(s)){ // 得注意添加时不需要两边都添加，因为当遍历到另一个单词时还会添加一遍
	                        m[wordList[i]].push_back(s);
	                    }
	                }
	            }
	        }
	
	        while(q.size()){
	            string s = q.front();
	            q.pop();
	            if(s == endWord) {
	                z = m1[s];
	                continue;
	            }
	            // 可加可不加，不影响结果。加了的话当找到终点后遇到距离大于最短路径的值时会跳过。不然，要等到遍历到无结点可遍历才会停下
	            if(m1[s] >= z) continue; 
	
	            for(int i = 0; i < m[s].size(); i++){
	                if(m1.count(m[s][i]) == 0){ // 遇到没碰到过的结点入队列
	                    m1[m[s][i]] = m1[s]+1;
	                    q.push(m[s][i]);
	                }
	                else if(m1[m[s][i]] < m1[s]+1) continue; // 只记录到达结点的最短路径
	                m2[m[s][i]].push_back(s); // 记录上一步的结点
	            }
	        }
	        dfs(m2, beginWord, endWord, vector<string>()); //最后倒着使用dfs遍历一遍，找出所有路径
	        return ret;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/word-ladder-ii/](https://leetcode-cn.com/problems/word-ladder-ii/)