# 839. 相似字符串组

## 题目

如果我们交换字符串 X 中的两个不同位置的字母，使得它和字符串 Y 相等，那么称 X 和 Y 两个字符串相似。如果这两个字符串本身是相等的，那它们也是相似的。

例如，"tars" 和 "rats" 是相似的 (交换 0 与 2 的位置)； "rats" 和 "arts" 也是相似的，但是 "star" 不与 "tars"，"rats"，或 "arts" 相似。

总之，它们通过相似性形成了两个关联组：{"tars", "rats", "arts"} 和 {"star"}。注意，"tars" 和 "arts" 是在同一组中，即使它们并不相似。形式上，对每个组而言，要确定一个单词在组中，只需要这个词和该组中至少一个单词相似。

我们给出了一个字符串列表 A。列表中的每个字符串都是 A 中其它所有字符串的一个字母异位词。请问 A 中有多少个相似字符串组？

## 示例

输入：["tars","rats","arts","star"]
输出：2

## 提示：

* A.length <= 2000
* A[i].length <= 1000
* A.length * A[i].length <= 20000
* A 中的所有单词都只包含小写字母。
* A 中的所有单词都具有相同的长度，且是彼此的字母异位词。
* 此问题的判断限制时间已经延长。

## 分析

假设每个单词为一个结点，对每两个单词进行判断，如果是相似字符串就给他添一条无向边

最后使用dfs来判断有多少个连通分量即可

## 代码
	
	class Solution {
	private:
	    unordered_map<string, vector<string>> m;
	    unordered_map<string, int> m1;
	public:
	    bool bj(string& a, string& b){
	        int z = 0;
	        for(int i = 0; i < a.size(); i++){
	            if(a[i] != b[i]) z++;
	            if(z > 2) break;
	        }
	        return z > 2 ? false : true;
	    }
	    void dfs(string& s){
	        if(m1[s]) return;
	        m1[s] = 1;
	        for(int i = 0; i < m[s].size(); i++){
	            dfs(m[s][i]);
	        }
	    }
	    int numSimilarGroups(vector<string>& A) {
	        int ret = 0;
	        for(int i = 0; i < A.size(); i++){
	            for(int j = i+1; j < A.size(); j++){
	                if(bj(A[i], A[j])){
	                    m[A[i]].push_back(A[j]);
	                    m[A[j]].push_back(A[i]);
	                }
	            }
	        }
	        for(int i = 0; i < A.size(); i++){
	            if(!m1[A[i]]){
	                ret++;  
	                dfs(A[i]);
	            }
	        }
	        return ret;
	    }
	
	};

> 题目网址：[https://leetcode-cn.com/problems/similar-string-groups/](https://leetcode-cn.com/problems/similar-string-groups/)