---
Created Time: 星期一, 七月 15日 2024, 3:25:39 下午
Title: Divide it!
aliases: ["**目录 Content**"]
linter-yaml-title-alias: "**目录 Content**"
Last Update: 星期二, 七月 16日 2024, 9:35:45 上午
---

# **目录 Content**

1. [A. Divide it!](#A.%20Divide%20it!)
	1. [Input](#Input)
	2. [Output](#Output)
	3. [Example](#Example)
		1. [Input](#Input)
		2. [Output](#Output)
	4. [解决](#%E8%A7%A3%E5%86%B3)
		1. [错误的](#%E9%94%99%E8%AF%AF%E7%9A%84)
		2. [问题:](#%E9%97%AE%E9%A2%98:)
		3. [正确的](#%E6%AD%A3%E7%A1%AE%E7%9A%84)




#笔记 #acm
# A. Divide it

```request
time limit per test: 1 second
memory limit per test:256 megabytes
input:standard input
output: standard output
```

You are given an integer n.

You can perform any of the following operations with this number an arbitrary (possibly, zero) number of times:
	1. Replace n with $\frac{n}{2}$ if n is divisible by 2;
	2. Replace n with $\frac{2n}{3}$ if n is divisible by 3;
	3. Replace n with $\frac{4n}{5}$ if n is divisible by 5.

For example, you can replace 30 with 15 using the first operation, with 20 using the second operation or with 24 using the third operation.

Your task is to find the minimum number of moves required to obtain 1 from n or say that it is impossible to do it.

You have to answer q independent queries.

## Input
	The first line of the input contains one integer q𝑞 (1≤q≤10001≤𝑞≤1000) — the number of queries.
	The next q𝑞 lines contain the queries. For each query you are given the integer number n𝑛 (1≤n≤10181≤𝑛≤1018).


## Output
	Print the answer for each query on a new line. If it is impossible to obtain 11 from n𝑛, print -1. Otherwise, print the minimum number of moves required to do it.

## Example
### Input

```input
7
1
10
25
30
14
27
1000000000000000000
```

### Output

```output
0
4
6
6
-1
6
72
```

## 解决
### 错误的

```ad-bug
问题代码
```
```python
def runfile():
    x=int(input())
    a,b,c=0,0,0
    if x==0:
        print("-1")
        return
    while x%5==0:
        c+=1
        x/=5
    while x%3==0:
        b+=1
        x/=3
    while x%2==0:
        a+=1
        x/=2
    if x!=1:
        print(-1)
        return
    else:
        a+=(2*c+b)
        answ=a+b+c
        print(answ)

n=int(input())
for i in range(n):
    runfile()
```

### 问题
最重要：==**未显式处理输入为 1 的情况**==
细节: 未使用整数除法（大数据容易出现精度问题）

### 正确的

```ad-success
正确结果
```
```python
def runfile(x):
    a, b, c = 0, 0, 0
    
    if x == 0:
        return -1
    if x == 1:
        return 0

    while x % 5 == 0:
        c += 1
        x //= 5

    while x % 3 == 0:
        b += 1
        x //= 3

    while x % 2 == 0:
        a += 1
        x //= 2

    if x != 1:
        return -1

    a += 2 * c + b
    answer = a + b + c
    return answer

n = int(input())
for _ in range(n):
    x = int(input())
    print(runfile(x))
```
