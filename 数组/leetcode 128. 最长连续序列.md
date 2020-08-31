# 128. 最长连续序列

## 题目

给定一个未排序的整数数组，找出最长连续序列的长度。

要求算法的时间复杂度为 O(n)。

## 示例

	输入: [100, 4, 200, 1, 3, 2]
	输出: 4
	解释: 最长连续序列是 [1, 2, 3, 4]。它的长度为 4。

## 分析

### 方法一

注意map是红黑树，不符合O(n)的复杂度

使用unordered_map，key是数组中的数，value存两个数，一个是当前数连续的最左侧的值，另一个是当前数连续的最右侧的值

每次添加一个数，可以根据左侧的数的左值和右侧数的右值来判断新的连续子序列的两端

每次只要更新两端的值即可，因为之后每次添加数需要判断的也只是序列的两端而已

### 方法二

直接看代码

## 代码

### 方法一

	class Solution {
	public:
	    int longestConsecutive(vector<int>& nums) {
	        unordered_map<int, pair<int, int>> m;
	        int ret = 0;
	        for(int i = 0; i < nums.size(); i++){
	            if(m.count(nums[i])) continue;
	            m[nums[i]];
	            int l;
	            int r; 
	            if(m.count(nums[i]-1)) l = m[nums[i]-1].first;
	            else l = nums[i];
	            if(m.count(nums[i]+1)) r = m[nums[i]+1].second;
	            else r = nums[i];
	            m[l].first = l;
	            m[l].second = r;
	            m[r].first = l;
	            m[r].second = r;
	            ret = max(r-l+1, ret);
	        }
	        return ret;
	    }
	};

### 方法二

	class Solution {
	public:
	    int longestConsecutive(vector<int>& nums) {
	        unordered_set<int> uset;
	        for (int num : nums)
	            uset.insert(num);
	        int longest = 0;
	        for (int num : uset) {
	            // 判断当前数的前一个数是否存在，若存在证明当前数不是序列的开头，跳过
	            if (uset.find(num - 1) == uset.end()) {
	                int cnt = 1;
	                while (uset.find(num + 1) != uset.end()) {
	                    num++;
	                    cnt++;
	                }
	                longest = max(longest, cnt);
	            }
	        }
	        return longest;
	    }
	}

> 题目网址：[https://leetcode-cn.com/problems/longest-consecutive-sequence/](https://leetcode-cn.com/problems/longest-consecutive-sequence/)