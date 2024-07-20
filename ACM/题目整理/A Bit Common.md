#学习 #acm 
# 英文
## 题目描述

- Given two integers $n$ and $m$, among all the sequences containing $n$ non-negative integers less than $2^m$, you need to count the number of such sequences $A$ that there exists a non-empty subsequence of $A$ in which the bitwise AND of the integers is 1.

- Note that a non-empty subsequence of a sequence $A$ is a non-empty sequence that can be obtained by deleting zero or more elements from $A$ and arranging the remaining elements in their original order.

Since the answer may be very large, output it modulo a positive integer $q$.

The bitwise AND of two non-negative integers $A$ and $B$ is defined as follows:
- When $A$ and $B$ is written in base two, the digit in the $2^k$ place ($k \geq 0$) is 1 if those of $A$ and $B$ are both 1, 0 otherwise.

For example, we have $4 \text{ AND } 6 = 4$ (in base two: 100 AND 110 = 100).

Generally, the bitwise AND of $k$ non-negative integers $p_1, p_2, \ldots, p_k$ is defined as
$$
\ldots ((p_1 \text{ AND } p_2) \text{ AND } p_3) \ldots \text{ AND } p_k
$$
and we can prove that this value does not depend on the order of $p_1, p_2, \ldots, p_k$.

### 输入描述

The only line contains three integers $n$ ($1 \leq n \leq 5000$), $m$ ($1 \leq m \leq 5000$) and $q$ ($1 \leq q \leq 10^9$).

### 输出描述

Output a line containing an integer, denoting the answer.

### 示例 1

输入:
```
2 3 998244353
```

输出:
```
17
```

### 示例 2

输入:
```
5000 5000 998244353
```

输出:
```
2274146
```
# 中文

## 题目描述

- 给定两个整数 $n$ 和 $m$，在所有包含 $n$ 个小于 $2^m$ 的非负整数的序列中，你需要计算存在一个非空子序列 $A$ 的序列的数量，其中 $A$ 的整数的按位与为 1。

- 注意，序列 $A$ 的非空子序列是可以通过删除 $A$ 的零个或多个元素并按原顺序排列剩余元素得到的非空序列。

由于答案可能非常大，输出对正整数 $q$ 取模的结果。

两个非负整数 $A$ 和 $B$ 的按位与定义如下：
- 当 $A$ 和 $B$ 以二进制表示时，如果 $A$ 和 $B$ 在 $2^k$ 位（ $k \geq 0$ ）上的数字均为 1，则该位为 1，否则为 0。

例如，我们有 $4 \text{ AND } 6 = 4$ （以二进制表示：100 AND 110 = 100）。

一般来说，$k$ 个非负整数 $p_1, p_2, \ldots, p_k$ 的按位与定义为
$$
\ldots ((p_1 \text{ AND } p_2) \text{ AND } p_3) \ldots \text{ AND } p_k
$$
我们可以证明这个值与 $p_1, p_2, \ldots, p_k$ 的顺序无关。

### 输入描述

唯一一行包含三个整数 $n$ ($1 \leq n \leq 5000$), $m$ ($1 \leq m \leq 5000$) 和 $q$ ($1 \leq q \leq 10^9$).

### 输出描述

输出一行整数，表示答案。

### 示例 1
#### 输入:
 ```
 2 3 998244353
 ```

#### 输出:
```
17
```
### 示例 2

#### 输入:
```
5000 5000 998244353
```
#### 输出:
```
2274146
```