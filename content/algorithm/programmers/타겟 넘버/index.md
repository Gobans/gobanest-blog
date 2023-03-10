---
emoji: π§Ά
title: '[νλ‘κ·Έλλ¨Έμ€] νκ² λλ²'
date: '2023-02-07 00:00:00'
author: κ³ λ°
tags: μκ³ λ¦¬μ¦
categories: Algorithm
---

## 1. λ¬Έμ 

`νλ‘κ·Έλλ¨Έμ€`

[κ³ λμ  Kit νκ² λλ²](https://school.programmers.co.kr/learn/courses/30/lessons/43165)


<br/>

## 2. ν΅μ¬ μμ΄λμ΄

`DFS` `BFS`

<br/>

## 3. μ½λ

[DFS]
```swift
import Foundation

func solution(_ numbers:[Int], _ target:Int) -> Int {
    let n = numbers.count
    var answer = 0

    func DFS(num: Int, index: Int) {
        if index == n {
            if num == target {
                answer += 1
            }
            return
        }
        DFS(num: num + numbers[index], index: index + 1)
        DFS(num: num - numbers[index], index: index + 1)
    }
    DFS(num: 0, index: 0)

    return answer
}
```

<br/>

[BFS]

```swift
import Foundation

func solution(_ numbers:[Int], _ target:Int) -> Int {
    // LinkedQueue, DoubleStackQueue
    var queue = EffectiveQueue<(Int, Int)>()
    queue.enqueue((0,0))
    let n = numbers.count
    var answer = 0
    while !queue.isEmpty {
        let element = queue.dequeue()!
        let num = element.0
        let index = element.1
        if index == n {
            if num == target {
                answer += 1
            }
            continue
        }
        queue.enqueue((num + numbers[index], index + 1))
        queue.enqueue((num - numbers[index], index + 1))
    }
    return answer
}
```

<br/>

[EffectiveQueue](https://github.com/Gobans/Swift-Algorithm/blob/main/SwiftAlgorithm/DataStrcutre/EffectiveQueue.swift)

μ΄ μ½λλ [μ΄κ³³](https://one10004.tistory.com/247) μμ μμ±λ μ½λμλλ€.

[LinkedQueue](https://github.com/Gobans/Swift-Algorithm/blob/main/SwiftAlgorithm/DataStrcutre/LinkedQueue.swift)

μ΄ μ½λλ [μ΄κ³³](https://nitinagam17.medium.com/data-structure-in-swift-queue-part-5-985601071606) μμ μμ±λ μ½λμλλ€.

[DoubleStackQueue](https://github.com/Gobans/Swift-Algorithm/blob/main/SwiftAlgorithm/DataStrcutre/DoubleStackQueue.swift)

μ΄ μ½λλ [μ΄κ³³](https://trumanfromkorea.tistory.com/37) μμ μμ±λ μ½λμλλ€.

<br/>

## 4. νμ΄ κ³Όμ 

κ°λ¨νκ² μ«μλ€μ DFS/BFS λ‘ νμνλ μ½λλ₯Ό κ΅¬ννλ©΄ λλ λ¬Έμ μλ€.

λλ BFSλ‘ λ¬Έμ λ₯Ό λ¨Όμ  νμλλ° μκ°μ΄κ³Όκ° λ¬λ€..!

<br/>

κ·Έλ¦¬κ³  λμ DFSλ‘ νμλλ°, μκ°μ΄κ³Όκ° λμ§ μμλ€.

μ΄μν΄μ μμΈμ§ μ°Ύμλ΄€λλ°..

<br/>

```swift
removeFirst()
```

μ΄ λͺλ Ήμ΄ λλ¬Έμ΄μλ€.

!!!!

λλ§ μ΄ λͺλ Ήμ΄ O(1)μΈμ€ μκ³  μμλ..

<br/>

λ¬΄νΌ

λ€λ₯Έ λ°©μμΌλ‘ κ΅¬νλ queueλ₯Ό μ¬μ©ν΄μ μ€νν΄λ³΄λ ν΅κ³Όνλ€.

λ΄κ° μ¨λ³Έ queueλ `EffectiveQueue`, `LinkedQueue`, `DoubleStackQueue`

μΈλ° κ°κ°μ μκ° ν¨μ¨μ΄ λ¬λλ€.

<br/>

|<center>[EffectiveQueue](https://github.com/Gobans/Swift-Algorithm/blob/main/SwiftAlgorithm/DataStrcutre/EffectiveQueue.swift)<center/>|<center>[DoubleStackQueue](https://github.com/Gobans/Swift-Algorithm/blob/main/SwiftAlgorithm/DataStrcutre/DoubleStackQueue.swift)<center/>|<center>[LinkedQueue](https://github.com/Gobans/Swift-Algorithm/blob/main/SwiftAlgorithm/DataStrcutre/LinkedQueue.swift)<center/>|
| :---: | ---: | ---: | 
|![EffectiveQueue.png](EffectiveQueue.png)|![DoubleStackQueue.png](DoubleStackQueue.png)|![LinkedQueue.png](LinkedQueue.png)|

EffectiveQueue > LinkedQueue > DoubleStackQueue μμΌλ‘ λΉ¨λλλ° κ·Έ μ΄μ λ κ°κ° λ€μκ³Ό κ°λ€κ³  μκ°νλ€.

<br/>

    1. LinkedQueue: enqueue λ§λ€ Nodeλ₯Ό λ§λ€κΈ° λλ¬Έμ λ©λͺ¨λ¦¬ ν λΉμ΄ κ³μ μΌμ΄λλ€. μ΄ λλ¬Έμ μκ°μ΄ λλ €μ§λ€.
    2. DoubleStackQueue: inbox -> outboxλ‘ μ?κ²¨κ° λ μλ‘­κ² λ©λͺ¨λ¦¬κ° ν λΉλλ©΄μ λλ €μ§λ€.
    3. EffectiveQueue: λ©λͺ¨λ¦¬ κ³΅κ° νλ³΄λ₯Ό μν΄ removeFirst() λ©μλλ₯Ό μ¬μ©νμ§λ§, headλ₯Ό μμ§μ¬μ κ°μ λ°ννκΈ° λλ¬Έμ dequeue() λ©μλμμ μλ‘μ΄ λ©λͺ¨λ¦¬ ν λΉμ΄ νμμλ€.

<br/>

κ·Έλ°λ° λ©λͺ¨λ¦¬ ν λΉμ΄ μ΄λ κ² μκ°μ°¨μ΄λ₯Ό λ§μ΄ λ΄λ??

ν ..

μ΄μ¨λ .. nodeκ° λ§€λ² νμλ§λ€ λ§μ΄ μ¦κ°νλ€λ©΄ `removeFirst()` μ¬μ©μ μ§μν΄μΌκ² λ€.

<br/>


```toc

```
