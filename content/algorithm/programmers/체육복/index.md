---
emoji: ๐งถ
title: '[ํ๋ก๊ทธ๋๋จธ์ค] ์ฒด์ก๋ณต'
date: '2023-01-19 00:00:00'
author: ๊ณ ๋ฐ
tags: ์๊ณ ๋ฆฌ์ฆ
categories: Algorithm
---

## 1. ๋ฌธ์ 

`ํ๋ก๊ทธ๋๋จธ์ค`

[๊ณ ๋์  Kit ์ฒด์ก๋ณต](https://school.programmers.co.kr/learn/courses/30/lessons/42862)


<br/>

## 2. ํต์ฌ ์์ด๋์ด

`๊ทธ๋ฆฌ๋`

<br/>

## 3. ์ฝ๋

```swift
import Foundation

func solution(_ n:Int, _ lost:[Int], _ reserve:[Int]) -> Int {
    var sortedLost = lost.sorted(by: < )
    var suitDict: [Int:Bool] = [:]
    var count = 0
    for suitNum in reserve {
        if sortedLost.contains(suitNum) {
            let removeIndex = sortedLost.firstIndex(of: suitNum)
            sortedLost.remove(at: removeIndex!)
            count += 1
            continue
        }
        suitDict[suitNum] = true
    }
    for lostNum in sortedLost {
        if let suit = suitDict[lostNum - 1], suit == true {
            suitDict[lostNum - 1] = false
            count += 1
            continue
        }
        if let suit = suitDict[lostNum + 1], suit == true {
            suitDict[lostNum + 1] = false
            count += 1
            continue
        }
    }
    let answer = n - lost.count + count
    return answer
}

```

<br/>

## 4. ํ์ด ๊ณผ์ 

๋ฌธ์ ๋ฅผ ๋ณด๊ณ  ๋ค์๊ณผ ๊ฐ์ด ์๊ฐํ๋ค.

    ์ ๋ค ์์์ ์น๊ตฌ์๊ฒ๋ง ์ฒด์ก๋ณต์ ๋น๋ ค์ค ์ ์์.
    -> ์์ ์น๊ตฌ๊ฐ ์ฐ์  ๋น๋ ค์ฃผ๊ณ , ์๋๋ฉด ๋ค์ ์น๊ตฌ๊ฐ ๋น๋ ค์ฃผ์.

์ด๋ฅผ ๋ฐํ์ผ๋ก ์ฝ๋์ ํ๋ฆ์ ์ง๋ดค๋ค.
    
    1. lost: ์ค๋ฆ์ฐจ์์ผ๋ก ์ ๋ ฌ.
    2. reserve: dict์ผ๋ก ์ ์ฅ.
    3. lost ํ๋์ฉ ๋ณด๊ณ  ์,๋ค์ ์ฒด์ก๋ณต์ ๋น๋ ค์ค ์ ์๋์ง ํ์ธ.
        - ๋น๋ ค์ค ์ ์๋ค๋ฉด ๋น๋ ค์ฃผ๊ณ  dict ์๋ฐ์ดํธ

<br/>

์ด๋ ๊ฒ ํด์ ๋ฌธ์ ๊ฐ ์ ํ๋ฆด์ค ์์๊ฑด๋ง...!

๊ณ์ ์คํจ๊ฐ ๋ ์ ๋ญ๊ฐ ์๋ชป๋์๋ ๋ดค๋๋,

- ์ฌ๋ฒ ์ฒด์ก๋ณต์ ๊ฐ์ ธ์จ ํ์์ด ์ฒด์ก๋ณต์ ๋๋๋นํ์ ์ ์์ต๋๋ค. ์ด๋ ์ด ํ์์ ์ฒด์ก๋ณต์ ํ๋๋ง ๋๋๋นํ๋ค๊ณ  ๊ฐ์ ํ๋ฉฐ, ๋จ์ ์ฒด์ก๋ณต์ด ํ๋์ด๊ธฐ์ ๋ค๋ฅธ ํ์์๊ฒ๋ ์ฒด์ก๋ณต์ ๋น๋ ค์ค ์ ์์ต๋๋ค.

<br/>
์๋ฐ ์กฐ๊ฑด์ด ์์๋ค.

์ด๊ฑธ ์๋ณด๊ณ  ํ๋ค๊ฐ ์คํจ๊ฐ ๊ณ์ ๋ฌ๊ฒ..!

๊ทธ๋์ dict ์ ๋ง๋๋ ๋ฐ๋ณต๋ฌธ์ ์ฝ๋๋ฅผ ์ถ๊ฐํ์ฌ, ์์ด๋ฒ๋ฆฐ ์ฒด์ก๋ณต์ ๋๋ ค์คฌ๋ค.

<br/>

> ๋ฌธ์  ์กฐ๊ฑด์ ์ ๋ณด์!


<br/>


```toc

```
