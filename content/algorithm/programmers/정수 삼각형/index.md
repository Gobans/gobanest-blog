---
emoji: π§Ά
title: '[νλ‘κ·Έλλ¨Έμ€] μ μ μΌκ°ν'
date: '2023-01-30 00:00:00'
author: κ³ λ°
tags: μκ³ λ¦¬μ¦
categories: Algorithm
---

## 1. λ¬Έμ 

`νλ‘κ·Έλλ¨Έμ€`

[κ³ λμ  Kit μ μ μΌκ°ν](https://school.programmers.co.kr/learn/courses/30/lessons/43105)


<br/>

## 2. ν΅μ¬ μμ΄λμ΄

`DP` `λ©λͺ¨μ΄μ μ΄μ`

<br/>

## 3. μ½λ

[swift]
```swift
import Foundation

func solution(triangle:[[Int]]) -> Int {
    var answer = 0
    var nTriangle = triangle.map { [0] + $0 + [0] }
    for i in 1..<nTriangle.count {
        for j in 1...i+1 {
            nTriangle[i][j] += max(nTriangle[i-1][j-1], nTriangle[i-1][j])
        }
    }
    answer = nTriangle[nTriangle.endIndex - 1].max()!
    return answer
}
```

<br/>

## 4. νμ΄ κ³Όμ 

κ°λ¨νκ² DFS λ‘ κ±°μ³κ° μ«μλ₯Ό νμ ν μλ°μ΄νΈ νλ©΄ λμ§ μμκΉ μκ°μ νλλ°.. DFSλ‘ νμλλ μκ°μ΄κ³Όκ° λ¬λ€.

```python
maxSum = 0
def solution(triangle):
    answer = 0
    def DFS(nodeIndex, lineIndex, sum):
        global maxSum
        sum += triangle[lineIndex][nodeIndex]
        if sum > maxSum:
            maxSum = sum
        if lineIndex >= len(triangle) - 1:
            return
        leftIndex = nodeIndex
        rightIndex = nodeIndex + 1
        if leftIndex >= 0:
            DFS(leftIndex, lineIndex + 1, sum)
        if rightIndex < len(triangle[lineIndex + 1]):
            DFS(rightIndex, lineIndex + 1, sum)
    DFS(0,0,0)
    return maxSum
```

<br/>

μ‘°κΈ μ±λ₯μ κ°μ ν΄λ³΄κΈ° μν΄μ 0μΌλ‘ μ΄κΈ°ν λ Visit λ°°μ΄μ λ§λ€μ΄, DFS λ‘ νμμ ν  λ νλ² λ μ‘°κ±΄μ κ±Έμ΄ νμνλ μ½λλ₯Ό μμ±ν΄λ΄€λ€.
```python
maxSum = 0
def solution(triangle):
    answer = 0
    # visit λ°°μ΄μ λ§λ€μ΄μ μ΅λκ° μ μ₯, μ΅λκ° λ³΄λ€ ν¬λ©΄ ν΄λΉ λΈλ μ¬νμ
    triangleSum = []
    for line in triangle:
        temp = []
        for _ in line:
            temp.append(0)
        triangleSum.append(temp)

    def DFS(nodeIndex, lineIndex, sum):
        global maxSum
        sum += triangle[lineIndex][nodeIndex]
        triangleSum[lineIndex][nodeIndex] = sum
        if sum > maxSum:
            maxSum = sum
        if lineIndex >= len(triangle) - 1:
            return
        leftIndex = nodeIndex
        rightIndex = nodeIndex + 1
        if leftIndex >= 0 and triangleSum[lineIndex + 1][leftIndex] < sum + triangle[lineIndex + 1][leftIndex]:
            DFS(leftIndex, lineIndex + 1, sum)
        if rightIndex < len(triangle[lineIndex + 1]) and triangleSum[lineIndex + 1][rightIndex] < sum + triangle[lineIndex + 1][rightIndex]:
            DFS(rightIndex, lineIndex + 1, sum)
    DFS(0,0,0)
    return maxSum
```

νμ§λ§ μ¬μ ν ν¨μ¨μ± νμ€νΈλ ν΅κ³Όνμ§ λͺ»νλ€..γ

<br/>

[μ΄κ³³](https://velog.io/@younge/Python-νλ‘κ·Έλλ¨Έμ€-μ μ-μΌκ°ν-λμ κ³νλ²) μ μ°Έκ³ νμ¬ λ΅μ λ΄€λλ°, `λ©λͺ¨μ΄μ μ΄μ` μ΄λΌλκ² μ΄λ μ¬μ©λλκ±°κ΅¬λ μκ²λμλ€.

νμ€ν λ¬Έμ λ₯Ό λ§μ΄ νμ΄μΌ μ΄λ»κ² νμ§ μ’ κ°μ μ‘μ μ μμ κ² κ°λ€.

<br/>


```toc

```
