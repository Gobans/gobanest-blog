---
emoji: ๐งถ
title: '[ํ๋ก๊ทธ๋๋จธ์ค] ๋ชจ์์ฌ์ '
date: '2023-01-19 00:00:00'
author: ๊ณ ๋ฐ
tags: ์๊ณ ๋ฆฌ์ฆ
categories: Algorithm
---

## 1. ๋ฌธ์ 

`ํ๋ก๊ทธ๋๋จธ์ค`

[๊ณ ๋์  Kit ๋ชจ์์ฌ์ ](https://school.programmers.co.kr/learn/courses/30/lessons/84512)


<br/>

## 2. ํต์ฌ ์์ด๋์ด

`์์ ํ์` `DFS`

``

<br/>

## 3. ์ฝ๋

```swift
import Foundation

var count = 0
var isSearched = false

func solution(_ word:String) -> Int {
    DFS(combString: "", targetWord: word)
    return count
}

func DFS(combString: String, targetWord: String) {
    if combString == targetWord {
        isSearched = true
        return
    } else if combString.count == 5 {
        return
    } else {
        let letters = ["A", "E", "I", "O", "U"]
        for letter in letters {
            count += 1
            if !isSearched {
                DFS(combString: combString + letter, targetWord: targetWord)
            }
        }
    }
}
```

<br/>

## 4. ํ์ด ๊ณผ์ 

์ด๋ป๊ฒ ํ์ด์ผํ ์ง ํ 30๋ถ์ ๋ ๊ณ ๋ฏผ์ ํ๋๋ฐ, ๋๋ฌด์ง ๋ฐฉ๋ฒ์ด ๋ ์ค๋ฅด์ง ์์์, ๋ค๋ฅธ ์ฌ๋์ ํ์ด๋ฅผ ์ฐธ๊ณ ํ๋ค.

๋ด๊ฐ ์ฐธ๊ณ ํ ๊ณณ์ [์ด๊ณณ](https://velog.io/@j_aion/ํ๋ก๊ทธ๋๋จธ์ค-LV2-๋ชจ์์ฌ์ -i93blnu7) ์ด๋ค.

์ฌ๊ธฐ์๋ DFS๋ฅผ ๋ฉ์ถ๋ flag๊ฐ ์ค์ ๋์ด ์์ง ์์์, ์กฐ๊ธ ๋ฆฌํฉํ ๋ง ํด์ ์ฝ๋๋ฅผ ์์ฑํ๋ค.

<br/>

๋ต์ ๋ณด๋ฉด ๋จ์ํ๋ฐ, ๋ฌธ์ ๋ฅผ ํ๋๋ AAAAA -> AAAAE -> AAAAI -> .... -> E -> EE

์ด๋ฐ์์ผ๋ก ์ฌ์ ์ด ํ์ฑ๋๋๊ฒ์ด DFS์ ์ฌ๊ท๋ก ๋ง๋ค ์ ์๋ค๋ ๊ฒ์ ๋ ์ฌ๋ฆฌ๊ธฐ๊ฐ ํ๋ค์๋ค.

`์ฌ๊ท์ ์คํ ์์`๊ฐ ์ด ํ์ด์ ํต์ฌ ํค์๋ค.

<br/>

## 5. ๋ค๋ฅธ ์ฌ๋์ ์ฝ๋

```swift
import Foundation

func solution(_ word:String) -> Int {
    var answer = word.count
    var count = 0
    var arr = [781, 156, 31, 6, 1]
    var arr2 = ["A": 0, "E": 1, "I": 2, "O":3, "U":4]

    for ch in word{
        answer += arr2[String(ch)]!*arr[count]
        count += 1
    }
    return answer
}
```
<br/>

๋ค๋ฅธ ๊ธ์๋ก ๋ณ๊ฒฝ๋  ๋ ํ์ํ ์๋ฆฟ์๋ง๋ค์ ์ฝ์คํธ๋ฅผ ๋ฏธ๋ฆฌ ์ ์ฅํด์ ๋ํด์ฃผ๋ ๋ฐฉ๋ฒ์ด ์์๋ค.

๊ทธ๋ฐ๋ฐ AAAAA -> EAAAA ๋ก ๋ณ๊ฒฝ๋  ๋ ์ฝ์คํธ๋ฅผ ์ด๋ป๊ฒ ์์๋ธ๊ฑธ๊น?

์ด๋ฅผ ํ์ํ๊ธฐ๊ฐ ์ค์ ์์๋ ์กฐ๊ธ ์ด๋ ค์ธ ๊ฒ ๊ฐ๋ค.


```toc

```