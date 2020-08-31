# 685. 冗余连接 II

## 题目

在本问题中，有根树指满足以下条件的有向图。该树只有一个根节点，所有其他节点都是该根节点的后继。每一个节点只有一个父节点，除了根节点没有父节点。

输入一个有向图，该图由一个有着N个节点 (节点值不重复1, 2, ..., N) 的树及一条附加的边构成。附加的边的两个顶点包含在1到N中间，这条附加的边不属于树中已存在的边。

结果图是一个以边组成的二维数组。 每一个边 的元素是一对 [u, v]，用以表示有向图中连接顶点 u 和顶点 v 的边，其中 u 是 v 的一个父节点。

返回一条能删除的边，使得剩下的图是有N个节点的有根树。若有多个答案，返回最后出现在给定二维数组的答案。

## 示例

示例 1:
	
	输入: [[1,2], [1,3], [2,3]]
	输出: [2,3]
	解释: 给定的有向图如下:
	  1
	 / \
	v   v
	2-->3

示例 2:

	输入: [[1,2], [2,3], [3,4], [4,1], [1,5]]
	输出: [4,1]
	解释: 给定的有向图如下:
	5 <- 1 -> 2
	     ^    |
	     |    v
	     4 <- 3

## 分析

有两种可能

* 多出来的边连通根结点，每个结点的入度为1
	* 遍历树，找出环，返回最后出现在给定二维数组的边
* 多出来的边不连通根结点，有一个结点的入度为2
	* 尝试删除入度为2的其中一条边，若无环，就返回另一条边，若有环，返回靠后的那条边

## 代码
	
	class Solution {
	private:
	    map<int, vector<int>> m; // 记录每个结点的边
	    map<int, map<int, int>> m1; // 记录入度为1的可能中形成环的边
	public:
	    int dfs(int root, vector<int>& vi){ // 返回值大于0表示环的起点，返回值等于0表示无环，返回值等于-1表示已找到环并且已经将环全部遍历完成
	        if(vi[root] == 1) return root;
	        vi[root]++;
	        for(int i = 0; i < m[root].size(); i++){
	            int z = dfs(m[root][i], vi);
	            if(z > 0){
	                if(root != z){
	                    m1[root][m[root][i]] = 1;
	                    return z;
	                }
	                else{ // 遇到环开始的结点时表示已找到环并且已经将环全部遍历完成
	                    m1[root][m[root][i]] = 1;
	                    return -1;
	                }
	                    
	            }
	            else if(z == -1) return -1;
	        }
	        return 0; 
	    }
	    vector<int> findRedundantDirectedConnection(vector<vector<int>>& edges) {
	        vector<int> v(edges.size()+1, 0);
	        int z1 = -1; // 记录入度为2时的第一条边
	        int z2 = -1; // 记录入度为2时的第二条边
	        int a = -1; // 记录入度为2的结点
	        // 初始化
	        for(int i = 0; i < edges.size();i++){
	            m[edges[i][0]].push_back(edges[i][1]);
	            if(v[edges[i][1]] != 0){
	                z1 = v[edges[i][1]];
	                z2 = edges[i][0];
	                a = edges[i][1];
	            }
	            v[edges[i][1]] = edges[i][0];
	        }
	        if(z1 == -1){
	            vector<int> vi(edges.size()+1, 0);
	            for(int i = 1; i < vi.size(); i++){ // 从每个节点开始遍历找环
	                if(vi[i] == 0){
	                    if(dfs(i, vi) == -1){
	                        // 找到环后返回最后一个出现的边
	                        for(int j = edges.size()-1; j >= 0; j--){
	                            if(m1[edges[j][0]][edges[j][1]] == 1){
	                                return edges[j];
	                            }
	                        }
	                    }
	                }
	            }
	        }
	        else{
	            for(int i = 0; i < m[z2].size(); i++){
	                if(m[z2][i] == a){
	                    m[z2].erase(m[z2].begin()+i);
	                    vector<int> vi(edges.size()+1, 0);
	                    if(dfs(a, vi) == -1) return vector<int>{z1, a}; // 如果当前删除当前边还有环返回另一条边
	                    else return vector<int>{z2, a}; // 因为z2本就是靠后的边，所以一但删除后无环，就返回z2那条边
	                }
	            }
	        }
	
	        return vector<int>{};
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/redundant-connection-ii/submissions/](https://leetcode-cn.com/problems/redundant-connection-ii/submissions/)