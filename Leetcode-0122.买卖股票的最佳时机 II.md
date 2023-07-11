# Leetcode 0122.买卖股票的最佳时机 II

---

## 原题链接：[Leetcode - 买卖股票的最佳时机 II](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/)

难度：**<span style="color:yellow">中等</span>**

---

### 题意

> 给出数组 `prices` ，第 `i` 个元素 `prices[i]` 表示股票第 `i` 天的价格
>
> 你可以在每一天决定购买/卖出股票。你在任何时候 **最多** 只能持有 **一股** 股票。你可以先购买，然后在同一天出售。
>
> 返回能得到的最大利润

### 示例

> 输入：**prices = [7,1,5,3,6,4]**
>
> 输出：**7**

> 输入：**prices = [1,2,3,4,5]**
>
> 输出：**4**

> 输入：**prices = [7,6,4,3,1]**
>
> 输出：**0**

---

## 暴力破解

<br>

因为题目并没有规定一天只能进行一次买卖，所以有利可图就买，收集所有上坡的利益。那就一个 `for` 循环可以解决。



```cpp
class Solution{
public:
  int maxProfit(vector<int>& prices) {
    int result = 0;
    for (int i = 1; i < prices.size(); i++) {
      if (prices[i] > prices[i-1]) {
        // 只要下一天的利润比今天大，那就有利可图
        result += prices[i] - prices[i-1];
      }
    }
    return result;
  }
};
```



---

## To be continued.
