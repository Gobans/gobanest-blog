---
emoji: ๐งถ
title: '[ํ๋ก๊ทธ๋๋จธ์ค] ๊ฐ์ฅ ํฐ ์'
date: '2023-01-08 00:00:00'
author: ๊ณ ๋ฐ
tags: ์๊ณ ๋ฆฌ์ฆ
categories: Algorithm
---

## 1. ๋ฌธ์ 

`ํ๋ก๊ทธ๋๋จธ์ค`

[๊ณ ๋์  Kit ๊ฐ์ฅ ํฐ ์](https://school.programmers.co.kr/learn/courses/30/lessons/42747)


<br/>

## 2. ํต์ฌ ์์ด๋์ด

`๋ฌธ์์ด ์ ๋ ฌ`

<br/>

## 3. ์ฝ๋

[swift]
```swift
func solution(_ numbers:[Int]) -> String {
    var answer = ""
    var stringNumbers = numbers.map({ String($0)})
    stringNumbers.sort { lhs, rhs in
        return isLhsBigger(lhs: lhs, rhs: rhs)
    }
    stringNumbers.forEach { stringNumber in
        answer += stringNumber
    }
    if Int(answer) == 0{
        return "0"
    }
    return answer
}

func isLhsBigger(lhs: String, rhs: String) -> Bool {
    let lhsFirst = lhs + rhs
    let rhsFirst = rhs + lhs
    return lhsFirst > rhsFirst
}


```

<br/>

## 4. ํ์ด ๊ณผ์ 

์ฐ์  ๋ฌธ์ ๋ฅผ ๋ณด์ ์๋์ ๊ฐ์ ์๊ฐ์ ํ๋ค.

1. ์ ์๋ฅผ ์ด์ด ๋ถ์์ ๋ ๊ฐ์ฅ ํฐ์๋ฅผ ๊ตฌํ๋ผ
    - ์์๋ฆฌ ์๊ฐ ๊ฐ์ฅ ํฐ ์๋ฅผ ๋ถ์ฌ์ ๋ง๋  ์
2. ๋ฌธ์๋ก ์ ๋ ฌํด๋๊ณ  ๋ถ์ด๋ฉด ๋์ง์๋?

๊ทธ๋์ ๋จ์ํ๊ฒ ๋ฌธ์๋ฅผ ๋์ ๋น๊ตํด์ ์ ๋ ฌ ํ๋๋ฐ, ์ ๋๋ก ์ ๋ ฌ์ด ๋์ง ์๋ ์ํฉ์ด ๋ฐ์ํ๋ค.

์๋ฅผ๋ค๋ฉด "121" ๊ณผ "12", "10" ๊ณผ "1" ๋ฌธ์์ด์์๋ ์ด๋ค์ "121" ๊ณผ "10" ์ด ์ฐ์ ๋๊ฒ ์ ๋ ฌ์ ํ๋ค.


๊ทธ๋์ ๊ทธ ๋ค์ ๋  ์๊ฐ์ด '๋ฌธ์์ด ์์ chracter ๋ฅผ ์๋ฆฟ์๋ง๋ค ํ๋์ฉ ๋น๊ตํ์' ์๋๋ฐ, ๋ฌธ์์ด ์๋ก์ ๊ธธ์ด๊ฐ ๋ค๋ฅผ ๊ฒฝ์ฐ, ์๋ฆฟ์๋ฅผ ๋ค์ ๋ฐ๋ณตํด์ ๋น๊ตํด์ค์ผํ๋ ๋ฒ๊ฑฐ๋กญ๊ณ  ๋นํจ์จ์ ์ธ ๋ฌธ์ ๊ฐ ์์๋ค.


๊ณ ๋ฏผ๊ณ ๋ฏผ์ ํ๋ค ๊ฒฐ๊ตญ ์ข์ ๋ฐฉ๋ฒ์ด ๋ ์ฌ๋๋๋ฐ, `๋ฌธ์์ด ๋๊ฐ๋ฅผ ์๋ก ๋ค๋ฅธ ์์๋ฅผ ๋ง๋ถ์ฌ ๋ง๋ค์ด์ง ๋ฌธ์์ด์ ๋น๊ต`ํ๋ ๊ฒ์ด์๋ค. 

[swift]
```swift
// compare one by one
func isLhsBigger(lhs: String, rhs: String) -> Bool {
    let lhsFirst = lhs + rhs
    let rhsFirst = rhs + lhs
    let lhsArray: [Int] = lhsFirst.compactMap{ $0.wholeNumberValue }
    let rhsArray: [Int] = rhsFirst.compactMap{ $0.wholeNumberValue }
    for (lhsNum, rhsNum) in zip(lhsArray, rhsArray) {
        if lhsNum > rhsNum {
            return true
        } else if lhsNum < rhsNum{
            return false
        }
    }
    return true
}
```

๊ทธ๋ฐ๋ฐ ๋ ์๊ฐํด๋ณด๋ ์ด๋ ๊ฒ ํ๋ํ๋์ฉ ๋ฐ๋ณต๋ฌธ์ผ๋ก ๋น๊ตํ  ํ์๊ฐ ์์๋ค. ์ด์ฐจํผ ํฉ์ณค์ ๋ ํฐ์ ๋๋ก ์ ๋ ฌํ๋ฉด ๋์ง ์๋๊ฐ?

๊ทธ๋์ ์ฝ๋๋ฅผ ๋ฐ๊ฟจ๊ณ  ๊ทธ๊ฒ์ด ์ง๊ธ ์ฝ๋์ด๋ค.

๊ทธ๋ฐ๋ฐ ํ์คํธ ์ผ์ด์ค์์ ํ๋์ ์ผ์ด์ค์์ ๊ณ์ ํ๋ฆฐ๋ค๊ณ  ๋จ๊ธธ๋, ๋ญ๊ฐ ์ถ์๋๋ฐ numbers๊ฐ 0 ์ผ๋ก๋ง ์ด๋ฃจ์ด์ก์ ๋์ ์ผ์ด์ค์๋ค.. 

์์ธ ์ผ์ด์ค๋ฅผ ํ๋ฒ ์๊ฐํด๋ณด๊ณ  ํ์คํธ ํด๋ณด๋ ๊ฒ์ด ํ์ํ๋ค๊ณ  ๋๊ผ๋ค.


<br/>

## 5. ๋ค๋ฅธ ์ฌ๋์ ์ฝ๋

```swift
import Foundation

func solution(_ numbers: [Int]) -> String {
    let sortedNumbers = numbers.sorted {
        Int("\($0)\($1)")! > Int("\($1)\($0)")!
    }

    let answer = sortedNumbers.map { String($0) }.reduce("") { $0 + $1 }
    return sortedNumbers.first == 0 ? "0" : answer
}
```

reduce ๋ฅผ ์จ์ ๋ฌธ์์ด์ ๋ํด์ค ๊ฒ์ด ์ธ์๊น์๋ค.

๋๋ reduce ๋ฅผ ์ ๊น ์๊ฐํ๋๋ฐ, ์ Int ์๋ฃํ๋ง ๋๋ค๊ณ  ์๊ฐํ๊ณ  ์์ผ์๊น..? ๋ฐ๋ณด๋ค

<br/>


```toc

```
