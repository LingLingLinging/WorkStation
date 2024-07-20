---
Created Time: 星期一, 七月 15日 2024, 10:07:13 上午
Title: 0-2-1 深度优先算法 Depth First Search
aliases: ["**目录 Content**"]
linter-yaml-title-alias: "**目录 Content**"
Last Update: 星期一, 七月 15日 2024, 2:23:26 下午
---

#acm #学习

# **目录 Content**

1. [0-2 深度优先算法](#0-2%20%E6%B7%B1%E5%BA%A6%E4%BC%98%E5%85%88%E7%AE%97%E6%B3%95)
	1. [题目类型描述](#%E9%A2%98%E7%9B%AE%E7%B1%BB%E5%9E%8B%E6%8F%8F%E8%BF%B0)
	1. [题目示例](#%E9%A2%98%E7%9B%AE%E7%A4%BA%E4%BE%8B)
		1. [**示例 1:**](#**%E7%A4%BA%E4%BE%8B%201:**)
		1. [拓展题](#%E6%8B%93%E5%B1%95%E9%A2%98)


# 0-2-1 深度优先算法
`Depth First Search`
## 题目类型描述
	图问题，如 最长递增/递减路径 等
## 题目示例
### **示例 1:**
求下图中的最长递减路径:

$$

\begin{array}{| c | c | c |}
\hline
\text{1} & \text{1} & \text{3} \\
\hline
\text{2} & \text{3} & \text{4} \\
\hline
\text{1} & \text{0} & \text{1}\\
\hline
\end{array}

$$

#### 解法
##### 1、递归解法 Recursive Solution
中心思想:
	依次查看每个点向四周移动是否可行并记下最长路径

```python
def dfs(i,j,val):
    if i<0 or i==m:
        return 0 
    if j<0 or j==n:
        return 0
    if lst[i][j]>=val:
        return 0
```

###### 逐个解读
变量解释

$$
\begin{array}{c c}
\text{变量} & \text{在代码中含义 }\\
\hline
i & \text{横坐标} \\
j & \text{纵坐标} \\
val & \text{当前坐标的值}
\end{array}
$$

逐行分析
`dfs(i,j,val)` 传入当前坐标的 x、y 坐标以及值
`if i<0 or i==m : return 0 ` 横坐标越界
`if j<0 or j==n : return 0 `  纵坐标越界
`if lst[i][j]>=val : return 0 ` 不满足递减
完善代码:

```python
lst=[
	 [1,1,3],
	 [2,3,4],
	 [1,0,1]
]
m,n=3,3  #行,列
def dfs(i,j,val):
    if i<0 or i==m:
        return 0  # 行越界
    if j<0 or j==n:
        return 0  # 列越界
    if lst[i][j]>=val:
        return 0  # 不是递减，不满足
    
    res = 1
    res = max(res, 1 + dfs(i-1,j,lst[i][j]))  # 向上
    res = max(res, 1 + dfs(i + 1, j, lst[i][j]))  # 向下
    res = max(res, 1 + dfs(i, j-1, lst[i][j]))  # 向左
    res = max(res, 1 + dfs(i , j+1, lst[i][j]))  # 向右

    return res

for x in range(m):
    for y in range(n):
        res = dfs(x,y,100)
        print(res,end=" ")
    print()
'''输出
- 1 1 2
- 3 4 5
- 2 1 2
(输出为每个位置的最长递减路径长度,求max即为答案)
'''
```

##### 2、中间解保存 Memorize Intermediate Results
中心思想:
	比如看(3,2) 的时候(4), 向左走时遇到已经运行过的 (2,2) 3, 从表格中读取这格的最长路径长度, 存到本格的位置以便可能的调用

$$
\begin{array}{| c | c | c |}
\hline
\text{1} & \text{1} & \text{3} \\
\hline
\text{2} & \text{3} & \text{4} \\
\hline
\text{1} & \text{0} & \text{1}\\
\hline
\end{array}
$$

```python
lst=[
	 [1,1,3],
	 [2,3,4],
	 [1,0,1]
]
m,n=3,3  #行,列
def dfs(i,j,val):
    if i<0 or i==m:
        return 0  # 行越界
    if j<0 or j==n:
        return 0  # 列越界
    if lst[i][j]>=val:
        return 0  # 不是递减，不满足
    if (i,j) in dp:
        return dp[(i,j)]
    
    res = 1
    res = max(res, 1 + dfs(i-1,j,lst[i][j]))  # 向上
    res = max(res, 1 + dfs(i + 1, j, lst[i][j]))  # 向下
    res = max(res, 1 + dfs(i, j-1, lst[i][j]))  # 向左
    res = max(res, 1 + dfs(i , j+1, lst[i][j]))  # 向右
    dp[(i,j)]=res #保存
    return res

dp={}
for x in range(m):
    for y in range(n):
        res = dfs(x,y,100)
        print(res,end=" ")
    print()
print(dp)
'''输出
- 1 1 2
- 3 4 5
- 2 1 2  (同递归的答案)
- {(0, 0): 1, (0, 1): 1, (0, 2): 2, (2, 1): 1, (2, 0): 2, (1, 0): 3, (1, 1): 4, (2, 2): 2, (1, 2): 5}  （最终的路径）
'''
```

### 拓展题

```
    有一片海域划分为N*M个方格，其中有些海域已被污染（用0表示），有些海域没被污染（用1表示）。请问这片N*M海域中有几块是没被污染的独立海域（没被污染的独立海域是指该块海域上下左右被已污染的海域包围，且N*M以外的海域都视为已被污染的海域）例如：N=4，M=5，4*5的海域中，已被污染海域和没被污染的海域如下图：
```

![[Pasted image 20240715140402.jpg]]

```
    这块4*5的海域，有3块海域（绿色）没被污染，因为每一块的上下左右都被污染的海域包围。

输入描述:
	第一行输入两个正整数N和M，N表示矩阵方格的行，M表示矩阵方格的列，N和M之间以一个英文逗号隔开
	第二行开始输入N行，每行M个数字（数字只能为0，1表示没被污染的海域，0表示已被污染的海域）
输出描述:
	输出一个整数，表示N*M的海域中有几块是没被污染的独立海域 
```

#### 解法
##### 递归算法 Recursive Solution

```python
lst = [[1, 1, 0, 0, 0],
       [1, 0, 0, 0, 0],
       [0, 0, 0, 0, 0],
       [1, 1, 0, 1, 1]]

m = 4  # m是行, n是列
n = 5
def dfs(x, y):
    if x < 0 or x == m or y < 0 or y == n or lst[x][y] == 0:
        return
    lst[x][y] = 0  # 标记一下
    dfs(x + 1, y)  # 向上
    dfs(x - 1, y)  # 向下
    dfs(x, y - 1)  # 向左
    dfs(x, y + 1)  # 向右

cnt = 0
for i in range(m):
    for j in range(n):
        if lst[i][j] == 1:
            dfs(i, j)
            cnt += 1
print(cnt)
```
