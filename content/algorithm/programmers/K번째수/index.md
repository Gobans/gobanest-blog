---
emoji: π§Ά
title: '[νλ‘κ·Έλλ¨Έμ€] Kλ²μ§Έμ'
date: '2023-01-07 00:00:00'
author: κ³ λ°
tags: μκ³ λ¦¬μ¦
categories: Algorithm
---

## 1. λ¬Έμ 

`νλ‘κ·Έλλ¨Έμ€`

[κ³ λμ  Kit Kλ²μ§Έμ](https://school.programmers.co.kr/learn/courses/30/lessons/42748)


<br/>

## 2. ν΅μ¬ μμ΄λμ΄

`μ λ ¬` `λ¬Έμμ΄ μ¬λΌμ΄μ±`

<br/>

## 3. μ½λ
[swift]
```swift
import Foundation

func solution(_ array:[Int], _ commands:[[Int]]) -> [Int] {
    var answer: [Int] = []
    for command in commands {
        let slicedArray = array[command[0] - 1...command[1] - 1]
        let sortedSlicedArray = slicedArray.sorted(by: < )
        let element = sortedSlicedArray[command[2] - 1]
        answer.append(element)
    }
    
    return answer
}

```

<br/>

## 4. νμ΄ κ³Όμ 

λ¬Έμ μμ μκ΅¬νλλλ‘ μ½λμ νλ‘μ°λ₯Ό λ€μκ³Ό κ°μ΄ μκ°νλ€.

1. commands 1,2 λ‘ λ°°μ΄ μ¬λΌμ΄μ±
2. μ¬λΌμ΄μ±ν λ°°μ΄μ μ λ ¬
3. commands 3 λ²μ¨° μμ μ λ΅ λ°°μ΄μ μΆκ°
-> λ°λ³΅

κ·Έλλ‘ κ΅¬νν΄μ νμλλ°, νΈλ κ³Όμ μμ `SubSequence`μ λν μ΄ν΄λ₯Ό μ λͺ°λΌμ μ€λ₯κ° λ°μνμλ€.

```swift
let slicedArray = array[command[0] - 1...command[1] - 1]
slicedArray.sort(by: < )
let element = slicedArray[command[2] - 1]
```

μ΄ μ½λλ‘ μ²μμ λ°°μ΄μ κ³§λ°λ‘ μ λ ¬μ ν΄μ μΈλ±μ±μ ν΄μ€¬λλ°, index out of range μ€λ₯κ° λ°μνλ€. μ΄μ λ μ¦μ¨ slicedArray μ **index κ°μ΄ μλ‘λ§λ€μ΄ μ§μ§ μκΈ°** λλ¬Έμ΄λ€.

μλνλ©΄ `SubSequence` λ λ°°μ΄μ μλ‘ λ§λ€μ΄ λ΄λκ² μλλΌ, μ°Έμ‘°ν΄μ λ§λ€μ΄μ§κΈ° λλ¬Έμ΄λ€. λν μλ λ°°μ΄μ indices λ₯Ό κ³΅μ νλ€.

-> κΈ°μ‘΄ λ°°μ΄μ idnex κ°λ€μ΄ μ μ§κ° λ¨.

![subSequence.png](subSequence.png)


κ·Έλμ μλ‘­κ² λ°°μ΄μ λ§λ€μ΄λ΄λ sorted λ index μ€λ₯κ° μμκ³ , sort λ index μ€λ₯κ° λ°μνλ€.

λλ¬Έμ κ·Έλλ‘ λ°°μ΄μ μ μ§νμ±λ‘ indexing μ νκΈ°μν΄μλ μλ μ½λμ κ°μ΄ index λ₯Ό start index λ§νΌ λν΄μ€μ μλ³Έ λ°°μ΄μ index λ‘ SubSequence indexλ₯Ό μλ‘ λ§μΆλ μμμ΄ νμνλ€.

```swift
func solution(_ array:[Int], _ commands:[[Int]]) -> [Int] {
    var answer: [Int] = []
    for command in commands {
        var slicedArray = array[command[0] - 1...command[1] - 1]
        slicedArray.sort(by: <)
        let bufferIndex = slicedArray.index(command[2] - 1, offsetBy: slicedArray.startIndex)
        // changed
        let element = slicedArray[bufferIndex]
        answer.append(element)
    }
    
    return answer
}
```



<br/>

## 5. λ€λ₯Έ μ¬λμ μ½λ

```swift
import Foundation

    func solution(_ array:[Int], _ commands:[[Int]]) -> [Int] {
        return commands.map({(key) in
            return array[(key[0]-1)...(key[1]-1)].sorted()[key[2]-1]
        })

    }
```

κΉλνκ² mapμ μ¬μ©νμ¬ λ¬Έμ λ₯Ό νμλ€! 

map μμ°λ©΄ λ©μλλ―.

<br/>


```toc

```
