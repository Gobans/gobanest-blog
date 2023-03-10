---
emoji: π§Ά
title: '[νλ‘κ·Έλλ¨Έμ€] λ°©μ κ°μ'
date: '2023-02-23 00:00:00'
author: κ³ λ°
tags: μκ³ λ¦¬μ¦
categories: Algorithm
---

## 1. λ¬Έμ 

`νλ‘κ·Έλλ¨Έμ€`

[κ³ λμ  Kit λ°©μ κ°μ](https://school.programmers.co.kr/learn/courses/30/lessons/49190)


<br/>

## 2. ν΅μ¬ μμ΄λμ΄

`κ·Έλν` `κ·Έλ¦¬λ`

<br/>

## 3. μ½λ

```swift
import Foundation

struct Point: Hashable {
    let y: Int
    let x: Int
}

struct Route: Hashable {
    let from: Point
    let to: Point
}

func solution(_ arrows:[Int]) -> Int {
    var answer = 0
    // y, x μ΄λ μ’ν
    let move = [(-1, 0), (-1, 1), (0, 1), (1, 1), (1, 0), (1, -1), (0, -1), (-1, -1)]
    var isVisited: [Point : Bool] = [:]
    var isVisitedDirection: [Route: Bool] = [:]
    
    var now = Point(y: 0, x: 0)
    isVisited[now] = true
    arrows.forEach { arrow in
        for _ in 0..<2 {
            let next = Point(y: now.y + move[arrow].0, x: now.x + move[arrow].1)
            if isVisited[next] == true {
                if isVisitedDirection[Route(from: now, to: next)] == nil {
                    answer += 1
                }
            } else {
                isVisited[next] = true
            }
            isVisitedDirection[Route(from: now, to: next)] = true
            isVisitedDirection[Route(from: next, to: now)] = true
            now = next
        }
    }
    return answer
}
```

<br/>

## 4. νμ΄ κ³Όμ 

μ°μ  λ¬Έμ λ₯Ό λ³΄κ³  λ€μκ³Ό κ°μ΄ μκ°νλ€.

    λκ°μ μ μμ§μμ λνλ΄κΈ° μν΄ μμ§μμ 2λ°°λ‘ λ§λ€κΈ°?
    μ¬λ¬λ°©μ΄ μλμ§ μ΄λ»κ² νμΈνλκ°?
    λ°©μ΄ λ§λ€μ΄μ§λ μ‘°κ±΄: μ§λμλ μ’νλ₯Ό λ λ°©λ¬Ένμλ
    -> 1. λκ² μ΄λ ν λνμΌλ‘ λ§λ€μ΄ μ Έμ λμ°©νμλ
    -> 2. λκ°μ μΌλ‘ μμ μΈλͺ¨μ ννλ‘ λ§λ€μ΄ μ‘μλ

<br/>

λκ°μ μ μμ§μμ λνλ΄κΈ° μν΄μ μ’νκ³λ₯Ό 2λ°°λ‘ κ·Έλ¦¬λ κ²μ [μμ΄ν μ€κΈ°](https://gobanest.com/algorithm/programmers/μμ΄ν%20μ€κΈ°/) λ¬Έμ μμ μμ΄λμ΄λ₯Ό λ μ¬λ Έλ€.

λκ°μ μ νμνλ μ΄μ λ λ€μκ³Ό κ°λ€.

<br/>

![room2.png](room2.png)|

<br/>

κ·Έλ¦Όμμμ²λΌ λ€λͺ¨μμ νλμ λκ°μ μ΄ κ°λ‘μ§λ¬ 2κ°μ λ°©μ΄ μλ μνλ₯Ό κ°μ ν΄λ³΄μ.

<br/>

![room4.png](room4.png)|

<br/>

κ·Έ λ€μ λκ°μ μ λ€λ₯Έ λκ°μ μ΄ κ°λ‘μ§λ₯΄λ κ²½μ°, μ’νκ³μμ λ°λ‘ νμν  μ μμΌλ―λ‘ ν΄λΉ λκ°μ μμ κ΅μ°¨νλ€λ μ¬μ€μ μκΈ° μ΄λ ΅λ€.

νμ§λ§ μ’νκ³λ₯Ό 2λ°°λ‘ λ§λ λ€λ©΄, λκ°μ μ μ€κ°μ λΈλκ° μκ²¨μ μ½κ² λκ°μ μ κ΅μ°¨λ₯Ό νμΈν  μ μλ€.

<br/>

κ·Έ λ€μ λ°©μ΄ λ§λ€μ΄μ§λ μ‘°κ±΄μ `νμ¬ λΈλμμ κΈ°μ‘΄μ λ°©λ¬Ένλ λΈλλ₯Ό λ€μ λ°©λ¬Ένμλ` μ΄λ€. 

λλ¬Έμ νμ¬ λΈλμ λ°©λ¬Έν  λ€μ λΈλ λκ° λͺ¨λ νμνκ³ , μ΄ λμ κ²½λ‘λ₯Ό μΆμ νλ κ²μ΄ νμνλ€.

(μ€λ³΅λλ κ²½λ‘λ‘ λ°©μ κ°μκ° μ€λ³΅ μΉ΄μ΄ν λλ κ²μ λ§κΈ° μν¨)

<br/>

κ·Έλ¦¬κ³  μ΄λ¬ν μμ΄λμ΄λ₯Ό μ’ν©ν΄μ μ½λλ₯Ό μ§λ©΄ λλ€. (μ΄ν κ±Έλ¦Όγγ)

<br/>

μ½λμμ Pointμ Route κ΅¬μ‘°μ²΄λ₯Ό λ§λ€μ§ μκ³  κ·Έλ₯ tupleλ‘ λ¬Έμ λ₯Ό νλ €νλλ°,

Swiftμμλ dictionaryμ tupleμ μ΄μ©ν  μ μμλ€.

μ°Ύμλ³΄λ hashableλ‘ μ¬μ©ν  μ μκ² λ§λλ λΌμλ₯Ό [μ΄κ³³](https://forums.swift.org/t/synthesizing-equatable-hashable-and-comparable-for-tuple-types/7111) μμ νμΈν  μ μλλ°, Swift μ½μ΄ κ°λ°μλ€μ΄ κ΅¬νμ λ³΅μ‘μ±κ³Ό μ»΄νμΌ μκ°μ λν μ°λ €λ‘ λ°λν΄μ λ¬΄μ°λλ―νλ€.

π₯²


<br/>

κ·Όλ° κ΅¬μ‘°μ²΄λ₯Ό λ§λ€μ΄μ μ¬μ©νλ λ κ°λμ±μ΄ μ€λ₯Έ κ² κ°λ€. μ€νλ € μ’μ?

μ νμ ν°λ»μ λ νλ² λλλ€...


```toc

```
