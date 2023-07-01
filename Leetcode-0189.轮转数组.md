# Leetcode 0189.轮转数组

---

### 原题链接：[Leetcode - 轮转数组](https://leetcode.cn/problems/rotate-array/)

难度：<span style="color:yellow;">中等</span>

---

### 题意

> 给定一个整数数组 `nums`，将数组中的元素向右轮转 `k` 个位置，其中 `k` 是非负数。

### 示例

> 输入：**nums = [1,2,3,4,5,6,7], k = 3**
> 输出：**[5,6,7,1,2,3,4]**

---

### 临时数组法

#### 原理：定义数组 `temp` 来储存轮转后的数组

毋庸置疑地定义一个数组 `temp` 来储存，因为数组不需要添加或删除值，新的数组和 `nums` 相等，即 `nums.size()`。

```cpp
vector<int> temp(nums.size())
```

<br>

然后遍历数组。

```cpp
for (int i = 0; i < nums.size(); i++) {
	/* code */
}
```

<br>

接着就是把数组进行轮回并且放入 `temp` 中。  
这里就是有点讲究了，我应该怎么放？如果我直接 `temp[i + k] = nums[i]` 的话会怎么样呢？ 那么最后的 $k$ 个数字就无法被读取，然后在 Leetcode 上被报堆内存溢出，并且前 $k$ 个数字也被舍弃。  
这里选择 $i + k \mod nums.size()$ 来把前面的 $k$ 个数取回来。~~非常聪明的写法~~

```cpp
temp[(i + k) % nums.size()] = nums[i];
```

<br>

最后到循环外面把数组替换就可以了

```cpp
nums.assign(temp.begin(), temp.end());
```

<br>

#### 总体代码如下

```cpp
class Solution{
public:
	void rotate(vector<int>& nums, int k) {
		vector<int> temp(nums.size()); // 一定要声明长度
		for (int i = 0; i < nums.size(); i++) {
			// 需要把前 k 个数字拿回来
			temp[(i + k) % nums.size()] = nums[i];
		}
		nums.assign(temp.begin(), temp.end());
	}
};
```

---

### To be continued.