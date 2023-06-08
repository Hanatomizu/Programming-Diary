# Leetcode 0002.两数相加

---
### 原题链接： [Leetcode - 两数相加](https://leetcode.cn/problems/add-two-numbers/)  

Leetcode 题库第二道题目  
难度：`中等`


##### 这篇的语言表述还是不太清楚，不久会修改的。
---

#### 题意

> ###### 把两个逆序的链表的值加起来，每个节点只能存储一位数字，然后以相同的方式返回。  

#### 示例

> ###### 输入：`l1 = [2,4,3], l2 = [5,6,4]`  
> ###### 输出：`[7,0,8]`  

---

好了，看到这个题目，就知道考的是链表了，官方呢也是非常贴心地提供了 `ListNode* l1, ListNode* l2` 以及定义方式。

要相加两个链表的和，就要先遍历一遍列表，并且记录每一个节点的进位并储存到 `carry`，就像小学数学一样。$\downarrow$ ~~完全不恰当的比喻~~

$$
\begin{matrix*}
    &4 & 8 \\
    +&1 & 9 \\ \hline
    &6 & 7
\end{matrix*}
$$

好了，遍历链表后需要新的链表来储存数据，那就先定义好吧。

```cpp
ListNode *head = nullptr, *cur = nullptr; // 先设置为空指针，等下再赋值
int carry = 0; // 设置进位，默认为 0
```

<br>

因为链表不能使用 `size()` 之类的来求长度，所以知道循环多少次，那么使用 `while` 来进行循环操作。

```cpp
// 如果 l1 或者 l2 任何一个指向的地址还有值，那就继续循环
while (l1 || l2){
    /* code... */
}
```

<br>

然后把两个链表里的值和进位都储存下来。
```cpp
int num1 = l1 ? l1->val : 0; // 一个简单的三目运算，如果 l1 还有，那就设置为 l1->val，没有就设置为 0
int num2 = l2 ? l2->val : 0; // 同理
```

<br>

接着进行相加操作。

```cpp
int sum = num1 + num2 + carry; // 别忘了进位哦
```

<br>

还记得之前定义的列表吗？在数据输入之前需要检查链表是否为空，也就是 `head` 是否仍然等于 `nullptr`。  
如果是，那就给 `head` 和 `cur` 都赋为第一个和，否则只给 `cur` 赋予和。  
这个和就是 `sum`，但是仔细看题目， 题目中标出 `每一个节点只能储存 一位 数字`，那么要赋值的时候就需要判断 `sum` 是不是两位数字了，这里只需要取模 $($`sum % 10`$)$ 就行了。

```cpp
if (head == nullptr){
    head = cur = new ListNode(sum % 10);
} else {
    cur = new ListNode(sum % 10);
    cur = cur -> next; // 到下一个地址
}
```

<br>

然后重置进位。

```cpp
carry = sum /10;
```

<br>

接下来就是两个链表遍历了。
```cpp
if (l1)
    l1 = l1 -> next; // 如果 l1 还有数，那么就到下一个指针，如果没有就不作处理了
if (l2)
    l2 = l2 -> next; // 同理
```

<br>

那么总体的循环体代码如下：
```cpp
while(l1 || l2){
    // 定义变量储存两个链表指向的值
    int num1 = l1 ? l1->val : 0;
    int num2 = l2 ? l2->val : 0;
    // 储存和
    int sum = num1 + num2 + carry;
    // 判断是否初始化结果链表
    if (head == nullptr){
        head = cur = new ListNode(sum % 10);
    } else {
        cur->next = new ListNode(sum % 10);
        cur = cur -> next;
    }
    // 重置进位
    carry = sum /10;
    // 遍历
    if (l1){
        l1 = l1 -> next;
    }
    if (l2) {
        l2 = l2 -> next;
    }
}
```

<br>

以上为循环体的代码，仔细看一下，然后思考一下有没有一种可能，我是说可能$($~~废话~~$)$，最后一位会不会还有进位呢？  
也就是退出循环的时候会不会出现 $carry \not ={0}$ 的情况呢？

所以在循环体外面再加一层判断：
```cpp
if (carry > 0)
    cur->next = new ListNode(carry);
```

现在想想算法部分是不是完成了？  
没错，确实完成了。

最后把储存结果的链表的头返回去就 OK 了
```cpp
return head;
```

---

##### 总体代码如下：
```cpp
class Solution{
    ListNode* addTwoNumbers(ListNode *l1, ListNode *l2){
        ListNode *head = nullptr, *cur = nullptr; // 定义储存结果的链表
        int carry = 0; // 定义进位变量，默认为 0
        while(l1 || l2){
            // 定义变量储存两个链表指向的值
            int num1 = l1 ? l1->val : 0;
            int num2 = l2 ? l2->val : 0;
            // 储存和
            int sum = num1 + num2 + carry;
            // 判断是否初始化结果链表
            if (head == nullptr){
                head = cur = new ListNode(sum % 10);
            } else {
                cur->next = new ListNode(sum % 10);
                cur = cur -> next;
            }
            // 重置进位
            carry = sum /10;
            // 遍历
            if (l1){
                l1 = l1 -> next;
            }
            if (l2) {
                l2 = l2 -> next;
            }
        }

        // 判断是否最后还有没有进位的数
        if (carry > 0)
            cur->next = new ListNode(carry);
        // 返回结果
        return head;
    }
};
```

---

#### 分析小结

这个题目考查的是对链表的遍历和运算，还有高精度，难度不算很高，但是题目第一眼确实很那难懂，多读几遍是可以理解的。

---

## Thanks for Reading.