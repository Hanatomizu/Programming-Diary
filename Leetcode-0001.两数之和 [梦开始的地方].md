# 梦开始的地方 LeetCode 0001.两数之和

---

##### 原题链接：[两数之和-Leetcode](https://leetcode.cn/problems/two-sum/)

这是我在 Leetcode 上做的第一道题目，梦想开始的地方。

---
##### 原题目如下
- 给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出 和为目标值 `target`  的那 两个 整数，并返回它们的数组下标。

- 你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

- 你可以按任意顺序返回答案。


---
##### 最简单的解法也就是最暴力的最直接的解法，直接双重循环暴力寻找。

第一重循环寻找第一个数字。

```cpp
for(int i = 0; i < nums.size(); i++)
```

然后是第二层循环，因为结果只有两个，只需要2层循环就够了。

```cpp
for(int j = i+1; j < nums.size(); j++)
```

最后加上一个 if 判定和是否等于 `target`，接着直接 `return` 回去.
```cpp
if(nums[i] + nums[j] == target){
    return vector<int>{i, j};
}
```

如果没有的答案的话是在循环结束的时候还没有 `return` ，这时候就 `return` 一个空的向量回去。
```cpp
return vector<int> {};
```

总体代码如下：

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        for(int i = 0; i < nums.size(); i++){
            for(int j = i+1; j < nums.size(); j++){
                if(nums[i] + nums[j] == target){
                    return vector<int> {i,j};
                }
            }
        }
        return vector<int> {};
    }
};
```
时间复杂度：`O(N^2)`  
空间复杂度：`O(1)`


---

看到这个代码似乎有点太慢了吧，那么能不能把时间复杂度控制在 `O(n^2)` 之内呢？

重新整理思路，我们需要做的是什么？是枚举一个 `x` 然后寻找另外一个值等于 `target`。那么就可以把要寻找的值看作 `target - x`，枚举可以直接使用 `for` 解决，问题就剩下要寻找一个值为 `target - x`。
那么，哈希表似乎是一个不错的选择。

题目标出 `你可以按任意顺序返回答案。`， 那么 key 可以是无序的，选择 `std::unordered_map` 效率将会更高。

在哈希表中，储存结构为 `{key: 数据, value: 对应的下表}`。

```cpp
class Solution{
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        std::unordered_map <int, int> table;
        for(int i = 0; i< nums.size(); i++){
            // 遍历，看看在 table 中是否有匹配的值
            auto iter = table.find(target - nums[i]);
            if (iter != table.end()){
                // 有则直接返回
                return vector<int> {iter->second, i};
            }
            // 如果没有匹配上，就把访问过的元素和下标加入到 table 中
            table.insert(pair<int, int> {nums[i], i});
        }
        return vector<int> {};
    }
};

```

时间复杂度：`O(n)`
空间复杂度：`O(n)`

---

##### 分析小结

- 暴力破解不作分析。

1. 本题目中因为需要快速寻找一个值 `target - x`， 所以选择哈希表会更加快。
2. 题目中标出不需要按照顺序输出，所以使用 `std::unordered_map` 会更加快一点。
3. 本题中 `table` 用来存储我们访问过的元素，然后在这些元素里寻找 `target - x`。
4. 在 `table` 中 `key` 用来存储值， `value` 用来存储下标。
   

---
## Thanks for reading.
