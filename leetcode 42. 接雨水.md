# 42. 接雨水

## 题目

给定 n 个非负整数表示每个宽度为 1 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。

## 示例

	输入: [0,1,0,2,1,0,1,3,2,1,2,1]
	输出: 6

## 分析

### 第一种

直接看代码注释

### 第二种

建立一个数组a，遍历height

* 遇到小于a[0]的值就加入数组。
* 遇到大于a[0]的值的时候，以最高的边为a[0]来处理数组中的数，计算可接的雨水的量。清空数组，将新的值加入数组
* 当处理完一遍之后，翻转数组a，重新进行一次之前的步骤

## 代码

### 第一种

	class Solution {
	public:
	    int trap(vector<int>& height) {
	        vector<int> vi;
	        int ret = 0;
	        for(int i = 0; i < height.size(); i++){
	            if(vi.size() > 0 && height[i] > vi[vi.size()-1]){
	                // 如果vi[0]小于等于最新的数height[i]时，那么能接住的水最高为vi[0]，并且可以将数组清空，因为不论之后的值有多大，height[i]左边将无法接到更多的雨水
	                if(vi[0] <= height[i]){  
	                    while(vi.size() > 0){ //
	                        ret += vi[0] - vi[vi.size()-1];
	                        vi.pop_back();
	                    }
	                }
	                else{ // 否则能接住的水最高为新的数height[i]，并且将最后一部分小于height[i]的值，修改为height[i]。因为这部分已经计算过了，避免下次遇到更高的数时重复计算
	                    for(int j = vi.size()-1; height[i] > vi[j]; j--){
                        ret += height[i] - vi[j];
                        vi[j] = height[i];
                    }
                }
            }
            vi.push_back(height[i]);
        }
        return ret;
    }
	};

### 第二种

	class Solution {
	public:
	    int trap(vector<int>& height) {
	        vector<int> a;
	        vector<int> b;
	        int n = 0;
	        int t = 0;
	        int x = 0;
	        int y = 0;
	        for(int i = 0; i < height.size(); i++)
	        {
	            if(a.size() && a[0] <= height[i])
	            {
	                while(a.size() > 1)
	                {
	                    n+=a[a.size() - 1];
	                    a.pop_back();
	                    t++;
	                }
	                x += a[0] * t - n;
	                t = 0;
	                n = 0;
	                a.pop_back();
	            }
	            a.push_back(height[i]);
	            cout << a.size() << " ";
	        }
	        while(a.size() > 0)
	        {
	            b.push_back(a[a.size() - 1]);
	            a.pop_back();
	        }
	
	        for(int i = 0; i < b.size(); i++)
	        {
	            if(a.size() && a[0] <= b[i])
	            {
	                while(a.size() > 1)
	                {
	                    n+=a[a.size() - 1];
	                    a.pop_back();
	                    t++;
	                }
	                x += a[0] * t - n;
	                t = 0;
	                n = 0;
	                a.pop_back();
	            }
	            a.push_back(b[i]);    
	        }
	
	        return x;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/trapping-rain-water/submissions/](https://leetcode-cn.com/problems/trapping-rain-water/submissions/)