---
Created Time: 星期四, 七月 11日 2024, 6:27:09 晚上
Title: 0-1 背包问题 Knapsack Problem
aliases:
  - 0-1 背包问题
linter-yaml-title-alias: 0-1 背包问题
Last Update: 星期一, 七月 15日 2024, 9:57:14 上午
---
#acm #学习

# **目录 Content**

1. [0-1 背包问题](#0-1%20%E8%83%8C%E5%8C%85%E9%97%AE%E9%A2%98)
	1. [题目类型描述](#%E9%A2%98%E7%9B%AE%E7%B1%BB%E5%9E%8B%E6%8F%8F%E8%BF%B0)
	1. [题目示例](#%E9%A2%98%E7%9B%AE%E7%A4%BA%E4%BE%8B)
		1. [**示例 1:**](#**%E7%A4%BA%E4%BE%8B%201:**)
		1. [示例 2](#%E7%A4%BA%E4%BE%8B%202)

# 0-1 背包问题
`Knapsack Problem`
## 题目类型描述
	在有限的容量(Limited Volume或者其他限制) 下达到价值总和(Value 或者其他值) 最大
## 题目示例
### **示例 1:**
有一个背包,容量为10kg,要在一下物品中选择,欲使背包内物品的价值最大

| 重量  | 1   | 2   | 4   | 2   | 5   |
| :-: | :---: | :---: | :---: | :---: | :---: |
| 价值  | 5   | 3   | 5   | 3   | 2   |
#### 解法
##### 1、递归解法 Recursive Solution
从后往前, 标记每一个物品(放的标 yes(示例), 不放的标 no)

```python
def ks(n,C):
    if n==0 or C==0: #①
    	result=0
    elif w[n]>C:
	    result=ks(n-1,C)
    else:
	    tmp1=ks(n-1,C)
	    tmp2=v[n]+ks(n-1,C-w[n])
	    result=max(tmp1,tmp2)
return result
```

###### 逐个解读
变量解释

$$
\begin{array}{c c}
\text{变量} & \text{在代码中含义 }\\
\hline
n & \text{下一个物品的索引(编号)} \\
C & \text{剩余容量} 
\end{array}
$$

逐行分析
`if n==0 or C==0:result=0`: 确认剩余的容量, 如果为 0(没有空间了)—结束(递归出口)
`elif w[n]>C:result=ks(n-1,C)`: 如果该物品的占用空间大于剩余空间: 跳到下一个
`else:`
	`tmp1=ks(n-1,C)` :分支 1, 不放该物品
	`tmp2=v[n]+ks(n-1,C-w[n])`: 分支 2, 放该物品
	`result=max(tmp1,tmp2)`: 比较两个方案最终结果谁大, 取大的
`return result`
时间复杂度: $O（2^n）$

完善代码:

```python
w = [0, 1, 2, 4, 2, 5]
v = [0, 5, 3, 5, 3, 2]

def ks(n, C):
    if n == 0 or C == 0:
        result = 0
    elif w[n] > C:
        result = ks(n - 1, C)
    else:
        tmp1 = ks(n - 1, C)
        tmp2 = v[n] + ks(n - 1, C - w[n])
        result = max(tmp1, tmp2)
    return result

res = ks(len(w) - 1, 10)
print(res)
```

可以继续完善成获取输入以及循环
##### 2、中间结果记忆 Memorize Intermediate Results
中心思路:
	将结果以自变量和因变量为两个轴，创建二维表
	如果在运行过程中这个值已经存在表里了就直接读取，如果没有就写进表里

```python
w = [0,1,2,4,2,5]
v = [0,5,3,5,3,2]

def ks(n, C):
    if memo[n][C] != 0:
        for row in memo:
            print(row)
        print()
        return memo[n][C] # 取出结果
    
    if n == 0 or C == 0: # base case
        result = 0
    elif w[n] > C:
        result = ks(n-1, C)
    else:
        tmp1 = ks(n-1, C)
        tmp2 = v[n] + ks(n-1, C - w[n])
        result = max(tmp1, tmp2)
    
    memo[n][C] = result # 存结果
    return result

n = 5
C = 10
memo = [[0] * (C+1) for x in range(n+1)] # 数据存储在列表中
res = ks(n, C)
```

### 示例 2

宝妈在网购平台上指定了N(2≤N≤50) 件礼品供小明挑选, 挑选钱妈妈提出以下要求:
	每种礼物只能挑选一件(即不重复)
	总价值不能超过V(1≤V≤100)
已知 N 件礼物中小明对每件礼物的喜爱值, 请帮小明挑选使得喜爱值s最高且满足要求, 输出喜爱值

#### 解法(中间结果记忆)

```python
def ks(n, C):
    if memo[n][C] != 0:
        for row in memo:
            print(row)
        print()
        return memo[n][C] # 取出结果
    
    if n == 0 or C == 0: # base case
        result = 0
    elif w[n] > C:
        result = ks(n-1, C)
    else:
        tmp1 = ks(n-1, C)
        tmp2 = v[n] + ks(n-1, C - w[n])
        result = max(tmp1, tmp2)
    
    memo[n][C] = result # 存结果
    return result

# 输入处理
n, C = list(map(int, input().split(',')))
w = [0]
v = [0]
for x in range(n):
    w1, v1 = list(map(int, input().split(',')))
    w.append(w1)
    v.append(v1)

memo = [[0] * (C + 1) for _ in range(n + 1)] # 数据存储在列表中
res = ks(n, C)
print(res)
```
