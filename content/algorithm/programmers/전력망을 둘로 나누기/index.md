---
emoji: ๐งถ
title: '[ํ๋ก๊ทธ๋๋จธ์ค] ์ ๋ ฅ๋ง์ ๋๋ก ๋๋๊ธฐ'
date: '2023-01-17 00:00:00'
author: ๊ณ ๋ฐ
tags: ์๊ณ ๋ฆฌ์ฆ
categories: Algorithm
---

## 1. ๋ฌธ์ 

`ํ๋ก๊ทธ๋๋จธ์ค`

[๊ณ ๋์  Kit ์ ๋ ฅ๋ง์ ๋๋ก ๋๋๊ธฐ](https://school.programmers.co.kr/learn/courses/30/lessons/86971)


<br/>

## 2. ํต์ฌ ์์ด๋์ด

`์์  ํ์` `BFS` `DFS`

<br/>

## 3. ์ฝ๋

[BFS]
```swift
func solution(_ n:Int, _ wires:[[Int]]) -> Int {
    var minDiff = 100
    func BFS(towerGraph: [[Bool]]) {
        var visited = Array(repeating: false, count: n + 1)
        var stack: [Int] = []
        stack.append(1)
        visited[1] = true
        while !stack.isEmpty {
            let checkPoint = stack.removeLast()
            for i in 1...n {
                if !visited[i] && towerGraph[checkPoint][i] {
                    visited[i] = true
                    stack.append(i)
                }
            }
        }
        let firstTowers = visited.filter{ $0 == true }.count
        let secondTowers = n - firstTowers
        let diff = abs(firstTowers - secondTowers)
        if diff < minDiff {
            minDiff = diff
        }
    }
    for i in 0..<wires.count {
        var cWires = wires
        cWires.remove(at: i)
        let towerGraphLine = Array(repeating: false, count: n + 1)
        var towerGraph: [[Bool]] = Array(repeating: towerGraphLine, count: n + 1)
        for wire in cWires {
            let startPoint = wire[0]
            let endPoint = wire[1]
            towerGraph[startPoint][endPoint] = true
            towerGraph[endPoint][startPoint] = true
        }
        BFS(towerGraph: towerGraph)
    }

    return minDiff
}
```

<br/>

[DFS]
```swift
func solution(_ n:Int, _ wires:[[Int]]) -> Int {
    var minDiff = 100
    func DFS(towerGraph: [[Bool]], lineIndex: Int, visited: inout [Bool], towerCount: inout Int) {
        for i in 1...n {
            if !visited[i] && towerGraph[lineIndex][i] {
                visited[i] = true
                towerCount += 1
                DFS(towerGraph: towerGraph, lineIndex: i, visited: &visited, towerCount: &towerCount)
            }
        }
    }
    for i in 0..<wires.count {
        var cWires = wires
        cWires.remove(at: i)
        let towerGraphLine = Array(repeating: false, count: n + 1)
        var towerGraph: [[Bool]] = Array(repeating: towerGraphLine, count: n + 1)
        for wire in cWires {
            let startPoint = wire[0]
            let endPoint = wire[1]
            towerGraph[startPoint][endPoint] = true
            towerGraph[endPoint][startPoint] = true
        }
        var visited = Array(repeating: false, count: n + 1)
        var towerCount = 0
        DFS(towerGraph: towerGraph, lineIndex: 1, visited: &visited, towerCount: &towerCount)
        let secondTowers = n - towerCount
        let diff = abs(towerCount - secondTowers)
        if diff < minDiff {
            minDiff = diff
        }
    }

    return minDiff
}
```

<br/>

## 4. ํ์ด ๊ณผ์ 

๋ฌธ์ ๋ฅผ ๋ณด๊ณ  ๋ค์๊ณผ ๊ฐ์ด ์๊ฐํ๊ณ , ๊ตฌํด์ผํ  ๊ฒ์ ์๊ฐํ๋ค.

    1. ์ ์ ์ ํ๋ ๋์์ ๋ ํ๋์ ๊ฐ์ ์ด ๋ช๊ฐ ์ด์ด์ ธ์๋์ง ํ์ธ
    2. ์ ์ฒด ์ก์ ํ - ์ด์ด์ง ์ก์ ํ = ๋ ๋ค๋ฅธ ์ก์ ํ์ ๊ฐฏ์
    3. ๋๊ฐ์ ์ก์ ํ ๊ฐ์์ ์ฐจ์ด (์ ๋๊ฐ)


๊ทธ๋์ ์๊ฐํ๋ ๋ฐฉ์๋๋ก ์ ์ ์ ๋๊ณ , ๋์ ์ ์ ๋๋ก graph๋ฅผ ๋ง๋ค์ด์ ์ฌ์ฉํ์๋ค.

<br/>

์ฒซ๋ฒ์งธ๋ก ๊ทธ๋ํ๋ฅผ ํ์์ ์ํด ์ฌ์ฉํ ๋ฐฉ์์ `BFS` ์ธ๋ฐ, ์คํ์ ์ฌ์ฉํ์ฌ ์ฒซ๋ฒ์งธ ํ์์ ์ฐ๊ฒฐ๋ ๋ธ๋์ ๊ฐ์๋ฅผ ๊ตฌํ ํ, ์ ์ฒด ๊ฐ์์ ๋นผ์คฌ๋ค.

์ด๋ ๋ฌธ์ ์์ ์ก์ ํ์ด ์ ์ ์ ํตํด `ํ๋์ ํธ๋ฆฌ` ํํ๋ฅผ ์ด๋ฃจ๊ณ  ์๊ธฐ ๋๋ฌธ์ ๊ฐ๋ฅํ ๋ฐฉ์์ด์๋ค.

<br/>

๋๋ฒ์จฐ๋ก๋ `DFS` ์ผ๋ก ์ฌ๊ท๋ฅผ ํตํด ๊ตฌํํ์๋ค. ๊ตฌํ์ด ์ต์์น ์์, ์กฐ๊ธ ๋ง์ด ๋ฒ๋ฒ ๊ฑฐ๋ฆฌ๊ณ  ์ฝ๋๊ฐ ๊น๋ํ์ง ์๋ค๊ณ  ๋๊ผ๋ค. ํ๋จ์ ๋ค๋ฅธ ์ฌ๋์ด ๊ตฌํํ DFS ์ฝ๋๋ฅผ ๋ณด๊ณ  ์์ง ํ์ฐธ ๋ฉ์๊ตฌ๋ ๋๊ผ๋ค..!

<br/>


|<center>BFS<center/>|<center>DFS<center/>|
| :---: | ---: | 
|![BFS.png](BFS.png)|![DFS.png](DFS.png)|

๋์ ์ฝ๋์์๋ BFS ๊ฐ ์กฐ๊ธ ๋ ์ข์ ์ฑ๋ฅ์ ๋ณด์ฌ์คฌ๋ค. 

๊ตฌํํ๊ธฐ๋ ๋น๊ต์  ํธํ๊ณ , ๋ ์ต์ํด์ ๊ทธ๋ฐ์ง ์ฝ๋๋ฅผ ์ฝ๊ธฐ๋ ํธํ ๋๋์ด๋ค.

๋๋ ์์ ํ์์์๋ BFS ๊ฐ ๋ ์ข๋ค..!

<br/>

## 5. ๋ค๋ฅธ ์ฌ๋์ ์ฝ๋

```swift
import Foundation

func solution(_ n:Int, _ wires:[[Int]]) -> Int {
    var connection = Array(repeating: Array(repeating: false, count: n+1), count: n+1)
    wires.forEach {
        connection[$0[0]][$0[1]] = true
        connection[$0[1]][$0[0]] = true
    }

    func countNodes(from root: Int, visited: [Bool]) -> Int {
        var count = 0
        var visited = visited

        func dfs(n: Int) {
            visited[n] = true
            count += 1
            connection[n].enumerated()
                .filter { $0.element == true && visited[$0.offset] == false }
                .forEach {
                    dfs(n: $0.offset)
                }
        }
        dfs(n: root)

        return count
    }

    // ์์์ ๋ธ๋์์, ๊ทธ ๋ธ๋ํฌํจํด์ ์๋ธํธ๋ฆฌ์ ๋ธ๋ ๊ฐ์๋ฅผ ๊ตฌํ๋ค.
    var difference = Int.max
    var visited = Array(repeating: false, count: n+1)
    func travel(to node: Int) {
        visited[node] = true

        let subtreeA = countNodes(from: node, visited: visited)
        let subtreeB = n - subtreeA
        difference = min(difference, abs(subtreeA - subtreeB))


        connection[node].enumerated()
            .filter { $0.element == true && visited[$0.offset] == false }
            .forEach {
                travel(to: $0.offset)
            }
    }
    travel(to: 1)

    return difference
}

```

์ฝ๋๊ฐ ๊น๋ํ๊ณ  ์ฝ๊ธฐ ์ข์์ ๊ฐ์ ธ์๋ดค๋ค. ํ์์ ์ํ ๊ตฌ์กฐ (travel -> countNodes -> dfs) ๋ ๊น๋ํ๊ณ  ์ฌ๋ฌ๋ชจ๋ก ๋ณธ๋ฐ์๊ฒ ๋ง์ ์ฝ๋์๋ค.

ํน์ดํ ์ ์ `enumerated` ๋ฅผ ์ ํ์ฉํ ์ ์ด๋ค.

์ ๋ฒ์ ๋ด๊ฐ enumerated ๋ฅผ ์ง์ํ์๊ณ  ์ผ๋๋ฐ, ์ด๋ฐ์์ผ๋ก ๊ณง๋ฐ๋ก element์ offset์ ํ์ฉํ๋ฉด ์ง์ํ  ํ์์๊ณ , ์งํฅ์ ํด๋ ๋  ๊ฒ ๊ฐ๋ค.

๋ง์ด ๋ฐฐ์ ๋ค..!!

<br/>

|<center>other DFS<center/>|
| :---: |
|![otherDFS.png](otherDFS.png)|

์๊ฐ์ด๋ ๋ณด๋ฉด ํ์คํธ ์ผ์ด์ค 2๋ฒ ๋นผ๊ณ ๋ ์ฐ์ํ ์๋๋ฅผ ๋ณด์ด๋๋ฐ, ์๋ง `graph`๋ฅผ ์ฌ์์ฑ ํ์ง ์๊ธฐ ๋๋ฌธ์ ์กฐ๊ธ ๋ ์๊ฐ์ ์ด์ ์ด ์๋๊ฒ ์๋๊น ์๊ฐํ๋ค.

<br/>


```toc

```
