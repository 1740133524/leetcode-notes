# 4. 寻找两个正序数组的中位数

## 题目

给定两个大小为 m 和 n 的正序（从小到大）数组 nums1 和 nums2。

请你找出这两个正序数组的中位数，并且要求算法的时间复杂度为 O(log(m + n))。

你可以假设 nums1 和 nums2 不会同时为空。

## 示例

示例 1:

	nums1 = [1, 3]
	nums2 = [2]

	则中位数是 2.0

示例 2:

	nums1 = [1, 2]
	nums2 = [3, 4]
	
	则中位数是 (2 + 3)/2 = 2.5

## 分析

看到 O(log(m + n))第一反应就是二分。

找中位数就是找中间一个或两个数，假设，现在要找第m个数。

可以将m个数分成两份，比较两个数组的第m/2个数字，有三种可能：

* nums1[m/2] < nums2[m/2], 这样可以判断出至少nums1的前m/2个数字是要小于中位数的，因为哪怕nums2的前m/2-1个数都是小于nums1[m/2]的，也最多是m-1个数，而中位数是第m个数。
* nums1[m/2] > nums2[m/2]，同理，可以排除掉nums2中的前m/2个数
* nums1[m/2] == nums2[m/2]， 可以按照第一种可能进行处理

这样子每轮可以减去一半的数，时间复杂度就为O(log(m + n))了

中途还有一些小的细节，比如：

* m/2大于其中一个数组的个数，那么直接将这个数组m/2调整为此数组的最后一个数。
* 有一个数组全部都小于中位数，就直接从另一个的数组找对应剩下的数即可

## 代码

	class Solution {
	public:
	    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
	        int m = (nums1.size() + nums2.size() + 1) / 2;
	        int n1l = 0;
	        int n2l = 0;
	        while(m > 1){
	            if(nums1.size() - n1l <= 0 || nums2.size() - n2l <= 0) break;
	            int n1, n2;
	            int a1, a2;
	            if(m/2+n1l-1 >= nums1.size()) {
	                n1 = nums1[nums1.size()-1];
	                a1 = nums1.size()-1;
	            }
	            else {
	                n1 = nums1[m/2+n1l-1];
	                a1 = m/2+n1l-1;
	            }
	            if(m/2+n2l-1 >= nums2.size()) {
	                n2 = nums2[nums2.size()-1];
	                a2 = nums2.size()-1;
	            }
	            else {
	                n2 = nums2[m/2+n2l-1];
	                a2 = m/2+n2l-1;
	            }
	            
	            if(n1 <= n2){
	                m -= a1 - n1l+1; 
	                n1l = a1+1;
	            }
	            else if(n1 > n2){
	                m -= a2 - n2l+1; 
	                n2l = a2+1;
	            }
	        }
	        if((nums1.size() + nums2.size()) % 2 == 0){
	            int a;
	            int b;
	            if(nums1.size() - n1l <= 0){
	                a = nums2[n2l+m-1];
	                b = nums2[n2l+m-1+1];
	                return double(a+b) / 2;
	            }
	            else if(nums2.size() - n2l <= 0){
	                a = nums1[n1l+m-1];
	                b = nums1[n1l+m-1+1];
	                return double(a+b) / 2;
	            }
	            if(nums1[n1l] < nums2[n2l]){
	                a = nums1[n1l];
	                if(n1l+1 < nums1.size())
	                    b = nums1[n1l+1] < nums2[n2l] ? nums1[n1l+1] : nums2[n2l];
	                else b = nums2[n2l];
	            }
	            else{
	                a = nums2[n2l];
	                if(n2l+1 < nums2.size())
	                    b = nums2[n2l+1] < nums1[n1l] ? nums2[n2l+1] : nums1[n1l];
	                else b = nums1[n1l];
	            }
	            return double(a+b) / 2;
	        }
	        else{
	            if(nums1.size() - n1l <= 0){
	                return double(nums2[n2l+m-1]);
	            }
	            else if(nums2.size() - n2l <= 0){
	                return double(nums1[n1l+m-1]);
	            }
	            return double(nums1[n1l] < nums2[n2l] ? nums1[n1l] : nums2[n2l]);
	        }
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/median-of-two-sorted-arrays/](https://leetcode-cn.com/problems/median-of-two-sorted-arrays/)
