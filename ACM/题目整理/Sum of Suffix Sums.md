---
Created Time: 星期三, 七月 17日 2024, 9:03:46 上午
Title: Sum of Suffix Sums
aliases: ["**目录 Content**"]
linter-yaml-title-alias: "**目录 Content**"
Last Update: 星期三, 七月 17日 2024, 9:05:06 上午
---



#学习 #acm

# 英文
## **题目描述及要求:**
- Given an array which is initially empty, you need to perform q operations:
- Given two non-negative integers t and k, take out the element from the end of the array for t times and then append k to the end of the array. It is guaranteed that t does not exceed the length of the array before this operation.

- Operation specification: b[i], c[i] ..., d[i], e[i], be the current array, find the sum of b[j] + c[j] + ... + e[i] + d[i] + ... + e[i], where j = d[i] + e[i] + ... + i, the sum of the suffix starting from position i.

- Since the answers may be very large, output them modulo 1,000,000,007.

### **输入描述:**

```
The first line contains an integer q (1 ≤ q ≤ 5 * 10^4), denoting the number of operations.

Each of the following q lines contains two non-negative integers t and k (0 ≤ t ≤ 10^9), describing an operation, where t does not exceed the length of the array before this operation.
```

### **输出描述:**

```
Output q lines, each of which contains an integer, denoting the answer.
```

### **示例:**

#### Input

```
5
0 1
0 2
1 3
0 1
2 100000
```

#### Output

```
1
5
7
25
200001
```

#### Explanation
- After the first operation, the current array is [1], the suffix sum array is [1], and the sum of the suffix sums is 1.
- After the second operation, the current array is [1, 2], the suffix sum array is [3, 2], and the sum of the suffix sums is 5.
- After the third operation, the current array is [3], the suffix sum array is [3], and the sum of the suffix sums is 7.
- After the fourth operation, the current array is [3, 1], the suffix sum array is [4, 1], and the sum of the suffix sums is 25.
- After the fifth operation, the current array is [100000], the suffix sum array is [100000], and the sum of the suffix sums is 200001.

### **示例 2:**

#### Input

```
1
0 1000000000
```

#### Output

```
1000000000
```

---
# 中文
## **题目描述及要求:**
- 给定一个初始为空的数组，你需要执行 q 次操作：
- 给定两个非负整数 t 和 k，从数组末尾取出 t 次元素，然后将 k 追加到数组的末尾。保证 t 不超过此操作前数组的长度。

- 操作规格：b[i], c[i] ..., d[i], e[i] 为当前数组，找出 b[j] + c[j] + ... + e[i] + d[i] + ... + e[i] 的和，其中 j = d[i] + e[i] + ... + i，从位置 i 开始的后缀和。

- 由于答案可能非常大，输出结果取模 1,000,000,007。

### **输入描述:**

```
第一行包含一个整数 q（1 ≤ q ≤ 5 * 10^4），表示操作次数。

接下来的 q 行每行包含两个非负整数 t 和 k（0 ≤ t ≤ 10^9），描述一个操作，其中 t 不超过此操作前数组的长度。
```

### **输出描述:**

```
输出 q 行，每行包含一个整数，表示答案。
```

### **示例 1:**

#### 输入

```
5
0 1
0 2
1 3
0 1
2 100000
```

#### 输出

```
1
5
7
25
200001
```

#### 解释
- 第一次操作后，当前数组是 [1]，后缀和数组是 [1]，后缀和的总和是 1。
- 第二次操作后，当前数组是 [1, 2]，后缀和数组是 [3, 2]，后缀和的总和是 5。
- 第三次操作后，当前数组是 [3]，后缀和数组是 [3]，后缀和的总和是 7。
- 第四次操作后，当前数组是 [3, 1]，后缀和数组是 [4, 1]，后缀和的总和是 25。
- 第五次操作后，当前数组是 [100000]，后缀和数组是 [100000]，后缀和的总和是 200001。

### 示例 2**
#### 输入

```
1
0 1000000000
```

#### 输出

```
1000000000
```

# 解决
## 中心思想
- 由题得按位与运算后只剩下最后面的 1, 所以在选择数字时应满足最后一位为 1 且前面的每一位至少要有 1 个 0( 1 AND 0 = 0 )
- 方案数为 $$
\sum_{k=1}^n2^{(n-k)(m-1)}(2^k-1)^{m-1}

$$
- 时间复杂度为O(n(n+m))
### 公式获得
- 对于序列 AAA 中的每个整数，我们可以将其看作一个 m 位的二进制数。
- 符合条件的序列中，所有末位为 1 的元素的 & 和一定为 1，因为其他元素的末位为 0，再做 & 运算会消灭末位 1。
- 枚举序列包含的末位为 1 的元素个数 i。
- 对于这 i 个元素，要满足除末位以外每一个二进制位不全为 1。这 i 个数每个二进制位上的方案数为 $2^i−1$，除末位外有 $m−1$ 个二进制位，（有序）方案数为 $a=(2^i−1)^{m−1}$。
- 对于剩余的 n−in - in−i 个元素，只需要保证末位为 0。可能的数字有 $2^{m−1}$ 种，n−i 个数的（有序）方案数为 $b=(2m−1)n−i$。
- 综合部分，方案数为 a∗b∗(C(n,i))。C(n,i) 表示序列的 n 个位置中选取 i 个用于顺序放置末位为 1 的个数。
