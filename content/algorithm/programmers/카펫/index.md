---
emoji: ๐งถ
title: '[ํ๋ก๊ทธ๋๋จธ์ค] ์นดํซ'
date: '2023-01-13 00:00:00'
author: ๊ณ ๋ฐ
tags: ์๊ณ ๋ฆฌ์ฆ
categories: Algorithm
---

## 1. ๋ฌธ์ 

`ํ๋ก๊ทธ๋๋จธ์ค`

[๊ณ ๋์  Kit ์นดํซ](https://school.programmers.co.kr/learn/courses/30/lessons/42842)


<br/>

## 2. ํต์ฌ ์์ด๋์ด

`์์ ํ์` `์ฌ๊ท` `stack`

<br/>

## 3. ์ฝ๋

[์ฌ๊ท]
```swift
import Foundation

func solution(_ brown:Int, _ yellow:Int) -> [Int] {
    var answer: [Int] = []
    func searchCarpet(curBrown: Int, curYellow: Int, width: Int, height: Int) {
        if curBrown == brown && curYellow == yellow {
            answer = [width, height]
            return
        }
        if curBrown >= brown || curYellow >= yellow {
            return
        }
        searchCarpet(curBrown: curBrown + 2, curYellow: curYellow + height-2, width: width + 1, height: height)
        if width > height {
            for i in 1...width - height {
                if (curBrown + (2*i) == brown) && (curYellow + i*(width-2) == yellow) {
                    answer = [width, height + i]
                    return
                }
            }
        }
    }
    searchCarpet(curBrown: 8, curYellow: 1, width: 3, height: 3)
    return answer
}

```

<br/>

[stack]
```swift
struct Carpet {
    let brown: Int
    let yellow: Int
    let width: Int
    let height: Int
}

func solution(_ brown:Int, _ yellow:Int) -> [Int] {
    var answer: [Int] = []
    var searchStack: [Carpet] = []
    searchStack.append(Carpet(brown: 8, yellow: 1, width: 3, height: 3))
    
    while !searchStack.isEmpty {
        let carpet = searchStack.removeLast()
        if carpet.brown == brown, carpet.yellow == yellow {
            return [carpet.width, carpet.height]
        }
        if carpet.brown >= brown || carpet.yellow >= yellow {
            continue
        }
        if carpet.width > carpet.height {
            for i in 1...carpet.width - carpet.height {
                if (carpet.brown + (2*i) == brown) && (carpet.yellow + i*(carpet.width-2) == yellow){
                    return [carpet.width, carpet.height + i]
                }
            }
        }
        searchStack.append(Carpet(brown: carpet.brown + 2, yellow: carpet.yellow + carpet.height - 2, width: carpet.width + 1, height: carpet.height))
    }
    return answer
}
```

<br/>

## 4. ํ์ด ๊ณผ์ 

์ฒ์์ ๋ฌธ์ ๋ฅผ ์ด๋ป๊ฒ ํ์ด์ผํ ์ง ๊ฐ์ด ์ ์์๋๋ฐ, **๊ฐ์ ํ์ผ์ด ๋ธ๋์ ํ์ผ์ ํ๋๋ฆฌ 1์ด์ ์ฐจ์งํ๋ค** ๋ผ๋ ๋ฌธ๊ตฌ์์ ํํธ๋ฅผ ์ป์ด ๊ท์น์ ์ฐพ์๋๋ค.

- ๊ฐ๋ก, ์ธ๋ก๋ฅผ ๋๋ฆฌ๋ ๋์์ ๋ฐ๋ณตํ์ฌ ๋ง์กฑํ๋ brown, yellow์ ๊ฐฏ์๋ฅผ ์ฐพ๋๋ค. <br/> (๊ฐ๋ก >= ์ธ๋ก ์ผ๋ ์ธ๋ก๋ฅผ ๋๋ฆผ)
    - ๊ฐ๋ก๋ก ๋๋ฆฌ๋ ๋์: yellow + 1*(height-2), brown + 2
    - ์ธ๋ก๋ก ๋๋ฆฌ๋ ๋์: yellow * n, brown + 2*n

์ด ๊ท์น์ ๋ฐ๋ผ ๊ฐ๋ก๋ก ํ์ผ์ ๋๋ ค๊ฐ๋ฉด์ ์ธ๋ก๋ก ๋๋ ธ์๋ ๊ฒฝ์ฐ๋ฅผ ์ฒดํนํ๋ฉด ๋  ๊ฒ ๊ฐ๋ค๊ณ  ์๊ฐํ์๊ณ , ํ๋ฒ `์ฌ๊ท`๋ฅผ ์ฌ์ฉํ์ฌ ๋ฌธ์ ๋ฅผ ํ์ด๋ดค๋ค.

<br/>

๊ทธ ๋ค์์ ์๊ฐ์ด ์ฐจ์ด๊ฐ ์ผ๋ง๋ ๋๋์ง ๊ถ๊ธํด์ stack ์ผ๋ก๋ ํ๋ฒ ํ์ด๋ดค๋๋ฐ, ๊ฒฐ๊ณผ๋ ๋๋ผ์ ๋ค.

|<center>recursion<center/>|<center>stack<center/>|
| :---: | ---: | 
|![recursion.png](recursion.png)|![stack.png](stack.png)|

์ซ์๊ฐ ํฐ ํ์คํธ ์ผ์ด์ค์์ 5๋ฐฐ ์ ๋ ์๊ฐ์ฐจ์ด๊ฐ ๋ฒ์ด์ก๋ค.

์๋ง๋ ์ฌ๊ท๋ ์ ๋ต์ ์ฐพ์ ํ์๋ ๋จ์์๋ ์ฌ๊ท method ๋ฅผ ๊ณ์ ์คํ์ ํ๊ธฐ ๋๋ฌธ์ธ ๊ฒ ๊ฐ๋ค. ์ ๋ง ์ด์ฉ ์ ์๋ ๊ฒฝ์ฐ๊ฐ ์๋๋ฉด stack or queue ๋ฅผ ์จ์ผ๊ฒ ๋ค..!

<br/>


```toc

```
