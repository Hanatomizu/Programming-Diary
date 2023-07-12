# Luogu B2030.计算线段长度

---

## 原题链接： [洛谷 - 计算线段长度](https://www.luogu.com.cn/problem/B2030)

### 题意

> 已知线段的两个端点的坐标 $A(x_{a}, y_{a})$ ，$B(x_{a} ,y_{b})$ ，求线段 AB 的长度。

### 输入格式

> 输入共两行。  
> 第一行是两个实数 $x_{a}$ ，$y_{a}$ ，即 $A$ 的坐标。  
> 第二行是两个实数 $x_{b}$ ，$y_{b}$ ，即 $B$ 的坐标。  
> 输入中所有实数的绝对值均不超过 $10000$ 。  

### 输出格式

> 输出一个实数，即线段 $AB$ 长度，保留小数点后 $3$ 位。

### 示例

> 输入： $1 & 1 \\ 1 & 1$ 
>
> 输出： $1.414$ 

---

## 解题思路与方法

洛谷上的题目很多都是数学方面的，这题很明显就是。

在坐标轴中计算线段长度一般用**勾股定理**（即： $a^{2} + b^{2} = c^{2}$ ）。

首先定义变量储存四个值，然后输入。

```cpp
double xa = 0, ya = 0, xb = 0, yb = 0;
scanf("%lf %lf\n%lf %lf", &xa, &ya, &xb, &yb);
/*
	这里也可以使用 cin 来输入，写法如下：
	std::cin >> xa >> ya >> xb >> yb;
*/
```

<br>

然后用勾股定理求出长度。数学表达式： $\sqrt{(x_{a} - x_{b})^{2} + (y_{a} - y_{b})^{2}}$ 

代码如下：

```cpp
double distance = sqrt(pow(xa - xb, 2) + pow(ya - yb, 2));
```

<br>

最后，题目要求格式输出，这里选择 `printf();` 。

```cpp
printf("%.3lf", distance);
```

<br>


### 总体代码如下

```cpp
#include <iostream>
#include <cmath>
using namespace std;

int main(){
    double xa = 0, xb = 0, ya = 0, yb = 0;
    scanf("%lf %lf\n%lf %lf", &xa, &ya, &xb, &yb);
    double distance = sqrt(pow(xa - xb, 2) + pow(ya - yb, 2));
    printf("%.3lf", distance);
    return 0;
}
```

---

## 分析小结

- 这个题目主要考察数学思维，用到的几何知识有勾股定理。

---

## Thanks for Reading