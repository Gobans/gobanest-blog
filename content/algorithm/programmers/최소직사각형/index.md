---
emoji: π§Ά
title: '[νλ‘κ·Έλλ¨Έμ€] μ΅μμ§μ¬κ°ν'
date: '2023-01-09 00:00:00'
author: κ³ λ°
tags: μκ³ λ¦¬μ¦
categories: Algorithm
---

## 1. λ¬Έμ 

`νλ‘κ·Έλλ¨Έμ€`

[κ³ λμ  Kit ](https://school.programmers.co.kr/learn/courses/30/lessons/86491)


<br/>

## 2. ν΅μ¬ μμ΄λμ΄

`μμ νμ` `μ λ ¬`

<br/>

## 3. μ½λ

```swift
import Foundation

func solution(_ sizes:[[Int]]) -> Int {
    let sortedSizes = sizes.sorted { lhs, rhs in
        return lhs[0]*lhs[1] > rhs[0]*rhs[1]
    }
    let maxSize = sizes.max { lhs, rhs in
        return lhs.max()! <= rhs.max()!
    }!
    let someMax = maxSize.max()!
    var someSize = 0
    while true {
        var isPossible = true
        for size in sortedSizes {
            if (someSize < size[0] && someSize < size[1] ) {
                isPossible = false
                break
            }
        }
        if isPossible {
            return someMax*someSize
        }
        someSize += 1
    }
    return someSize
}
```

<br/>

## 4. νμ΄ κ³Όμ 

λ¬Έμ λ₯Ό μ΄ν΄νλλ° μκ°μ λ§μ΄ μΌκ³ , κ΅¬ν λ°©λ²μ΄ κ³§λ°λ‘ λ μ€λ₯΄μ§ μμμ λ ν€λ§Έλ λ¬Έμ μ΄λ€.

νμ¬ λ΅μΌλ‘ μ μΆν μ½λλ λ¬Έμ λ₯Ό μ‘°κΈ μ€ν΄ν΄μ μμ±ν μ½λμΈλ°, λλ κ°λ‘ μΈλ‘ μ€ μ΅μκ°μ΄ μ§κ°λ€(sizes) λ§κ³  λ€λ₯Έ μ«μμμ λμ¬ μλ μμ κ²μ΄λΌ μκ°νκ³  μ½λλ₯Ό μμ±νλ€.

μ΄λ νλ¦° κ²μΌλ‘, μ΅λκ° μ΅μκ° λͺ¨λ sizes μμ μλ μ§κ°μ ν¬κΈ°μμ μ°μΆλλ€. (λΉμ°νκ±΄λ° μ μ΄μνκ² μκ°νμκΉ..!)

<br/>

## 5. λ€λ₯Έ μ¬λμ μ½λ

```swift
import Foundation

func solution(_ sizes:[[Int]]) -> Int {
    var maxNum = 0
    var minNum = 0

    for size in sizes {
        maxNum = max(maxNum, size.max()!)
        minNum = max(minNum, size.min()!)
    }
    return maxNum * minNum
}

```

κΉλνκ² size μ€μμ μ΅λκ° μ΅μκ°μ μ°Ύκ³ μλ€.

μ΄μ§ μ¬κ·μ  λλμ λ³μκ° νΉμ΄νλ€. π

<br/>


```toc

```
