---
emoji: ๐งถ
title: '[ํ๋ก๊ทธ๋๋จธ์ค] ํฐ ์ ๋ง๋ค๊ธฐ'
date: '2023-01-23 00:00:00'
author: ๊ณ ๋ฐ
tags: ์๊ณ ๋ฆฌ์ฆ
categories: Algorithm
---

## 1. ๋ฌธ์ 

`ํ๋ก๊ทธ๋๋จธ์ค`

[๊ณ ๋์  Kit ํฐ ์ ๋ง๋ค๊ธฐ](https://school.programmers.co.kr/learn/courses/30/lessons/42883)


<br/>

## 2. ํต์ฌ ์์ด๋์ด

`๊ทธ๋ฆฌ๋`

<br/>

## 3. ์ฝ๋

```swift
func solution(_ number:String, _ k:Int) -> String {
    let numberArray = Array(number)
    var pickCnt = k
    var stack: [Character] = []
    for i in 0..<numberArray.count {
        while !stack.isEmpty && pickCnt > 0 && stack.last!.wholeNumberValue! < numberArray[i].wholeNumberValue! {
            stack.removeLast()
            pickCnt -= 1
        }
        if stack.count < numberArray.count-k {
            stack.append(numberArray[i])
        }
    }
    return String(stack)
}
```

<br/>

## 4. ํ์ด ๊ณผ์ 

์ฒ์์ ์๊ฐ์ ๋ค์๊ณผ ๊ฐ์ด ์๊ฐํ๋ค.

    number ์ ๊ฐ์ - k ๋งํผ ๋ฝ์์ ๋ ๊ฐ์ฅ ํฐ ์

์ ๊ฑฐํ  ๊ฐ์๋ง๊ณ  ๋ฝ์ ๊ฐ์๋ฅผ ๊ธฐ๋ฐ์ผ๋ก ์กฐํฉํด์, DFS ๋ก ๋ชจ๋  ๊ฒฝ์ฐ๋ฅผ ํ์ํ๋ ๋ฐฉ๋ฒ์ผ๋ก ๋ฌธ์ ๋ฅผ ํ๋ ค๊ณ  ํ๋ค.

<br/>

[DFS]
```swift
func solution(_ number:String, _ k:Int) -> String {
    let numberArray = number.map{ String($0) }
    let pickNum = numberArray.count - k
    var maxNum = 0
    let visited = Array(repeating: false, count: numberArray.count)
    func DFS(perNumString: String, visited: [Bool], startIndex: Int) {
        if perNumString.count == pickNum {
            if let perNum = Int(perNumString) {
                maxNum = max(perNum, maxNum)
            }
            return
        }
        var cVisited = visited
        for i in startIndex..<numberArray.count {
            if !cVisited[i] {
                cVisited[i] = true
                let newString = perNumString + numberArray[i]
                DFS(perNumString: newString, visited: cVisited, startIndex: i)
            }
        }
    }
    DFS(perNumString: "", visited: visited, startIndex: 0)
    }
    return String(maxNum)
}
```

ํ์์ ์ผ์ง์ ์ผ๋ก (๋ฐฉ๋ฌธ์ ์์ํ ์ซ์์ ์  ์ซ์๋ฅผ ๋ฐฉ๋ฌธํ์ง ์๋๋ก)

์ด๋ ๊ฒ visited ์ ๋ฐฉ๋ฌธ์ `true` ๋ก๋ง ์ค์ ํ์ฌ์ ๊ตฌํํ์๋ค.

๊ทธ๋ฐ๋ฐ ์ด ๋ฐฉ๋ฒ์ ์๊ฐ์ด๊ณผ๊ฐ ๋์๋คใ

<br/>

๋ค๋ฅธ ๋ฐฉ๋ฒ์ผ๋ก ํ๋ฅผ ์ด์ฉํ์ฌ BFS๋ฅผ ์ฌ์ฉํด์ ํ์ด๋ดค๋ค.

```swift
func solution(_ number:String, _ k:Int) -> String {
    let numberArray = Array(number)
    var pickCnt = k
    var stack: [Character] = []
    for i in 0..<numberArray.count {
        while !stack.isEmpty && pickCnt > 0 && stack.last!.wholeNumberValue! < numberArray[i].wholeNumberValue! {
            stack.removeLast()
            pickCnt -= 1
        }
        if stack.count < numberArray.count-k {
            stack.append(numberArray[i])
        }
    }
    return String(stack)
}
```

๊ทธ๋ฐ๋ฐ ๋ชจ๋  ๊ฒฝ์ฐ๋ฅผ ํ์ํ๋ ๊ฑด DFS BFS ๋ชจ๋ ๋๊ฐ์์, ์ฌ์ ํ ์๊ฐ์ด๊ณผ์๋ค.

์ด๋ป๊ฒ ํ์ด์ผํ ์ง ๊ฐ์ด ์์กํ์ [์ด๊ณณ](https://sio2whocode.tistory.com/m/182) ์ ์ฐธ๊ณ ํ์๋ค.

<br/>

DFS๋ฅผ ํ๊ณ ๋ ํ ๋น์ทํ ์๊ฐ์ ํ์๋๋ฐ, `๋ค์ ์ซ์๋ก ์ด๋ํ๋ฉด์ ๋ฐฐ์ด์ ์๋ ๋ชจ๋ ์ซ์๋ฅผ ์ ์์ ์ถ ์์๋ก ๋ชจ๋ ๊บผ๋ด๊ณ  ๋น๊ตํด์ ์ญ์ ํด์ผํ์ง ์๋?` ๋ผ๊ณ  ์๋ชป์๊ฐํ์ฌ ์ด ํ์ด๊น์ง ๋๋ฌ์ ๋ชปํ์๋ค.๐ฅฒ

๋งค๋ฒ ๋ฐ๋ณต๋ฌธ์ ์คํ๋ง๋ค ๋ฐฐ์ด์ ์์์์ ์๋ ์ซ์์ ๋น๊ต๊ฐ ์ผ์ด๋๊ณ , ์ ๊ฑฐํ  ์ ์๋ ์นด์ดํธ๋งํผ ๊ต์ฒด๊ฐ ๋  ๊ฒ์ด๊ธฐ ๋๋ฌธ์ `์ ์์ ์ถ์ ์์`๋ก ๋น๊ตํ  ํ์๊ฐ ์์๋ค.

<br/>

๊ทธ๋ฆฌ๋ ์ด๋ ต๋ค.. ๋ฌธ์ ์ ์ํฉ์ ๋ํด ํ์ธต ๋ ๊น๊ฒ ์๊ฐํ์ฌ ์ต์ ์ ๋ฐฉ๋ฒ์ ๊ตฌํํด๋ด๋๊ฒ ์ด๋ ต๋ค.

์ฐ์ต์ ํ๋ฉด์ ๊ฐ์ ์ก์์ผํ ๋ฏํ๋ค.

<br/>

## 5. ๋ค๋ฅธ ์ฌ๋์ ์ฝ๋

```swift
import Foundation

func solution(_ number:String, _ k:Int) -> String {
    var answer = ""

    var _k:Int = k // k๋ฅผ ๊ฐ์์ํค๊ธฐ ์ํด ๋ณ์๋ก ์ ์ธ
    let numbers:[Character] = Array(number) // swift ๋ฌธ์์ด์ ์๋ธ์คํฌ๋ฆฝํธ๋ฅผ ์ ๊ณตํ์ง ์๊ธฐ ๋๋ฌธ์ ํธ์์ ๋ฐฐ์ด๋ก ๋ณํ
    let n:Int = numbers.count
    var stack:[Character] = []
    
    for (i,num) in numbers.enumerated() {
    	// ์คํ์์ ๊ฐ์ ๋นผ๋ด๋ ๋ฐ๋ณต๋ฌธ
        while !stack.isEmpty && _k > 0 && 
        stack.last!.wholeNumberValue! < num.wholeNumberValue! {
            stack.removeLast()
            _k -= 1
        }
        // ์ ํด์ง ๊ธธ์ด๋ฅผ ๋์ง ์๋๋ค๋ฉด stack์ append
        if stack.count < n-k {
            stack.append(num)
        }
    }
    return String(stack)
}
```

๋ด๊ฐ ์ฐธ๊ณ ํ ์ฝ๋์ธ๋ฐ, ์ด๊ณณ์์ enumerated ๋ง ๋ณ๊ฒฝํ์๋ค.

|<center>Enumerated<center/>|<center>No Enumerated<center/>|
| :---: | ---: | 
|![Enumerated.png](Enumerated.png)|![NoEnumerated.png](NoEnumerated.png)|

Enumerated ํ๋ ์ฐจ์ด์ธ๋ฐ ์๊ฐ์ด๊ฐ ์์ฃผ ์ฐจ์ด๋๋ค.

<br/>


```toc

```
