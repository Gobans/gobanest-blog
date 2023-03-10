---
emoji: ๐งถ
title: '[ํ๋ก๊ทธ๋๋จธ์ค] ์์ ์ฐพ๊ธฐ'
date: '2023-01-11 00:00:00'
author: ๊ณ ๋ฐ
tags: ์๊ณ ๋ฆฌ์ฆ
categories: Algorithm
---

## 1. ๋ฌธ์ 

`ํ๋ก๊ทธ๋๋จธ์ค`

[๊ณ ๋์  Kit ์์ ์ฐพ๊ธฐ](https://school.programmers.co.kr/learn/courses/30/lessons/42839)


<br/>

## 2. ํต์ฌ ์์ด๋์ด

`์์ด` `์์ ํ์`

<br/>

## 3. ์ฝ๋

```swift
import Foundation

func solution(_ numbers:String) -> Int {
    var answer = 0
    var madePermuString = Set<String>()
    let splitedNumbers = numbers.map{ $0 }
    for targetNum in 1...splitedNumbers.count {
        let permuByTargetNum = permutation(splitedNumbers, targetNum)
        for combArray in permuByTargetNum {
            let combString = combArray.reduce("") { String($0) + String($1)}
            if combString.first == "0" || madePermuString.contains(combString) {
                continue
            }
            madePermuString.insert(combString)
            if isPrime(Int(combString)!) {
                answer += 1
            }
        }
    }
    
    return answer
}

func isPrime(_ n: Int) -> Bool {
    guard n >= 2     else { return false }
    guard n != 2     else { return true  }
    guard n % 2 != 0 else { return false }
    return !stride(from: 3, through: Int(sqrt(Double(n))), by: 2).contains { n % $0 == 0 }
}

```

<br/>

## 4. ํ์ด ๊ณผ์ 

ํ์ด๋ฅผ ๋ค์๊ณผ ๊ฐ์ด ๋๊ฐ์ง ๋ฐฉ๋ฒ์ ์๊ฐํ๋ค.

    ์ข์ด ์กฐ๊ฐ์ผ๋ก ๋ง๋ค ์ ์๋ ์์๊ฐ ๋ช๊ฐ์ธ์ง ํ์ธ
    1. ์กฐํฉ์ ์ฌ์ฉํ์ฌ ์ซ์๋ฅผ ๋ง๋ค์ด๋ -> ํด๋น ์ซ์๊ฐ ์์์ธ์ง ํ๋ณ.
    2. ์์์ ์กฐ๊ฑด์ ๋ฐ๋ผ ์ซ์๋ฅผ ๋ง๋ค๊ธฐ (๊ฐ๋ฅํ๊ฐ?)
    -> ์์์ ์กฐ๊ฑด: 1๊ณผ ์์ ์ ์ ์ธํ ์์ฐ์๋ก ๋๋ ์ง์ง ์์.
    -> ์ด๊ฑด ๊ฒฐ๊ตญ ์ซ์๋ฅผ ๋ง๋ค์ด์ ํ์ธ์ ํด์ผํ๋? ์ ๋ชจ๋ฅด๊ฒ ๋ค.

๊ทธ๋ฐ๋ฐ 2๋ฒ ๋ฐฉ๋ฒ์ ๋ ๋ณต์กํ๊ฒ ํธ๋ ๊ฒ ๊ฐ์์ ์ง๊ด์ ์ธ 1๋ฒ ๋ฐฉ๋ฒ์ผ๋ก ์ฝ๋๋ฅผ ๊ตฌํํ๊ธฐ๋ก ํ๋ค.

์ฝ๋ ํ๋ก์ฐ๋ฅผ ๋ค์๊ณผ ๊ฐ์ด ์๊ฐํ๋ค.

    1. numbers ๋ฅผ ๋ฌธ์์ด ๋ฐฐ์ด๋ก ๋ฐ๊ฟ
    2. ๋ฐ๊พผ ๋ฌธ์์ด ๋ฐฐ์ด์ ์กฐํฉํ ์๋ค์ ๋ฐฐ์ด๋ก ๋ง๋ฌ
    3. filtering ํ์ฌ ๋งจ์ ์ซ์๊ฐ 0์ธ ๊ฒฝ์ฐ๋ฅผ ์ ์ธ
    4. ๋ฐ๋ณต๋ฌธ์ผ๋ก ์์์ธ์ง ํ๋ณ

<br/>

์ฐ์  ์กฐํฉํด์ ๋ง๋ค์ด์ง ์๋ค์ด ์์๊ฐ ์๊ด์์๊ธฐ ๋๋ฌธ์ `์์ด`์ ์ฌ์ฉํ๋ค.

ex) 17, 71

ํด๋น์ฝ๋๋ [์ด๊ณณ]() ์์ ํ์ธํ  ์ ์๋ค.

<br/>

์กฐํฉ์ผ๋ก ๋ง๋ค์ด์ง string ์ค์ ์ค๋ณต๋๋ string์ ๊ฑฐ๋ฅด๊ธฐ ์ํด set์ผ๋ก `madePermuString` ์ ๋ฌธ์์ด์ ๋ฃ์ด๊ฐ๋ฉฐ ์ค๋ณต์ ํ๋ณํ์๋ค.

์์ ํ๋ณ์ isPrime ๋ฉ์๋๋ฅผ ๋ง๋ค์ด ์ฌ์ฉํ๋๋ฐ ์ ๊ณฑ๊ทผ์ ์ด์ฉํด์ 2 ์ฉ n์ ๋๋ ค๊ฐ๋ฉฐ ์์๋ฅผ ํ๋ณํ๋ฉด 

$$O(\frac{1}{2}\sqrt{n})$$

์ ์๊ฐ๋ณต์ก๋๋ฅผ ๊ฐ์ง๋ค.

<br/>


```toc

```
