---
emoji: π§Ά
title: '[νλ‘κ·Έλλ¨Έμ€] λ±κ΅£κΈΈ'
date: '2023-01-30 00:00:00'
author: κ³ λ°
tags: μκ³ λ¦¬μ¦
categories: Algorithm
---

## 1. λ¬Έμ 

`νλ‘κ·Έλλ¨Έμ€`

[κ³ λμ  Kit λ±κ΅£κΈΈ](https://school.programmers.co.kr/learn/courses/30/lessons/42898)


<br/>

## 2. ν΅μ¬ μμ΄λμ΄

`DP`

<br/>

## 3. μ½λ

[swift]
```swift
func solution(m: Int, n: Int, puddles: [[Int]]) -> Int {
    var grid: [[Int]] = Array(repeating: Array(repeating: 0, count: m + 1), count: m + 1)
    grid[1][1] = 1
    for puddle in puddles {
        grid[puddle[1]][puddle[0]] = -1
    }
    for i in 1...n {
        for j in 1...m {
            if grid[i][j] == -1 {
                grid[i][j] = 0
                continue
            }
            grid[i][j] += (grid[i - 1][j] + grid[i][j - 1]) % 1000000007
        }
    }
    return grid[n][m]
}
```

<br/>

## 4. νμ΄ κ³Όμ 

μ²μμ DFSλ‘ μ¬λ¬ κ²½λ‘λ₯Ό νμνλ©΄ λ°λ‘ ν μ μμ§ μλ? μκ°μ νλ€.

    1. path λ₯Ό DFS λ‘ νμ. (κ²½λ‘μ κ°μλ₯Ό κ΅¬ν΄μΌνκΈ° λλ¬Έμ)
    2. κ²©μμλ€κ° νμ¬κΉμ§ νμν μ΄λκ°μ λ£μ΄μ€ (κ°κ±°λ μμ κ²½μ°λ§ κ³μ νμ)
    3. νμμ μλ£νλ©΄ κ°μ λ°λΌ cnt κ°±μ 

<br/>

μ΄ μκ°μ λ°νμΌλ‘ μ½λλ₯Ό μμ±νμλλ°..

```python
minMoveCnt = 100000
pathCnt = 0
def solution(m, n, puddles):
    grid = [[ 0 for _ in range(m + 1)] for _ in range(n + 1)]
    moves = [(0,1), (1,0)]
    for puddle in puddles:
        grid[puddle[1]][puddle[0]] = -1
    def DFS(x,y, moveCnt):
        global minMoveCnt
        global pathCnt
        if (x,y) == (m,n):
            if moveCnt == minMoveCnt:
                pathCnt += 1
            elif moveCnt < minMoveCnt:
                minMoveCnt = moveCnt
                pathCnt = 1
            return
        for move in moves:
            dx = x + move[0]
            dy = y + move[1]
            if dx <= m and dy <= n:
                if grid[dy][dx] == 0 or moveCnt + 1 <= grid[dy][dx]:
                    grid[dy][dx] = moveCnt + 1
                    DFS(dx,dy, moveCnt + 1)

    DFS(1,1,0)
    return pathCnt
```

μμνκ²~ μκ°μ΄κ³Όκ° λ¨Ήνλ€.

μ΄κ²λ λ°λ‘ μ΄μ μ νμλ [μ μμΌκ°ν](https://gobanest.com/algorithm/programmers/μ μ%20μΌκ°ν/) κ³Ό λΉμ·ν μ νμμΌλ‘ νμ΄μΌνλ λ¬Έμ μλ€.

<br/>

`μλ` `μ€λ₯Έμͺ½`μΌλ‘λ§ λ°©ν₯μ΄λμ΄ κ°λ₯νκΈ° λλ¬Έμ,

<br/>

> dp[i][j] = dp[i-1][j] + dp[i][j-1]

μλ‘ κ°μ λ£μ μΉΈ = λ°λ‘ μμΉΈκΉμ§μ κ²½λ‘μ + λ°λ‘ μΌμͺ½μΉΈ κΉμ§μ κ²½λ‘μ

μ΄ μ νμμ΄ μ±λ¦½νλκ±°μλ€.

<br/>

λλ μ λ°λ‘ μμμ°¨λ¦¬μ§ λͺ»νμκΉ..! π₯²

[μ΄κ³³](https://dev-note-97.tistory.com/141)μ μ°Έκ³ ν΄μ μκ²λμλ€..

<br/>
<br/>

λ§λΆμ¬ νλ‘κ·Έλλ¨Έμ€ λ¬Έμ λ€ swift μ§μμ μμ΄λ κ² μνλκ±ΈκΉ... 3κ°μ νλκΌ΄λ‘ μ§μμ μνλ λλμ΄λ€. πΏ μ£Όμ μ£Όμ ...

<br/>


```toc

```
