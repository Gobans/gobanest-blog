---
emoji: π§Ά
title: '[νλ‘κ·Έλλ¨Έμ€] μ΄μ€μ°μ μμν'
date: '2023-01-06 00:00:00'
author: κ³ λ°
tags: μκ³ λ¦¬μ¦
categories: Algorithm
---

## 1. λ¬Έμ 

`νλ‘κ·Έλλ¨Έμ€`

[κ³ λμ  Kit μ΄μ€μ°μ μμν](https://school.programmers.co.kr/learn/courses/30/lessons/42628)


<br/>

## 2. ν΅μ¬ μμ΄λμ΄

`heap` `μ λ ¬`

<br/>

## 3. μ½λ

[swift]
```swift
import Foundation


func solution(_ operations:[String]) -> [Int] {
    var maxHeap = Heap { (lhs: Int, rhs:Int) in
        return lhs > rhs
    }
    var minHeap = Heap { (lhs: Int, rhs:Int) in
        return lhs < rhs
    }
    
    for operation in operations {
        let trimedOperation = operation.components(separatedBy: " ")
        let command = trimedOperation[0]
        let paramater = trimedOperation[1]
        switch command {
        case "I":
            maxHeap.insert(Int(paramater)!)
            minHeap.insert(Int(paramater)!)
        case "D":
            if paramater == "1" {
                guard let element = maxHeap.remove() else { break }
                if let index = minHeap.index(of: element, startingAt: 0) {
                    minHeap.remove(at: index)
                }
            }
            if paramater == "-1" {
                guard let element = minHeap.remove() else { break }
                if let index = maxHeap.index(of: element, startingAt: 0) {
                    maxHeap.remove(at: index)
                }
            }
        default: break
        }
    }
    if minHeap.isEmpty && maxHeap.isEmpty {
        return [0,0]
    }
    return [maxHeap.remove()!,minHeap.remove()!]
}

```

<br/>

## 4. νμ΄ κ³Όμ 

λ¬Έμ μμ μ½μ, μ΅λκ° μ­μ , μ΅μκ° μ­μ  μΈκ°μ μ°μ°μ λ°λ³΅νκΈ° λλ¬Έμ, μ΅μ μ΅λ `heap` λκ°λ₯Ό λ§λ€μ΄ κ°κ° μ¬μ©μ νλ©΄ λ¬Έμ κ° νλ¦΄ κ² κ°μμ κ·Έλλ‘ κ΅¬ννμλ€.

λ€λ§ ν¨μ©μ΄ λ¨μ΄μ Έ μκ°μ΄κ³Όλ  κ²μ μμνμ§λ§ μΌλ¨ κ΅¬ν ν κ°μ μ μ μ°ΎμΌλ € νμλλ°, μκ°μ΄λ λ¬Έμ μμ νμ€νμ νμ§ μμκ³ , κ·Έλμ μ½κ² ν΅κ³Όλ₯Ό ν κ² κ°λ€.

<br/>

## 5. λ€λ₯Έ μ¬λμ μ½λ

[swift]
```swift
import Foundation

func solution(_ operations:[String]) -> [Int] {
    var items:[Int] = []


        for i in 0..<operations.count {

            let ii = operations[i].components(separatedBy: " ")

            if String(ii[0]) == "D" {
                if items.count > 0 {
                    items.remove(at: (Int(ii[1])! > 0 ? (items.count - 1) : 0))
                }

            }else if String(ii[0]) == "I"{
                items.append(Int(ii[1])!)
                items = items.sorted(by: {$0 < $1})
            }

        }

        items = items.sorted(by: {$0 < $1})

        var i:[Int] = [0,0]
        if items.count > 0 {
            i.removeAll()

            i.append(items.last!)
            i.append(items.first!)
        }
        return i
}

```

νλ‘κ·Έλλ¨Έμ€μ λ€λ₯Έ μ¬λμ μ½λλ₯Ό λ΄€λλ°, κ·Έλ₯ λ°°μ΄μ μ¬μ©ν΄μ νΌκ² λ§μλ€.

νμ€νΈμΌμ΄μ€ νμ€νμ λλ €λ³΄λ `heap` κ³Ό ν° μ°¨μ΄λ λμ§ μμλ€. (λ―ΈμΈνκ² heap μ΄ λ λΉ¨λλ€) 


<br/>


```toc

```
