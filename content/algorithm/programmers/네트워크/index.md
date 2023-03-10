---
emoji: ๐งถ
title: '[ํ๋ก๊ทธ๋๋จธ์ค] ๋คํธ์ํฌ'
date: '2023-02-03 00:00:00'
author: ๊ณ ๋ฐ
tags: ์๊ณ ๋ฆฌ์ฆ
categories: Algorithm
---

## 1. ๋ฌธ์ 

`ํ๋ก๊ทธ๋๋จธ์ค`

[๊ณ ๋์  Kit ๋คํธ์ํฌ ](https://school.programmers.co.kr/learn/courses/30/lessons/43162)


<br/>

## 2. ํต์ฌ ์์ด๋์ด

`DFS` `BFS`

<br/>

## 3. ์ฝ๋

[DFS]
```swift
func solution(_ n:Int, _ computers:[[Int]]) -> Int {
    var connectMap: [[Int]] = Array(repeating: Array(repeating: 0, count: n), count: n)
    var isVisited: [Bool] = Array(repeating: false, count: n)
    var cnt = 0
    for i in 0..<n {
        for j in 0..<n {
            if computers[i][j] == 1 {
                connectMap[i][j] = 1
            }
        }
    }
    func DFS(node: Int) {
        for idx in 0..<n  {
            if !isVisited[idx] && connectMap[node][idx] == 1 {
                isVisited[idx] = true
                DFS(node: idx)
            }
        }
    }
    for i in 0..<n {
        if !isVisited[i] {
            isVisited[i] = true
            cnt += 1
            DFS(node: i)
        }
    }
    return cnt
}
```

[BFS]
```swift
func solution(_ n:Int, _ computers:[[Int]]) -> Int {
    var connectMap: [[Int]] = Array(repeating: Array(repeating: 0, count: n), count: n)
    var isVisited: [Bool] = Array(repeating: false, count: n)
    var cnt = 0
    for i in 0..<n {
        for j in 0..<n {
            if computers[i][j] == 1 {
                connectMap[i][j] = 1
            }
        }
    }
    var queue: [Int] = []
    for i in 0..<n {
        if !isVisited[i] {
            queue.append(i)
            cnt += 1
            isVisited[i] = true
            while !queue.isEmpty {
                let node = queue.removeFirst()
                for k in 0..<n {
                    if !isVisited[k] && connectMap[node][k] == 1 {
                        isVisited[k] = true
                        queue.append(k)
                    }
                }
            }
        }
    }
    return cnt
}
```

<br/>

## 4. ํ์ด ๊ณผ์ 

๋ฌธ์ ๋ฅผ ๋ณด๊ณ  ๋ค์๊ณผ ๊ฐ์ด ์๊ฐํ๋ค.

    1. 2์ฐจ์ ๋ฐฐ์ด๋ก, ํด๋น ๋ธ๋์ ์ฐ๊ฒฐ๋ ๋ธ๋๋ฅผ 1๋ก ํํํจ
    2. ๋ธ๋์ ๋ฐฉ๋ฌธ์ ๋ํ๋ด๋ ๋ฐฐ์ด์ ํ๋ ๋ง๋ค์ด ์ํ.
    3. ๋ฐ๋ณต๋ฌธ์ผ๋ก ๋ธ๋๋ฅผ ๋ฐฉ๋ฌธํ๋์ง DFS/BFS ๋ก ํ์ธ.
    4. ๋ฐฉ๋ฌธํ ๋ธ๋๋ฅผ ์๋ฐ์ดํธ.

์ด ๋ฌธ์ ๋ฅผ ํผ ๊ธฐ์ต์ด ํฌ๋ฏธํ๊ฒ ์์๋ค.. ์๋ง ์์ ์ ํ๋ฒ ํ์์ด์ ์ฝ๊ฒ ํ์ด๊ฐ ๋ ์ค๋ฅธ ๊ฒ ๊ฐ๋ค.

<br/>

ํด๋น ํ๋ก์ฐ๋ก ์ฝ๋๋ฅผ ์์ฑํ์๋ค! 

์ฒ์์๋ DFS๋ก ๊ตฌํ์ ํ์๊ณ  BFS๋ก๋ ๊ตฌํ ํด๋ณด์๋ค.


<br/>


```toc

```
