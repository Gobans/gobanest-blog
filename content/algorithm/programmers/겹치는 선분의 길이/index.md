---
emoji: ๐งถ
title: '[ํ๋ก๊ทธ๋๋จธ์ค] ๊ฒน์น๋ ์ ๋ถ์ ๊ธธ์ด'
date: '2023-02-23 00:00:00'
author: ๊ณ ๋ฐ
tags: ์๊ณ ๋ฆฌ์ฆ
categories: Algorithm
---

## 1. ๋ฌธ์ 

`ํ๋ก๊ทธ๋๋จธ์ค`

[๊ณ ๋์  Kit ๊ฒน์น๋ ์ ๋ถ์ ๊ธธ์ด](https://school.programmers.co.kr/learn/courses/30/lessons/120876)


<br/>

## 2. ํต์ฌ ์์ด๋์ด

`๊ทธ๋ฆฌ๋`

<br/>

## 3. ์ฝ๋

```swift
import Foundation

func solution(_ lines:[[Int]]) -> Int {
    var answer = 0
    let minLength = lines.map{ $0[0]}.min()!
    let maxLength = lines.map{ $0[1]}.max()!
    for i in minLength...maxLength {
        var count = 0
        for line in lines {
            if line[0] ..< line[1] ~= i {
                count += 1
            }
        }
        if count >= 2 {
            answer += 1
        }
    }
    
    return answer
}
```

<br/>

## 4. ํ์ด ๊ณผ์ 

์ฒ์์๋ ์ด๋ ๊ฒ ์๊ฐํ๋ค.

์ ๋ถ์ ์ด ๊ธธ์ด๋ฅผ ๊ตฌํด์ 0์ผ๋ก ๋ฐฐ์ด์ ์ด๊ธฐํ ํ ํ,

ํด๋น ๋ฐฐ์ด์ ์ฃผ์ด์ง ์ ๋ถ๋ค์ ๊ธธ์ด์ ํด๋นํ๋ ์์น์ += 1 ์ฉ ํด์ค์ 2 ์ด์์ธ ์์น์ ๊ฐ์๋ฅผ ๊ตฌํ๋ฉด ๋์ง ์์๊น?

๋๋ต ์ด๋ฐ์์ด๋ค.

<br/>

```swift
let minLength = lines.map{ $0[0]}.min()!
let maxLength = lines.map{ $0[1]}.max()!
var resultLine =  Array(repeating: 0, count: maxLength - minLength + 1)

for line in lines {
    startIdx = minLength < 0 ? line[0] + minLength
    endIdx = minLength < 0 ? line[1] + minLength
    for i in startIdx...endIdx {
        resultLine[i] += 1
    }
}
resultLine.filter{ $0 >= 2 }.count
```

<br/>

๊ทธ๋ฐ๋ฐ ์ด๋ ๊ฒ ํ๋ฉด resultLine ๋ฐฐ์ด์ ๊ธธ์ด๋ ๋ค์ ๋ง์ถฐ์ฃผ๊ฑฐ๋, ๋์ ์ผ๋ก ๋ง์ถฐ์ฃผ์ง ์๊ณ  ์ ํ์ฌํญ์ ๋ง๊ฒ resultLine์ 200 (์ ๋ถ์ ๊ธธ์ด๋ -100 ~ 100)์ ๋ง์ถฐ์ค์ผํ๋๋ฐ, ์ ์๋ ๋ฒ๊ฑฐ๋กญ๊ณ  ํ์๋ ๋ญ๋น๋ผ๊ณ  ์๊ฐํด์ ๋ค๋ฅธ ๋ฐฉ๋ฒ์ ํํ๋ค.

<br/>

```swift
import Foundation

func solution(_ lines:[[Int]]) -> Int {
    var answer = 0
    let minLength = lines.map{ $0[0]}.min()!
    let maxLength = lines.map{ $0[1]}.max()!
    for i in minLength...maxLength {
        var count = 0
        for line in lines {
            if line[0] ... line[1] ~= i {
                count += 1
            }
        }
        if count >= 2 {
            answer += 1
        }
    }
    
    return answer
}
```

<br/>

๊ฐ๋จํ๊ฒ ~= ์ฐ์ฐ์๋ฅผ ์ฌ์ฉํ์ฌ ๋ฐ๊ฟจ๋๋ฐ, ํจ์ฌ ๊ฐ๊ฒฐํ๊ณ  ๋น ๋ฅด๊ฒ answer์ ์ฐพ์ ์ ์๋ค.

๊ทธ๋ฐ๋ฐ ํ์ฌ ์ด ์ฝ๋๋ก๋ ๋ต์ด 2๋ฐฐ๊ฐ ๋์๋ค.

<br/>

![exception.png](exception.png)

์์ธ๊ฐ ํ๋ ๋ผ์ธ์ด [[0, 2], [-3, -1], [-2, 1]] ์ผ๋ก ์ฃผ์ด์ง ๋ ํด๋น ์์น์์ ํ๋ฒ ๋ ์ฒดํน์ด ๋๊ธฐ ๋๋ฌธ์ด์๋ค.

์ฌ์ค์ ์ ๋ถ์ด ๋๋๋ ์ ์ ํ์นธ ์ ์์ ์ด๋ฏธ ์ ๋ถ์ ํ ๊ตฌ๊ฐ์ด ์ฒดํน๋๋ ๊ฒ์ด๋ฏ๋ก 

<br/>

```swift
if line[0] ..< line[1] ~= i {
    count += 1
}
```

<br/>

์ด๋ ๊ฒ ์ ๋ถ์ ๋์ ์ ์ฒดํน์ ํฌํจํ์ง ์๋๋ก ์ ์ฝ์ฌํญ์ ๋ฐ๊ฟ์ฃผ๋ฉด ๋๋ค.

LV0์ธ๋ฐ ์ด๋ ต๋ค๊ณ  ์๊ฐ์ด ๋ค์๋ค. LV0์ ํ๋ฒ ์น๋ค ํ์ด๋ด์ผ๊ฒ ๋ค.


<br/>

## 5. ๋ค๋ฅธ ์ฌ๋์ ์ฝ๋

```swift
import Foundation

func solution(_ lines:[[Int]]) -> Int {
    var log: [Int] = Array(repeating: 0, count: 201)

    for line in lines {
        for i in (line.min()!+1)...line.max()! {
            log[i + 100] += 1
        }
    }

    var result: Int = 0
    for i in 1..<log.count {
        if log[i] > 1 {
            result += 1
        }    
    }

    return result
}

```

<br/>

๋ด๊ฐ ์๋ ํ๋ ค๊ณ  ํ๋ ๋ฐฉ์์ด๋ค.

<br/>

|<center>mySolution<center/>|<center>otherSolution<center/>|
| :---: | ---: | 
|![mySolution.png](mySolution.png)|![otherSolution.png](otherSolution.png)|

<br/>

๋ค๋ฅธ ์ฌ๋์ ์๋ฃจ์์ 3๊ฐ์ line๋ง๋ค์ ๊ธธ์ด๋งํผ for๋ฌธ ๋ฐ๋ณต + ๋ง์ง๋ง ์ฒดํน๋ ๋ค์ ์ ์ฒด ๊ธธ์ด ๋ฐ๋ณต์ด๊ณ 

๋์ ์๋ฃจ์์ line์ ์ ์ฒด ๊ธธ์ด๋งํผ for๋ฌธ ํ๋ฒ ๋ฐ๋ณต, ๋ฐ๋ณต๋ฌธ ์์์ ๋ผ์ธ 3๊ฐ์ ๋ฒ์ ์ฒดํน์ด๋ผ์

๋์ ์๋ฃจ์์ด line์ ๊ธธ์ด๊ฐ ๊ธธ์๋ก ์ ๋ฆฌํ ๊ฒ ๊ฐ๋ค.


```toc

```
