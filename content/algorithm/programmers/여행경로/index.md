---
emoji: ๐งถ
title: '[ํ๋ก๊ทธ๋๋จธ์ค] ์ฌํ๊ฒฝ๋ก'
date: '2023-02-05 00:00:00'
author: ๊ณ ๋ฐ
tags: ์๊ณ ๋ฆฌ์ฆ
categories: Algorithm
---

## 1. ๋ฌธ์ 

`ํ๋ก๊ทธ๋๋จธ์ค`

[๊ณ ๋์  Kit ์ฌํ๊ฒฝ๋ก](https://school.programmers.co.kr/learn/courses/30/lessons/43164)


<br/>

## 2. ํต์ฌ ์์ด๋์ด

`DFS`

<br/>

## 3. ์ฝ๋

```swift

import Foundation

func solution(_ tickets:[[String]]) -> [String] {
    var flightDict: [String: Int] = [:]
    var flightSet = Set<String>()
    for ticket in tickets {
        ticket.forEach { flight in
            flightSet.insert(flight)
        }
    }
    let sortedFlightSet = flightSet.sorted(by: <)
    var flightIndexCnt = 0
    for flight in sortedFlightSet {
        flightDict[flight] = flightIndexCnt
        flightIndexCnt += 1
    }
    var flightMap: [[Int]] = Array(repeating: Array(repeating: 0, count: sortedFlightSet.count), count: sortedFlightSet.count)
    for ticket in tickets {
        let departFlightIndex = flightDict[ticket[0]]!
        let arriveFlightIndex = flightDict[ticket[1]]!
        flightMap[departFlightIndex][arriveFlightIndex] += 1
    }
    let flightCnt = sortedFlightSet.count
    let depth = tickets.count
    var targetSearched = false
    var answerTravelCourse: [String] = []
    func DFS(departFlightIndex: Int, travelCourse: [String], usedTicketCnt: Int) {
        if usedTicketCnt == depth {
            targetSearched = true
            answerTravelCourse = travelCourse
            return
        }
        var travelCourse = travelCourse
        for i in 0..<flightCnt {
            if !targetSearched && flightMap[departFlightIndex][i] >= 1 {
                travelCourse.append(sortedFlightSet[i])
                flightMap[departFlightIndex][i] -= 1
                DFS(departFlightIndex: i, travelCourse: travelCourse, usedTicketCnt: usedTicketCnt + 1)
                flightMap[departFlightIndex][i] += 1
                travelCourse.removeLast()
            }
        }
    }
    DFS(departFlightIndex: flightDict["ICN"]!, travelCourse: ["ICN"], usedTicketCnt: 0)
    return answerTravelCourse
}
```

<br/>

## 4. ํ์ด ๊ณผ์ 

ํ์๋ฌธ์ ์ธ๋ฐ, ํน์ดํ๊ฒ ์ํ๋ฒณ ์ฌ์ ์์ผ๋ก ์ ๋ ฌ๋ ๊ฒฝ๋ก๋ฅผ ์ถ๋ ฅํด์ผํ๋ค.

๋ค์๊ณผ ๊ฐ์ด ์ฝ๋ ํ๋ก์ฐ๋ฅผ ์๊ฐํ์๋ค.

    1. ํญ๊ณต๊ถ์ด ๊ฐ ์ ์๋ ๊ฒฝ๋ก๋ฅผ 2์ฐจ์ ๋ฐฐ์ด๋ก ๋ํ๋.
    2. ๋จ์ด๋ง๋ค ๋์๋๋ฆฌ์ ์ ์ฅํ์ฌ, ์ธ๋ฑ์ค๋ฅผ ํด์ฑํจ. (set ์ผ๋ก ๋ฏธ๋ฆฌ ์ค๋ณต ์ ๊ฑฐ ํ ์ ๋ ฌํ๊ณ , ๋์๋๋ฆฌ ์์ฑ)
    3. ํญ๊ณต๊ถ ๊ฒฝ๋ก๋๋ก 2์ฐจ์ ๋ฐฐ์ด ์ฑ์ฐ๊ธฐ
    4. ์ฑ์์ง ํญ๊ณต๊ถ ๊ฒฝ๋ก๋๋ก DFS ํ, return

์ด๋ ๊ฒ ํ์๊ณ , ํ์คํธ ์ผ์ด์ค๋ ๋ฌด๋ํ ํต๊ณผํ๊ธธ๋ ์ ๋ต์ธ์ค ์์๋ค.

๊ทธ๋ฐ๋ฐ **ํ์คํธ ์ผ์ด์ค 1๋ฒ** ์์ ์คํจํ๋ค. (2,3,4 ๋ชจ๋ ํต๊ณผ)

<br/>

์ด์ ๊ฐ ๋ญ๊ฐ ๋ณด๋, ๋๋ ํญ๊ณต๊ถ์ผ๋ก ๊ฐ ์ ์๋ ๊ฒฝ๋ก๋ฅผ ๋ํ๋ธ 2์ฐจ์ ๋ฐฐ์ด์ [[Bool]] ๋ก ์ฌ์ฉํด์ ์ผ๋๋ฐ, ์ด ๋ ๊ฒฝ๋ก๊ฐ ๊ฐ์ ํญ๊ณต๊ถ์ด ์ฌ๋ฌ๊ฐ ์ค๋ณต์ผ๋ก ์์๊ฒฝ์ฐ, ํด๋น ์ํฉ์ ๋ํ๋ด์ง ๋ชปํด์ ์คํจํ๋ ๊ฒ์ด์๋ค.

๊ทธ๋์ ํด๋น 2์ฐจ์ ๋ฐฐ์ด์ [[Int]]๋ก ๋ฐ๊พธ๋ฉด ํญ๊ณต๊ถ์ด ์ค๋ณต์ผ๋ก ์กด์ฌํ๋ ๊ฒฝ์ฐ ์ซ์๋ก ํํ์ด ๊ฐ๋ฅํ๋ค.

์ด๋ ๊ฒ ๋ฐ๊ฟ์ ๋ฌธ์ ๋ฅผ ํต๊ณผํ๋ค!

<br/>

`BFS` ๋ ๋ฌธ์ ์ ์ํฉ๊ณผ ๋ง์ง ์๋ ์๊ณ ๋ฆฌ์ฆ์ด๋ผ ์๊ฐํด์ ๋ฐ๋ก ๊ตฌํํ์ง ์์๋ค. ์ฌํ ์์๋ฅผ ์ด๋ฏธ ์ ๋ ฌ๋ก ์ด๋์ ๋ ์ ํ๋๋ฐ BFS ๋ก ํ์ํ์ฌ ๋ฃจํธ๋ฅผ ์ฐพ๋ ๊ฒ์ ๋นํจ์จ์ ์ด๋ค. ์ฐพ๊ธด ์ฐพ๊ฒ ์ง๋ง.. ์ค๋ ๊ฑธ๋ฆด ๊ฒ์ด๋ค.

<br/>


```toc

```
