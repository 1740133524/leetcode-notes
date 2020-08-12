# 891. 子序列宽度之和

## 题目

给定一个整数数组 A ，考虑 A 的所有非空子序列。

对于任意序列 S ，设 S 的宽度是 S 的最大元素和最小元素的差。

返回 A 的所有子序列的宽度之和。

由于答案可能非常大，请返回答案模 10^9+7。

## 示例

	输入：[2,1,3]
	输出：6
	解释：
	子序列为 [1]，[2]，[3]，[2,1]，[2,3]，[1,3]，[2,1,3] 。
	相应的宽度是 0，0，0，1，1，2，2 。
	这些宽度之和是 6 。

## 提示

* 1 <= A.length <= 20000
* 1 <= A[i] <= 20000

## 分析

先排序数组

对于数 i：

* 成为最小元素的次数为 i 左侧的数的数量的平方减1
* 成为最大元素的次数为 i 右侧的数的数量的平方减1

## 代码
	
	class Solution {
	public:
	    int sumSubseqWidths(vector<int>& A) {
	        sort(A.begin(), A.end());
	        vector<long> v{1};
	        for(int i = 1; i <= 20000; i++)  v.push_back(v[v.size()-1] * 2 % 1000000007);
	        long ret = 0;
	        for(int i = 0; i < A.size(); i++){
	            ret = ret + A[i] * (v[i] - 1);
	            ret = (ret - A[i] * (v[A.size()-i-1]-1)) % 1000000007;
	        }
	        return ret;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/sum-of-subsequence-widths/](https://leetcode-cn.com/problems/sum-of-subsequence-widths/)