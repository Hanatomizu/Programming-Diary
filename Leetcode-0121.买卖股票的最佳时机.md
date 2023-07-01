# Leetcode 0121.买卖股票的最佳时机

---

### 原题链接：[Leetcode - 买卖股票的最佳时机](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock/)

难度：**<span style="color:lightgreen;">简单</span>**

---

#### 题意

> 给出数组 `prices` ，第 `i` 个元素 `prices[i]` 表示股票第 `i` 天的价格
>
> 只能在某一天买入这只股票，并在未来的某一天卖出。
>
> 求这笔交易中的最大利润



#### 示例

> 输入：**[7,1,5,3,6,4]**
>
> 输出：**5**

---

这题很明显要求找出数组中的两个数字，并使它们的差最大。

$$
\begin{matrix}
股票价格&7&1&5&3&6&4
\\
每日盈亏&/&-6&4&-2&3&-2
\end{matrix}
$$

返回的是最大利润，也就是这个最大值，所以不需要找出具体的数字，只需要定义一个变量储存这个值就可以了。

```cpp
int result = 0;
```

<br>

然后就是需要不断寻找使 `result` 的值最大。先定义变量把股票最小的价格储存起来。

```cpp
int min_price = INT32_MAX;
```

<br>

接着就可以遍历数组寻找最大值了。

```cpp
for (int i = 0; i < prices.size(); i++) {
  /* code */
  /* ... */
}
```

<br>

不断比较寻找最小值。

```cpp
min_price = min(min_price, prices[i]);
```

<br>

有了最小值就可以进行比较了，因为比较出来的结果可能不是最赚钱的，所以先临时储存一下。

```cpp
int temp_sub = prices[i] - min_price;
```

<br>

有了临时的结果，那么就继续比较是不是比 `result` 的结果更大，如果是，则将 `temp_sub` 的值赋予给 `result`。

```cpp
result = max(result, temp_sub);
```

<br>

以上代码功能已经实现，只需要 `return` 结果就可以了。

---

#### 总体代码如下

```cpp
class Solution{
public:
  int maxProfit(vector<int>& prices) {
    int result = 0; // 储存结果，如果不能盈利则返回 0
    int min_price = INT32_MAX; // 最小价格默认最大，然后遍历时寻找
    for (int i = 0; i < prices.size(); i++) { // 遍历寻找最小价格，并进行处理
      min_price = min(min_price, prices[i]); // 寻找最小价格
      int temp_sub = prices[i] - min_price; // 计算 prices[i] 和最小价格的差，即赚到的钱
      result = max(result, temp_sub); // 如果临时的盈利大于全局盈利，那就把全局盈利设置为总盈利
    }
    return result;
  }
};
```

---

#### 总结

简单的动态规划吧。

---

## Thanks for Reading
