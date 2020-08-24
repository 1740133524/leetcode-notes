# 75. 颜色分类

## 题目

给定一个包含红色、白色和蓝色，一共 n 个元素的数组，原地对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。

此题中，我们使用整数 0、 1 和 2 分别表示红色、白色和蓝色。

注意:
不能使用代码库中的排序函数来解决这道题。

## 示例

输入: [2,0,2,1,1,0]
输出: [0,0,1,1,2,2]

## 分析

申明两个指针，指针l从前往后指向存储数字0的后一个位置，指针r从后往前指向存储数字2的前一个位子

遇到0时，和指针l指向的数字互换，l++  
遇到2时，和指针r指向的数字互换，r--

最后l和r之间的位置填1

## 代码

	class Solution {
	public:
	    void sortColors(vector<int>& nums) {
	        int l = 0;
	        int r = nums.size()-1;
	        while(l < nums.size() && nums[l] == 0) l++;
	        while(r >= 0 && nums[r] == 2) r--;
	
	        for(int i = l; i <= r; i++){
	            if(nums[i] == 0){
	                nums[i] = nums[l];
	                nums[l] = 0;
	                i--;
	            }
	            else if(nums[i] == 2){
	                nums[i] = nums[r];
	                nums[r] = 2;
	                i--;
	            }
	            while(l < nums.size() && nums[l] == 0) l++;
	            while(r >= 0 && nums[r] == 2) r--;
	            i = i < l ? l-1 : i;
	        }
	        while(l <= r){
	            nums[l] = 1;
	            l++;
	        }
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/sort-colors/](https://leetcode-cn.com/problems/sort-colors/)