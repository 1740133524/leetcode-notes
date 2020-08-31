# 1157. 子数组中占绝大多数的元素

## 题目

实现一个 MajorityChecker 的类，它应该具有下述几个 API：

* MajorityChecker(int[] arr) 会用给定的数组 arr 来构造一个 MajorityChecker 的实例。
* int query(int left, int right, int threshold) 有这么几个参数：
	* 0 <= left <= right < arr.length 表示数组 arr 的子数组的长度。
   	* 2 * threshold > right - left + 1，也就是说阈值 threshold 始终比子序列长度的一半还要大。

每次查询 query(...) 会返回在 arr[left], arr[left+1], ..., arr[right] 中至少出现阈值次数 threshold 的元素，如果不存在这样的元素，就返回 -1。

## 示例

MajorityChecker majorityChecker = new MajorityChecker([1,1,2,2,1,1]);
majorityChecker.query(0,5,4); // 返回 1
majorityChecker.query(0,3,3); // 返回 -1
majorityChecker.query(2,3,2); // 返回 2

## 提示

* 1 <= arr.length <= 20000
* 1 <= arr[i] <= 20000
* 对于每次查询，0 <= left <= right < len(arr)
* 对于每次查询，2 * threshold > right - left + 1
* 查询次数最多为 10000

## 分析

当数据量小的时候，暴力搜索（可以不需要），数据量大的时候，为每个数字建立一个数组，存储出现时的下标，根据left和right确定有多少个该数字，满足直接返回，否则返回-1。

在判断时如果遇到 threshold 大于最多的数字的数量直接返回-1

## 代码
	
	class MajorityChecker {
	unordered_map<int, vector<int>> m;
	vector<int> v;
	int ma;
	public:
	    MajorityChecker(vector<int>& arr) {
	        v = arr;
	        ma = 0;
	        for(int i = 0; i < arr.size(); i++){
	            m[arr[i]].push_back(i);
	            if(m[arr[i]].size() > ma) ma = m[arr[i]].size();
	        } 
	        
	    }
	    int query(int left, int right, int threshold) {
	        if(ma < threshold) return -1;
	        if(right - left < 50){
	            unordered_map<int, int> m1;
	            for(int i = left; i <= right; i++){
	                m1[v[i]]++;
	            }
	
	            for(auto a = m1.begin(); a != m1.end(); a++){
	                if(a->second >= threshold){
	                    return a->first;
	                }
	            }
	            return -1;
	        }
	        for(auto a = m.begin(); a != m.end(); a++){
	            auto as = a->second;
	            int l = 0;
	            int r = as.size()-1;
	            while(l < r){
	                int m = (l+r)/2;
	                if(as[m] < left) l = m+1;
	                else r = m;
	            }
	            if(!(as[l] >= left && as[l] <= right)) continue;
	            int l1 = l;
	            r = as.size()-1;
	            while(l < r){
	                int m = (l+r+1)/2;
	                if(as[m] > right) r = m-1;
	                else l = m;
	            }
	            if(l - l1 + 1 >= threshold){
	                return a->first;
	            }
	        }
	        return -1;
	    }
	};
	
	/**
	 * Your MajorityChecker object will be instantiated and called as such:
	 * MajorityChecker* obj = new MajorityChecker(arr);
	 * int param_1 = obj->query(left,right,threshold);
	 */

> 题目网址：[https://leetcode-cn.com/problems/online-majority-element-in-subarray/](https://leetcode-cn.com/problems/online-majority-element-in-subarray/)