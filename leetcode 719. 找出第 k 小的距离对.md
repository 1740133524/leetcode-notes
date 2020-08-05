# 719. 找出第 k 小的距离对

## 题目

给定一个整数数组，返回所有数对之间的第 k 个最小距离。一对 (A, B) 的距离被定义为 A 和 B 之间的绝对差值。

## 示例

	输入：
	nums = [1,3,1]
	k = 1
	输出：0 
	解释：
	所有数对如下：
	(1,3) -> 2
	(1,1) -> 0
	(3,1) -> 2
	因此第 1 个最小距离的数对是 (1,1)，它们之间的距离为 0。

### 提示

* 2 <= len(nums) <= 10000.
* 0 <= nums[i] < 1000000.
* 1 <= k <= len(nums) * (len(nums) - 1) / 2.

## 分析

根据距离来二分，使用双指针来计算有多少数对小于m

## 代码
	
	class Solution {
	public:
	    int smallestDistancePair(vector<int>& nums, int k) {
	        // 根据距离来二分，使用双指针来计算有多少数对小于m
	        sort(nums.begin(), nums.end());
	        int l = 0;
	        int r = nums[nums.size()-1] - nums[0];
	        while(l < r){
	            int m = (l+r)/2;
	            int z = 0;
	            for(int l1 = 0, r1 = 1; r1 < nums.size(); r1++){
	                while(nums[r1] - nums[l1] > m)  l1++;
	                z += r1 - l1;
	                if(z > k) break;
	            }
	            if(z >= k) r = m;
	            else if(z < k) l = m+1;
	        }
	        return l;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/find-k-th-smallest-pair-distance/](https://leetcode-cn.com/problems/find-k-th-smallest-pair-distance/)