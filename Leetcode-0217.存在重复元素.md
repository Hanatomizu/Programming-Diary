# Leetcode 0217.存在重复元素
---

## 原题链接：[Leetcode - 存在重复元素](https://leetcode.cn/problems/contains-duplicate/)

难度：**<span style="color:green;">简单</span>**

---

### 题意

> 给你一个整数数组 `nums` 。如果任一值在数组中出现 `至少` 两次 ，返回 `true` ；如果数组中每个元素互不相同，返回 `false` 。

### 示例

> 输入：**nums = [1,2,3,1]**
> 输出：**true**

<br>

---

## 排序

<br>

### 解题思路和方法

在排序的时候，重复的数据将被排在一起，并且题目说明只需要一个数值出现 $2$ 次即可，所以只需要排序后比对前后的数值是否相同即可。

这里直接快速排序。

```cpp
std::sort(nums.begin(), nums.end());
```

<br>

然后遍历列表并检查数值是否相同。

```cpp
for (int i = 1; i < nums.size(); i++) {
	if (nums[i-1] == nums[i])
		return true;
}
```

---
### 总体代码如下

```cpp
class Solution {
public:
	bool containsDuplicate(vector<int>& nums) {
		// 直接使用 std::sort 排序
		std::sort(nums.begin(), nums.end());
		// i 选用 1 减小一点点时间（真的就一点点）
		for (int i = 1; i < nums.size(); i++) {
		if (nums[i-1] == nums[i])
			return true;
		}
	}
};
```

时间复杂度： $O(N \log N)$ 

空间复杂度： $O(\log N)$ 

---

<br>

## 哈希表

<br>

### 解题思路和方法

遍历数组，并且把遍历过的值扔进哈希表，若发现相同，则直接 `return true`。

先声明一个哈希表 `map`，因为只需要判定在与否，所以可以用无序哈希表。

```cpp
std::unordered_set<int> map;
```

<br>

然后进行遍历。

```cpp
for (int i = 0; i < nums.size(); i++) {
	/* code */
}
```

<br>

接着判定 `nums[i]` 是否在 `map` 中，若在里面，直接 `return true` ，否则将 `nums[i]` 插入 `map`，然后进入下一层循环。

```cpp
if (map.find(nums[i]) != map.end())
	return true; 
map.insert(nums[i]);
```

<br>

最后，若没有找到，返回 `false` 。

```cpp
for (int i = 0; i < nums.size(); i++) {
	/* code */
}
return false;
```

---

### 总体代码如下

```cpp
class Solution {
public:
	bool containsDuplicate(vector<int>& nums) {
		std::unordered_set<int> map;
		for (int i = 0; i < nums.size(); i++){
			if(map.find(nums[i]) != map.end()) 
				return true;
			map.insert(nums[i]);
		}
		return false;
	}
};
```

时间复杂度： $O(N)$ 

空间复杂度： $O(N)$ 

<br>

---

# Thanks for Reading
