# 765. 情侣牵手

## 题目

N 对情侣坐在连续排列的 2N 个座位上，想要牵到对方的手。 计算最少交换座位的次数，以便每对情侣可以并肩坐在一起。 一次交换可选择任意两人，让他们站起来交换座位。

人和座位用 0 到 2N-1 的整数表示，情侣们按顺序编号，第一对是 (0, 1)，第二对是 (2, 3)，以此类推，最后一对是 (2N-2, 2N-1)。

这些情侣的初始座位  row[i] 是由最初始坐在第 i 个座位上的人决定的。

## 示例

示例 1:
	
	输入: row = [0, 2, 1, 3]
	输出: 1
	解释: 我们只需要交换row[1]和row[2]的位置即可。

示例 2:

	输入: row = [3, 2, 0, 1]
	输出: 0
	解释: 无需交换座位，所有的情侣都已经可以手牵手了。

## 说明:

* len(row) 是偶数且数值在 [4, 60]范围内。
* 可以保证row 是序列 0...len(row)-1 的一个全排列。

## 分析

将每一对沙发看做一个节点，在两者不是情侣的情况下要么换第一个人，要么换第二个人。将需要交换的沙发用无向边连起来，可以看到每个节点的度要么为0，要么为2。目标就是将每个节点的度变为0，可以发现不管怎么交换，一次交换也只能多出1个度为0的结点。所以可以使用贪心直接寻找另一半。直接查找时间复杂度为O(n^2)，可以使用map存储每个人的位置使复杂度降为O(n)。

> 参考：https://leetcode-cn.com/problems/couples-holding-hands/solution/qing-lu-qian-shou-by-leetcode/

## 代码
	
	class Solution {
	public:
	    int minSwapsCouples(vector<int>& row) {
	        vector<int> m(row.size(), 0);
	        int ret = 0;
	        for(int i = 0; i < row.size(); i++) m[row[i]] = i;
	        for(int i = 0; i < row.size(); i+=2){
	            int z = row[i] % 2 == 0 ? row[i]+1 : row[i]-1;
	            if(row[i+1] != z){
	                m[row[i+1]] = m[z];
	                m[z] = i+1;
	                row[m[row[i+1]]] = row[i+1];
	                row[m[z]] = z;
	                ret++;
	            }
	        }
	        return ret;
	    }
	};

> 题目网址：[https://leetcode-cn.com/problems/couples-holding-hands/](https://leetcode-cn.com/problems/couples-holding-hands/)