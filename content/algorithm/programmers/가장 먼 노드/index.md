---
emoji: ๐งถ
title: '[ํ๋ก๊ทธ๋๋จธ์ค] ๊ฐ์ฅ ๋จผ ๋ธ๋'
date: '2023-02-16 00:00:00'
author: ๊ณ ๋ฐ
tags: ์๊ณ ๋ฆฌ์ฆ
categories: Algorithm
---

## 1. ๋ฌธ์ 

`ํ๋ก๊ทธ๋๋จธ์ค`

[๊ณ ๋์  Kit ๊ฐ์ฅ ๋จผ ๋ธ๋](https://school.programmers.co.kr/learn/courses/30/lessons/49189?language=swift)


<br/>

## 2. ํต์ฌ ์์ด๋์ด

`DFS`

<br/>

## 3. ์ฝ๋

```swift
import Foundation

func solution(_ n:Int, _ edge:[[Int]]) -> Int {
    var graph = Array(repeating: [Int](), count: n + 1)
    var isVisited = Array(repeating: false, count: n + 1)
    edge.forEach{ graph[$0[0]].append($0[1]);graph[$0[1]].append($0[0]) }
    
    var currentNodes:Set = [1]
    var nodeCnt = 0
    while !currentNodes.isEmpty {
        var nodes = Set<Int>()
        var isStepIn = false
        currentNodes.forEach{ isVisited[$0] = true }
        for node in currentNodes {
            for number in graph[node] {
                if !isVisited[number] {
                    if !isStepIn {
                        isStepIn = true
                        nodeCnt = 0
                    }
                    isVisited[number] = true
                    nodes.insert(number)
                    nodeCnt += 1
                }
            }
        }
        currentNodes = nodes
    }
    return nodeCnt
}
```

<br/>

## 4. ํ์ด ๊ณผ์ 

๊ฐ์ฅ ๋ฉ๋ฆฌ์๋ ๋ธ๋๊ฐ ๋ช๊ฐ์ธ์ง ๊ตฌํ๋ ๋ฌธ์ ์ธ๋ฐ, ์ฒ์์๋ ์ฝ๋ค๊ณ  ์๊ฐํ๋ค.

์ฐ์  ์ฒ์์ ๋ฌธ์ ๋ฅผ ํ๋ ์ฐ๊ฒฐ๋ ์ ์ ๊ทธ๋ํ๋ก ๋ง๋ค์ด BFS๋ก ํ์ํ๋ ค๊ณ  ํ๋ค.

<br/>

```swift
func solution(_ n:Int, _ edge:[[Int]]) -> Int {
    // ๊ฐ์ ์ ๋ฐ๋ผ ํ์ (BFS)
    var graph = Array(repeating: Array(repeating: 0, count: n + 1), count: n + 1)
    var isVisited = Array(repeating: false, count: n + 1)
    for i in 0..<edge.count {
        let e = edge[i]
        graph[e[0]][e[1]] = 1
        graph[e[1]][e[0]] = 1
    }
    var farNodeDepth = 0
    var farNodeCnt = 0
    var queue: [(Int, Int)] = []
    queue.append((1,0))
    isVisited[1] = true
    while !queue.isEmpty {
        let (num, depth) = queue.removeFirst()
        if farNodeDepth < depth {
            farNodeDepth = depth
            farNodeCnt = 1
        } else {
            farNodeCnt += 1
        }
        for i in 1...n {
            if !isVisited[i] && graph[num][i] == 1 {
                isVisited[i] = true
                queue.append((i, depth + 1))
            }
        }
    }
    return farNodeCnt
}
```

<br/>

ํ์ง๋ง ์ด๋ ๊ฒ ํ๋ฉด graph ์์ฒด๊ฐ ๋งค์ฐ ํด๋ graph ํ๋์ ๋ผ์ธ์ n ๋งํผ ๊ณ์ ๋ฐ๋ณตํด์ค์ผํ๊ธฐ ๋๋ฌธ์ ์๊ฐ ๋ณต์ก๋๊ฐ ์ปค์ ธ์ ๋ฌธ์ ์ ํต๊ณผํ  ์ ์๋ค.

<br/>

ํด๋ต์ ๊ทธ๋ํ๋ฅผ ์ฐ๊ฒฐ๋ ๊ฐ์ ์ผ๋ก๋ง ๋ง๋ค์ด์ ํ์ํ๋ ๊ฒ์ด์๋ค.

ํด๋น ํ์ด๋ [์ด๊ณณ](https://fomaios.tistory.com/entry/Swift-ํ๋ก๊ทธ๋๋จธ์ค-๊ฐ์ฅ-๋จผ-๋ธ๋)์ ์ฐธ๊ณ ํ์๋ค.

<br/>

๊ทธ๋ฐ๋ฐ ์ด ํ์ด์์๋ ์ค๋ณต๊ฐ์ ์ ๊ฑฐํ๊ธฐ์ํด Node๋ฅผ ๋ด๋ ๋ฐฐ์ด์ Set์ ์ฌ์ฉํ์๋ค ํ๋๋ฐ, ์ฌ์ค์ isVisited ๋ฐฐ์ด์ด ์ค๋ณต์ ์ฒดํนํด์ฃผ๊ณ  ์์ด์ ์ค๋ณต๊ฐ์ด ๋ค์ด๊ฐ์ผ์ ์๋ค.

<br/>

|<center>[Set]()<center/>|<center>[Array]()<center/>|
| :---: | ---: |
|![Set.png](Set.png)|![Array.png](Array.png)|

<br/>

๋ค๋ง ์๊ฐ์ด์์ ์ ์๋ฏธํ ์ฐจ์ด๊ฐ ๋ฐ์ํด์ Set ๊ณผ Array์ iteration ์๋๋ฅผ ํ๋ฒ ์คํ์ผ๋ก ์ธก์ ํด๋ดค๋ค.

[Array์ Set์ ์๋ ์ฐจ์ด](https://gobanest.com/swift/[Swift]%20Array์%20Set/)


<br/>


```toc

```
