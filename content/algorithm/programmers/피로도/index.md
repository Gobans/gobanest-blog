---
emoji: π§Ά
title: '[νλ‘κ·Έλλ¨Έμ€] νΌλ‘λ'
date: '2023-01-15 00:00:00'
author: κ³ λ°
tags: μκ³ λ¦¬μ¦
categories: Algorithm
---

## 1. λ¬Έμ 

`νλ‘κ·Έλλ¨Έμ€`

[κ³ λμ  Kit νΌλ‘λ](https://school.programmers.co.kr/learn/courses/30/lessons/87946)


<br/>

## 2. ν΅μ¬ μμ΄λμ΄

`μμ νμ` `μμ΄` `DFS` 

<br/>

## 3. μ½λ

[μμ΄]
```swift
import Foundation

func solution(_ k:Int, _ dungeons:[[Int]]) -> Int {
    let dungeonPermutaion = permutation(dungeons, dungeons.count)
    var maxEnterTimes = 0
    for dungeonList in dungeonPermutaion {
        var userFatigue = k
        var enterTimes = 0
        for dungeon in dungeonList {
            let enterFatigue = dungeon[0]
            let consumeFatigue = dungeon[1]
            if userFatigue >= enterFatigue {
                userFatigue -= consumeFatigue
                enterTimes += 1
            }
        }
        if enterTimes > maxEnterTimes {
            maxEnterTimes = enterTimes
        }
    }
    return maxEnterTimes
}

```

[DFS]
```swift
import Foundation

func solution(_ k:Int, _ dungeons:[[Int]]) -> Int {
    let visited = Array(repeating: false, count: dungeons.count)
    var maxDepth = 0
    func DFS(visited: [Bool], fatigue: Int, depth: Int) {
        if depth > maxDepth {
            maxDepth = depth
        }
        for i in 0..<dungeons.count {
            let enterFatigue = dungeons[i][0]
            let consumeFatigue = dungeons[i][1]
            if !visited[i] && fatigue >= enterFatigue {
                var cVisited = visited
                cVisited[i] = true
                DFS(visited: cVisited, fatigue: fatigue - consumeFatigue, depth: depth + 1)
            }
        }
    }
    DFS(visited: visited, fatigue: k, depth: 0)
    return maxDepth
}
```

<br/>

## 4. νμ΄ κ³Όμ 

μ²μμλ λ€μκ³Ό κ°μ΄ μκ°νμ¬ μ λ¦¬νμλ€.

νμμ¬ν­:

     μ΅μ νμ νΌλ‘λ: λμ  ννμ μν νΌλ‘λ
     μλͺ¨ νΌλ‘λ: λμ  νν ν μλͺ¨λλ νΌλ‘λ
     μ μ κ° ννν  μ μλ μ΅λ λμ  μ

- μ°μ  μ λλ κ²: μλͺ¨ νΌλ‘λκ° λ?μ κ².
    - μλͺ¨ νΌλ‘λ 1μμ, μ΅μ νμ νΌλ‘λ 2μμλ‘ μ λ ¬.
    - μ νμ ν΄λκ°λ©΄μ κ°λ₯ν λμ  νμ.

μ΄λ°μμΌλ‘ μ λ ¬μ μ¬μ©ν΄μ λ¬Έμ λ₯Ό νλ©΄ μ΄λ¨κΉ μκ°μ νμλλ°,

μκ°ν΄λ³΄λ μ΄λ κ² νλ©΄ λμ μ λ°©λ¬Ένλ `μμ`λ₯Ό μ»€λ²ν  μκ° μμ΄μ, νλ¦¬κ² λλ€.

<br/>

κ·Έλμ `μμ΄`λ‘ λμ μ λ°©λ¬Ένλ λͺ¨λ  μμλ₯Ό κ΅¬ν΄μ νμνλ κ²μ μκ°νκ³ , ν΄λΉ μ½λκ° μμ μλ€.

κ·Έλ°λ° μ΄λ κ² νλ©΄ λͺ¨λ  κ²½μ°μ μλ₯Ό λ€ νμμ νλκ±°λΌ μλΉν λΉν¨μ¨μ  μΌ κ²μ΄λΌ μκ°νλ€.

κ·Έλμ `DFS` λ‘ λ€μ νλ² νμ΄λ³΄κ³  νμ€νΈ νλ€. 

|<center>μμ΄<center/>|<center>DFS<center/>|
| :---: | ---: | 
|![permutation.png](permutation.png)|![DFS.png](DFS.png)|

μ°¨μ΄κ° μμ²­λλ€!!

μμ΄μ μ λ§ μ΄μ© μ μμ λ μ¬μ©νμ..

<br/>

κ·Έλ¦¬κ³  λ νλ λ°κ²¬ν κ²μ΄ `enumerated` μ κ΄ν κ²μΈλ°,

μ κ° μμ²­λ μκ°μ μ‘μλ¨Ήλλ€λ κ²μ μ΄λ²μ λ°κ²¬νλ€.

|<center>DFS Enumerated<center/>|<center>DFS<center/>|
| :---: | ---: | 
|![DFSEnumerated.png](DFSEnumerated.png)|![DFS.png](DFS.png)|

λ³΄λ€μνΌ νμ€νΈ 8λ²μμ 134 -> 40 μ΄λΌλ μμ²­λ μ°¨μ΄κ° μλ€.

μλνλ©΄ Enumerated λ©μλκ° for λ¬ΈμΌλ‘ νμνλ μμλ₯Ό λ§΅ν νμ¬ i λ₯Ό μμ±νκΈ° λλ¬Έμ `O(N)` μ μκ°μ κ°μ§λ€κ³  νλ€..

Enumerated μκ³ λ¦¬μ¦ νλ μ§μνμ.

<br/>

μ΄κ±Έ μ΄λ»κ² μκ² λλλ©΄, λ€λ₯Έμ¬λ μ½λλ₯Ό νμ€νΈ ν΄λ³΄λ©΄μ μ€νμλλ₯Ό λ΄€λλ° λμ μ°¨μ΄κ° λ§μ΄ λμ λ­κ° μΆμ΄μ λ΄€λλ Enumerated μ°¨μ΄κ° μμλ κ²μ λ°κ²¬νλ€.

μ΄μ’κ² μ΄ μ¬μ€μ μκ²λμλ€!


<br/>


```toc

```