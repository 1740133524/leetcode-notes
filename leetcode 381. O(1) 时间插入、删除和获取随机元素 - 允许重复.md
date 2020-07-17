# 381. O(1) 时间插入、删除和获取随机元素 - 允许重复

## 题目

设计一个支持在平均 时间复杂度 O(1) 下， 执行以下操作的数据结构。

注意: 允许出现重复元素。

* insert(val)：向集合中插入元素 val。
* remove(val)：当 val 存在时，从集合中移除一个 val。
* getRandom：从现有集合中随机获取一个元素。每个元素被返回的概率应该与其在集合中的数量呈线性相关。

## 示例

	// 初始化一个空的集合。
	RandomizedCollection collection = new RandomizedCollection();
	
	// 向集合中插入 1 。返回 true 表示集合不包含 1 。
	collection.insert(1);
	
	// 向集合中插入另一个 1 。返回 false 表示集合包含 1 。集合现在包含 [1,1] 。
	collection.insert(1);
	
	// 向集合中插入 2 ，返回 true 。集合现在包含 [1,1,2] 。
	collection.insert(2);
	
	// getRandom 应当有 2/3 的概率返回 1 ，1/3 的概率返回 2 。
	collection.getRandom();
	
	// 从集合中删除 1 ，返回 true 。集合现在包含 [1,2] 。
	collection.remove(1);
	
	// getRandom 应有相同概率返回 1 和 2 。
	collection.getRandom();

## 分析

使用 `vector<int> v` 来存储插入的元素

使用 `unordered_map<int, unordered_set<int>> m` 来存储每个值对应的v中的位置

删除的时候通过 m 找到 val 对应的元素位置，将此元素和 v 中最后一个元素互换，pop最后一个元素。要记得删除 m 中 val 对应的元素，并且更新 m 中 v 的最后一个元素的位置

## 代码
	
	class RandomizedCollection {
	private:
	    unordered_map<int, unordered_set<int>> m;
	    vector<int> v;
	public:
	    /** Initialize your data structure here. */
	    RandomizedCollection() {
	    }
	    
	    /** Inserts a value to the collection. Returns true if the collection did not already contain the specified element. */
	    bool insert(int val) {
	        v.push_back(val);
	        m[val].insert(v.size()-1);
	        if(m[val].size() > 1) return false;
	        else return true;
	    }
	    
	    /** Removes a value from the collection. Returns true if the collection contained the specified element. */
	    bool remove(int val) {
	        if(m[val].size() > 0){
	            int z = *(m[val].begin());
	            m[val].erase(m[val].begin());
	            v[z] = v[v.size()-1];
	            // 得先添加再删除，不然如果删除的正好是同一个数并且同时是m中的最后一个数，有一次删除会无效
	            m[v[v.size()-1]].insert(z);
	            m[v[v.size()-1]].erase(v.size()-1);
	            v.pop_back();
	            return true;
	        }
	        else return false;
	    }
	    
	    /** Get a random element from the collection. */
	    int getRandom() {
	        if(v.size() == 0) return -1;
	        return v[rand() % v.size()];
	    }
	};
	
	/**
	 * Your RandomizedCollection object will be instantiated and called as such:
	 * RandomizedCollection* obj = new RandomizedCollection();
	 * bool param_1 = obj->insert(val);
	 * bool param_2 = obj->remove(val);
	 * int param_3 = obj->getRandom();
	 */

> 题目网址：[https://leetcode-cn.com/problems/insert-delete-getrandom-o1-duplicates-allowed/](https://leetcode-cn.com/problems/insert-delete-getrandom-o1-duplicates-allowed/)