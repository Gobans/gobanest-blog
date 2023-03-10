---
emoji: ๐งถ
title: '[ํ๋ก๊ทธ๋๋จธ์ค] N์ผ๋ก ํํ'
date: '2023-01-28 00:00:00'
author: ๊ณ ๋ฐ
tags: ์๊ณ ๋ฆฌ์ฆ
categories: Algorithm
---

## 1. ๋ฌธ์ 

`ํ๋ก๊ทธ๋๋จธ์ค`

[๊ณ ๋์  Kit N์ผ๋ก ํํ](https://school.programmers.co.kr/learn/courses/30/lessons/42895)


<br/>

## 2. ํต์ฌ ์์ด๋์ด

`DP` `DFS` `BruteForce`

<br/>

## 3. ์ฝ๋

[DFS]
```swift
func dfs(_ N: Int, _ number: Int, _ depth: Int, _ temp: Int, _ answer: inout Int)  {
    if depth > 8 {
        return
    }

    if temp == number && (answer > depth || answer == -1) {
        answer = depth
        return
    }

    var calc = 0

    for index in 0 ..< 8 {
        calc = calc * 10 + N
        dfs(N, number, depth + 1 + index, temp + calc, &answer)
        dfs(N, number, depth + 1 + index, temp - calc, &answer)
        dfs(N, number, depth + 1 + index, temp * calc, &answer)
        dfs(N, number, depth + 1 + index, temp / calc, &answer)
    }
}
func solution(_ N:Int, _ number:Int) -> Int {

    var answer = -1
    dfs(N, number, 0, 0, &answer)
    return answer
}
```

<br/>

[BruteForce]
```swift
import Foundation

var stack: [Int] = []
var count = 0
var minCount = 9

func bruteForceSearch(_ N: Int, _ number: Int) {
    let lastNum = count == 0 ? 0 : stack.last!
    if lastNum == number {
        minCount = count
    }
    
    var n = 0
    var addCount = 0
    var digit = 1
    
    while digit <= 100000 {
        addCount = addCount + 1
        if (count + addCount) >= minCount {
            break
        }
        
        n += (N*digit)
        count += addCount
        
        stack.append(lastNum + n)
        bruteForceSearch(N, number)
        stack.removeLast()
        
        if (lastNum - n) != 0 {
            stack.append(lastNum - n)
            bruteForceSearch(N, number)
            stack.removeLast()
        }
        
        stack.append(lastNum * n)
        bruteForceSearch(N, number)
        stack.removeLast()

        if (lastNum / n) != 0 {
            stack.append(lastNum / n)
            bruteForceSearch(N, number)
            stack.removeLast()
        }
        
        count -= addCount
        
        digit *= 10
    }
}

func solution(_ N:Int, _ number:Int) -> Int {
    bruteForceSearch(N, number)

    return minCount < 9 ? minCount : -1
}
```

<br/>

## 4. ํ์ด ๊ณผ์ 

์ฒ์ ๋ฌธ์ ๋ฅผ ํ๋, ์นดํ๊ณ ๋ฆฌ๊ฐ DP ๋ผ๋ ํ์ดํ์ ๋ฌ๊ณ ์์ด์ ์ ํ์์ ์ฐพ์์ผ๊ฒ ๋ค ๋ผ๋ฉฐ ๋จธ๋ฆฌ๋ฅผ ์ธ๋งธ๋๋ฐ...

๊ฒฐ๊ตญ ๋ชป์ฐพ์์ ์ธํฐ๋ท์์ ๋ต์ ๋ดค๋ค.

<br/>

[์ด๊ณณ](https://apple-apeach.tistory.com/70)์ ๋ดค๋๋ฐ.. ์๊ณ ๋ณด๋ ์ ํ์์ด ์๋๋ผ DFS BFS ๋ฅผ ์ด์ฉํ ์์ ํ์์ ํตํด ๋ฌธ์ ๋ฅผ ํ์์ด์ผ ํ๋ค.

DFS ๋ฅผ ์ด์ฉํ ์ฝ๋๋ [ํผ๋ก๋](https://gobanest.com/algorithm/programmers/ํผ๋ก๋/) ์์ ๋์จ DFS์ ์๋นํ ์ ์ฌํ๋ค. ๋๊ฐ์ด depth ๋ฅผ ํ์ธํ๋๋ฐ, N์ผ๋ก ํํ์ ์ต์ depth๋ฅผ ์ฐพ์์ผํ๊ณ  ํผ๋ก๋๋ ์ต๋ depth๋ฅผ ์ฐพ์์ผํ๋ ๋ฌธ์ ์๋ค.

<br/>

๋๊ฐ์ DFS์ด์ง๋ง ์๊ณ ๋ฆฌ์ฆ์ด ์กฐ๊ธ ๋ค๋ฅธ ๋ฐฉ์์ผ๋ก๋ ๋ฌธ์ ๋ฅผ ํผ ๊ณณ๋ ์์๋ค. ([์ด๊ณณ](https://boycoding.tistory.com/227))

์ฐจ์ด์ ์ stack์ ์ด์ฉํ๊ณ , ์กฐ๊ธ ๋ ์ ๋ฐํ ์กฐ๊ฑด์ ์ค์ 

    1. if (lastNum - n) != 0
    2. if (lastNum / n) != 0)
    3. if (count + addCount) >= minCount {
            break
        }

์กฐ๊ธ ๋ ํ์ ์๊ฐ์ ๋จ์ถ์ํค๋ ๊ฒ์ ์์๋ค.

<br/>


```toc

```
