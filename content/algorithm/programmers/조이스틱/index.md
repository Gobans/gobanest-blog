---
emoji: π§Ά
title: '[νλ‘κ·Έλλ¨Έμ€] μ‘°μ΄μ€ν±'
date: '2023-01-21 00:00:00'
author: κ³ λ°
tags: μκ³ λ¦¬μ¦
categories: Algorithm
---

## 1. λ¬Έμ 

`νλ‘κ·Έλλ¨Έμ€`

[κ³ λμ  Kit Hello μ‘°μ΄μ€ν±](https://school.programmers.co.kr/learn/courses/30/lessons/42860)


<br/>

## 2. ν΅μ¬ μμ΄λμ΄

`κ·Έλ¦¬λ`

<br/>

## 3. μ½λ

```swift
import Foundation

func solution(_ name:String) -> Int {
    let targetArray: [String] = name.map{ String($0) }
    var currentAray: [String] = Array(repeating: "A", count: targetArray.count)
    var minMove = targetArray.count - 1
    var answer = 0

    for index in 0..<targetArray.count {
        if currentAray[index] != targetArray[index] {
            var currentChar = currentAray[index]
            var updownCnt = 0
            while currentChar != targetArray[index] {
                currentChar = String(UnicodeScalar(UnicodeScalar(currentChar)!.value + 1)!)
                updownCnt += 1
            }
            currentAray[index] = currentChar
            answer += min(updownCnt, 26 - updownCnt)
        }

        var endIdx = index + 1
        while endIdx < targetArray.count && targetArray[endIdx] == "A" {
            endIdx += 1
        }

        let moveFront = index * 2 + (currentAray.count - endIdx)
        let moveBack = (currentAray.count - endIdx) * 2 + index

        minMove = min(minMove, moveFront)
        minMove = min(minMove, moveBack)
    }
    return answer + minMove
}


```

<br/>

## 4. νμ΄ κ³Όμ 

μ¬μ΄ λ¬Έμ μΈμ€ μμλλ°.. μκ°λ³΄λ€ ν¨μ¬ μ΄λ €μ λ€.

μ²μμ μκ°μ μ΄λ¬λ€.

    1. μ‘°μ΄μ€ν±μ μ΄λμ μ½λλ‘ μμ±.
    -> μ‘°μ΄μ€ν±μ μ»€μ μ΄λ μ "A" λΌλ©΄ μΉ΄μ΄νΈλ₯Ό λ¬΄μν¨
    2. A μμ μλλ‘ μ΄λ or μλ‘ μ΄λ, λ μ§§μ κ²μ λ¬Έμ λ³κ²½ νμλ‘ μ¬μ©ν¨.

μ¬κΈ°μ μ‘°μ΄μ€ν±μ μ΄λμ μ½λλ‘ μμ±νλ κ³Όμ μμ, μ’μΈ‘ μ°μΈ‘μ λ°λ³΅λ¬ΈμΌλ‘ νμνκ³  μ΅μ κ°μ κ°μ§λ κΈΈμ μ ννλ©΄ λλ€κ³  μκ°νλ€..

κ·Έλ°λ° μκ³ λ³΄λ `"A" κ° μ€κ°μ λ¬΄μν λ§μ κ²½μ°` μ§κΈκΉμ§ μλ κΈΈμ λ€μ λλμ κ°λ κ²μ΄ λΉ λ₯Έ κΈΈμΌλκ° μμλ€.

<br/>

μ΄ κ²½μ°λ₯Ό μ΄λ»κ² μ²λ¦¬ν μ§ κ°μ΄ μμ‘ν [μ΄κ³³](https://inuplace.tistory.com/1091)μ μ°Έκ³ νμ¬ μ½λλ₯Ό μμ±νμλ€.

ν΅μ¬μ index 0 μΈ μλ¦¬μμ μ λ€λ‘ κ°μ λλ₯Ό κ³μ°νμ¬, κ°μ₯ λΉ λ₯Έ κ²½μ° λͺ¨λ μ°Ύμμ£Όλ κ²μ΄μλ€.

μ΄λ ΅λ€ μ΄λ €μ..!

<br/>

## 5. λ€λ₯Έ μ¬λμ μ½λ

```swift
import Foundation

func solution(_ name:String) -> Int {
    let name = Array(name)
    let aValue = Int(Character("A").asciiValue!)
    let zValue = Int(Character("Z").asciiValue!)

    var updown = 0    
    var leftright = name.count-1  

    for startIdx in 0..<name.count {
   
        updown += min(Int(name[startIdx].asciiValue!) - aValue, zValue - Int(name[startIdx].asciiValue!) + 1)

        var endIdx = startIdx + 1
        while endIdx < name.count && name[endIdx] == "A" {
            endIdx += 1
        }

        let moveFront = startIdx * 2 + (name.count - endIdx)
        let moveBack = (name.count - endIdx) * 2 + startIdx

        leftright = min(leftright, moveFront)
        leftright = min(leftright, moveBack)
    }

    return updown + leftright
}

```

λ΄κ° μ°Έκ³ ν μ½λμΈλ°, μμ£Ό κΉλνλ€..!π

<br/>


```toc

```
