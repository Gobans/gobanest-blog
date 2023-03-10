---
emoji: ๐งถ
title: '[ํ๋ก๊ทธ๋๋จธ์ค] H-Index'
date: '2023-01-08 00:00:00'
author: ๊ณ ๋ฐ
tags: ์๊ณ ๋ฆฌ์ฆ
categories: Algorithm
---

## 1. ๋ฌธ์ 

`ํ๋ก๊ทธ๋๋จธ์ค`

[๊ณ ๋์  Kit H-Index](https://school.programmers.co.kr/learn/courses/30/lessons/42747)


<br/>

## 2. ํต์ฌ ์์ด๋์ด

`์ ๋ ฌ`

<br/>

## 3. ์ฝ๋

[swift]
```swift
import Foundation

func solution(_ citations:[Int]) -> Int {
    var hIndex = 0
    guard let maxCitation = citations.max(), maxCitation != 0 else {
        return 0
    }
    let sortedCitations = citations.sorted(by: >)
    for index in 1...maxCitation {
        var citationCount = 0
        for citation in sortedCitations {
            if citation >= index {
                citationCount += 1
            } else {
                break
            }
        }
        if citationCount >= index {
            hIndex = index
        } else {
            break
        }
    }
    return hIndex
}

```

<br/>

## 4. ํ์ด ๊ณผ์ 

๋ฌธ์ ๋ฅผ ๋ณด๊ณ  ๋ค์๊ณผ ๊ฐ์ด ์๊ฐํ์๋ค.

- h ๋ฒ์ด์ ์ธ์ฉ, h ํธ ์ด์ ์ธ์ฉ
    - -> ์ธ์ฉ๋ ํ์์ ์ธ์ฉ๋ ๊ฐฏ์๊ฐ ํจ๊ป h ์ด์์ด์ฌ์ผํจ.
- h ๋ฒ ์ดํ ์ธ์ฉ 
    - -> H-Index ์ ์ต๋๋ฅผ ๊ตฌํด์ผํ๊ณ , H-Index ๊ฐ ์ธ์ฉํ์ ๋ฒ์๋ฅผ ์ด์, ์ดํ ๋ชจ๋ ํฌํจํ๊ธฐ ๋๋ฌธ์ ๋ณ๋ก ์๊ด ์์

๋๋ฌธ์ 'h ๋ฒ์ด์ ์ธ์ฉ, h ํธ ์ด์ ์ธ์ฉ' ์ด ์กฐ๊ฑด์ ๋ง๋์ง ๊ฒ์ฆ์ ํด์ผํ๊ธฐ ๋๋ฌธ์ ๋ค์๊ณผ ๊ฐ์ด ์ฝ๋์ ํ๋ก์ฐ๋ฅผ ์๊ฐํ๋ค.

1. max citation ๋งํผ ๋ฐ๋ณต
2. 1๋ถํฐ ๊ฒ์ฆ
3. ๋ด๋ฆผ์ฐจ์์ผ๋ก ์ ๋ ฌ๋ citations ์์ h ๋ฒ ์ด์ ์ธ์ฉ๋ ๋ผ๋ฌธ์ด ๋ช๊ฐ์ธ์ง ํ์ธ.
4. ๋ถ๋ง์กฑ ์ ํ์ฌ๊น์ง์ ์ต๋ h-index return

๊ทธ๋๋ก ๊ตฌํํ๋๊น ํต๊ณผํ ๋ป ํ๋๋ฐ, `(signal: illegal instruction (core dumped))`
์ค๋ฅ๊ฐ ๋ฐ์ํ๋ค.

ํฌ๋์ฌ๊ฐ ๋ ๊ณณ์ด ์ด๋์ง ์๊ฐํด๋ณด๋ maxCitation์ ๊ตฌํ๊ณ , 1๋ถํฐ ๋ฐ๋ณต๋ฌธ์ ์คํํ๋ ๊ตฌ๊ฐ์ด์๋ค. 

maxCitation์ด 0์ผ ๊ฒฝ์ฐ `Fatal error: Range requires lowerBound <= upperBound` ์ค๋ฅ๊ฐ ๋ด๋ค.

๋๋ฌธ์ guard let ์ผ๋ก ์กฐ๊ฑด์ ์ถ๊ฐํ์ฌ ์์ธ ์ผ์ด์ค๋ฅผ ์ฒ๋ฆฌํด์คฌ๋ค.

<br/>

## 5. ๋ค๋ฅธ ์ฌ๋์ ์ฝ๋

```swift
import Foundation

func solution(_ citations:[Int]) -> Int {
    let citations = citations.sorted() { $0 > $1 }
    var result = 0

    for i in 0..<citations.count {
        if i + 1 <= citations[i] {
            result = i + 1
        } else {
            break
        }
    }

    return result
}

```

์ธ์ฉ๊ฐฏ์์ ์ธ์ฉํ์๋ฅผ ์ด๋ฐ์์ผ๋ก ๊ฐ๋จํ๊ฒ ํจ๊ป ํ์ธ์ ํ ์๊ฐ ์์๋ค.

์ด๋ฐ ํ์ด๊ฐ ๋ฐ๋ก ๋ ์ค๋ฅผ๋ ค๋ฉด ์ด๋ป๊ฒ ํด์ผํ ๊น?

๋ถ๋จํ ์ฐ์ต์ ํด์ผ๊ฒ ๋ค..

<br/>


```toc

```
