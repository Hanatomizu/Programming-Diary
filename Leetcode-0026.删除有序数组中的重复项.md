# Leetcode 0026.删除有序数组中的重复项

---
### 原题链接： [Leetcode - 删除有序数组中的重复项](https://leetcode.cn/problems/remove-duplicates-from-sorted-array/)

难度：**<span style="color:lightgreen;">简单<span>**

---

#### 题意

> ###### 要求 [原地](https://baike.baidu.com/item/原地算法) 删除 **升序排列** 的数组 `nums` 中的重复出现的元素，返回删除后的数组的长度，要求数组的 **相对顺序** 一致

<br>

#### 判定标准

> ```cpp
> int[] nums = [...]; // 输入数组
> int[] expectedNums = [...]; // 长度正确的期望答案
>
> int k = removeDuplicates(nums); // 调用
>
> assert k == expectedNums.length;
> for (int i = 0; i < k; i++) {
>     assert nums[i] == expectedNums[i];
> }
> ```

<br>

#### 示例

> ###### 输入：**nums = [1, 1, 2]**
> ###### 输出：**2, nums = [1, 2]**

---

诶？看到这道题目是不是有点奇怪，为什么它会给我们这个 **判定标准** 呢？  
那是因为 C++ 中数组在内存中是连续的，所以说要删除元素，就是把下一个元素放到这个元素的空间里，题目中要求返回的值就被放到了 `k` 中，判定的时候就取到第 `k` （下标）个数字，也就是说下面还有其他值人家就不去判定了，同时是为什么要求数组的相对顺序一致了，这样题目就简单很多了。

首先考虑一种情况，就是如果输入的数组长度为 0，那么直接 `return 0` 不需要考虑

```cpp
if (nums.size() == 0)
    return 0;
```

<br>

在列表中删除元素的原理上文已经提到了，用的方法毫无疑问就是双指针法了。~~又快又简单。~~

```cpp
int slowIndex = 0;
for (int fastIndex = 1; fastIndex < nums.size(); fastIndex++){
    /* code... */
}
```
<br>

如果快指针和慢指针指向的值是一样的，那就说明有重复的值出现了。  
这时候慢指针不动，快指针继续前进，直到两个指针所指向的值不同时，把快指针指向的值往前面移动

```cpp
if(nums[slowIndex] != nums[fastIndex]){
    // 把快指针的值赋予给慢指针的下一个，不然的话慢指针指向的值就被彻底删除了。
    nums[++slowIndex] = nums[fastIndex];
}
```
<br>

慢指针走完了就是数组最后，所以慢指针最后指向的就是最后一位数字的下标，那下标直接返回去可以吗？答案是否定的。因为下标是从 0 开始的，所以返回的是 `slowIndex+1`

```cpp
return slowIndex+1;
```

<br>

总体代码如下：

```cpp
class Solution{
public:
    int removeDuplicates(vector<int>& nums){
        // 如果长度为 0，直接返回 0
        if(nums.size() == 0)
            return 0;
        // 定义慢指针
        int slowIndex = 0;
        // 快指针一定要是 1，否则可能会出现一些神奇的 bug
        for(int fastIndex = 1; fastIndex < nums.size(); fastIndex++){
            // 如果两个值相等，快指针前进，慢指针不动
            // 不相等时把快指针所指的值向前移动
            if(nums[slowIndex] != nums[fastIndex])
                nums[++slowIndex] = nums[fastIndex];
        }
        // 因为下标是从 0 开始的，所以返回时要 +1
        return slowIndex + 1;
    }
};
```

---

#### 分析小结

- 本题考查对 **双指针** 和 **数组** 的掌握情况。

---

### Thanks for Reading!