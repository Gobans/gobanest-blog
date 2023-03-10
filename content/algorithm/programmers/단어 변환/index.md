---
emoji: ๐งถ
title: '[ํ๋ก๊ทธ๋๋จธ์ค] ๋จ์ด ๋ณํ'
date: '2023-02-04 00:00:00'
author: ๊ณ ๋ฐ
tags: ์๊ณ ๋ฆฌ์ฆ
categories: Algorithm
---

## 1. ๋ฌธ์ 

`ํ๋ก๊ทธ๋๋จธ์ค`

[๊ณ ๋์  Kit ๋จ์ด ๋ณํ](https://school.programmers.co.kr/learn/courses/30/lessons/43163?language=swift)


<br/>

## 2. ํต์ฌ ์์ด๋์ด

`DFS` `BFS`

<br/>

## 3. ์ฝ๋

[DFS]
```swift
import Foundation

func solution(_ begin:String, _ target:String, _ words:[String]) -> Int {
    var isVisited: [Bool] = Array(repeating: false, count: words.count)
    var minCnt = 52
    func DFS(nowWord: String, cnt: Int, isVisited: [Bool]) {
        if nowWord == target {
            if cnt < minCnt {
                minCnt = cnt
            }
            return
        }
        if cnt >= minCnt {
            return
        }
        var cVisited = isVisited
        for i in 0..<words.count {
            if !isVisited[i] && isPossibleChange(lhs: nowWord, rhs: words[i]) {
                cVisited[i] = true
                DFS(nowWord: words[i], cnt: cnt + 1, isVisited: cVisited)
                cVisited[i] = false
            }
        }
    }
    DFS(nowWord: begin, cnt: 0, isVisited: isVisited)
    return minCnt == 52 ? 0 : minCnt
}

func isPossibleChange(lhs: String, rhs: String) -> Bool {
    var lhs = Array(lhs)
    var rhs = Array(rhs)
    var cnt = 0
    for i in 0..<lhs.count {
        if lhs[i] != rhs[i] {
            cnt += 1
            if cnt == 2 {
                return false
            }
        }
    }
    return true
}

```

[BFS]

```swift
struct WordInfo {
    let word: String
    let cnt: Int
    let isVisited: [Bool]
}

func solution(_ begin:String, _ target:String, _ words:[String]) -> Int {
    let isVisited: [Bool] = Array(repeating: false, count: words.count)
    var minCnt = 52
    var queue: [WordInfo] = []
    queue.append(WordInfo(word: begin, cnt: 0, isVisited: isVisited))
    while !queue.isEmpty {
        let wordInfo = queue.removeFirst()
        if wordInfo.word == target {
            if wordInfo.cnt < minCnt {
                minCnt = wordInfo.cnt
            }
            continue
        }
        if wordInfo.cnt >= minCnt {
            continue
        }
        var cVisited = wordInfo.isVisited
        for i in 0..<words.count {
            if !wordInfo.isVisited[i] && isPossibleChange(lhs: wordInfo.word, rhs: words[i]) {
                cVisited[i] = true
                queue.append(WordInfo(word: words[i], cnt: wordInfo.cnt + 1, isVisited: cVisited))
                cVisited[i] = false
            }
        }
    }
    return minCnt == 52 ? 0 : minCnt
}

func isPossibleChange(lhs: String, rhs: String) -> Bool {
    print("lhs: \(lhs) -> rhs: \(rhs)")
    let lhs = Array(lhs)
    let rhs = Array(rhs)
    var cnt = 0
    for i in 0..<lhs.count {
        if lhs[i] != rhs[i] {
            cnt += 1
            if cnt == 2 {
                return false
            }
        }
    }
    return true
}

```

<br/>

## 4. ํ์ด ๊ณผ์ 

๋ค์๊ณผ ๊ฐ์ด ํ๋ฉด ๋๊ฒ ๋ค๊ณ  ์๊ฐํ๋ค.

    ๋ฐ๊ฟ ์ ์๋ ๋จ์ด (๋ฐ๊พธ๋ cost ๊ฐ 1 ์ดํ์ธ ์ํ๋ฒณ)๋ฅผ ์ฐพ์ ํ BFS or DFS

์ฐ์  DFS๋ก์ ๊ตฌํ์ด ์ฌ์ธ ๊ฒ ๊ฐ์์ ๋จผ์  ๊ตฌํํ๊ณ , ๋ค์์ BFS๋ก ๊ตฌํํ๋ค.

์ฑ๋ฅ์ ํฐ ์ฐจ์ด ์์ ๊ฒ ๊ฐ๋ค. 

์ต์ cnt๋ฅผ ์กฐ๊ฑด์ผ๋ก ๋น๊ตํ๋ ์กฐ๊ฑด์ ๋ ๋ฐฉ๋ฒ ๋ชจ๋ ์๊ธฐ ๋๋ฌธ์, ๊ฒฐ๊ตญ ์ต์ cnt ๋ฅผ ์ฐพ๊ธฐ์ํด์ ํ์ํ๋ ์์ ๋น์ทํ๋ค.

<br/>


```toc

```
