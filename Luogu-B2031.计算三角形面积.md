# Luogu B2031.计算三角形面积

---
## 原题链接：[洛谷 - 计算三角形面积](https://www.luogu.com.cn/problem/B2031)

难度：<span style="color:red;">**入门**</span>

---
### 题意

> 给出一个三角形顶点坐标分别为 $(x1, y1)$ $(x2, y2)$ $(x3, y3)$ ，求该三角形面积

### 输入格式

> 输入一行双精度浮点数，分别对应 $x1$ , $y1$ , $x2$ , $y2$ , $x3$ , $y3$ .

### 输出格式

> 输出一行，输出三角形面积，要求精确到小数点后两位

### 示例

> 输入：**0 0 4 0 0 3**  
> 输出：**6.00**

<br>

---

## 解题思路与方法

这就是简单的一道数学题了，然后用编程的方法解。

很明显，这道题目应该用 [海伦公式](https://baike.baidu.com/item/%E6%B5%B7%E4%BC%A6%E5%85%AC%E5%BC%8F/106956) 来解。

海伦公式需要知道三条边的长度，可以使用 [勾股定理](https://baike.baidu.com/item/%E5%8B%BE%E8%82%A1%E5%AE%9A%E7%90%86/91499) 来取得。

$$
a^2 + b^2 = c^2
\\
勾股定理
$$

定义变量储存三角形的顶点坐标并输入值

```cpp
double x1 = 0, x2 = 0, x3 = 0, y1 = 0, y2 = 0, y3 = 0;
cin >> x1 >> y1 >> x2 >> y2 >> x3 >> y3; // 也可以用 scanf();
```

由题意得 $a = x1 - x2$ , $b = y1 - y2$ ，以此类推剩下两条边的长度，得到以下代码：

```cpp
/* 需要导入 cmath 库 */
double dis_a = sqrt(pow(x1 - x2, 2) + pow(y1 - y2, 2)); // a 边长度
double dis_b = sqrt(pow(x2 - x3, 2) + pow(y2 - y3, 2)); // b 边长度
double dis_c = sqrt(pow(x1 - x3, 2) + pow(y1 - y3, 2)); // c 边长度
```

然后是海伦公式进行运算。

$$
S = \sqrt{p(p - a)(p - b)(p - c)}
\\
p = \frac{a + b + c}{2}
$$

得到代码：

```cpp
double p = (dis_a + dis_b + dis_c) / 2;
double s = sqrt(p * (p - dis_a) * (p - dis_b) * (p - dis_c));
```

最后，格式输出：

```cpp
printf("%.2lf", S);
```

<br>

总体代码如下：

```cpp
#include <iostream>
#include <cmath>
using namespace std;

int main(){
	double x1 = 0, x2 = 0, x3 = 0, y1 = 0, y2 = 0, y3 = 0;
	cin >> x1 >> y1 >> x2 >> y2 >> x3 >> y3;
	double dis_a = sqrt(pow(x1 - x2, 2) + pow(y1 - y2, 2));
	double dis_b = sqrt(pow(x2 - x3, 2) + pow(y2 - y3, 2));
	double dis_c = sqrt(pow(x1 - x3, 2) + pow(y1 - y3, 2));
	double p = (dis_a + dis_c + dis_b) / 2;
	double s = sqrt(p * (p - dis_a) * (p - dis_b) * (p - dis_c));
	printf("%.2lf", s);
	return 0;
}
```

<br>

---
## 分析小结

本题主要看数学思维，编程方面看对 cmath 函数库的熟练程度。

<br>

---

## Thanks for Reading