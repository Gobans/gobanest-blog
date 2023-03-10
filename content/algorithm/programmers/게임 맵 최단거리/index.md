---
emoji: ๐งถ
title: '[ํ๋ก๊ทธ๋๋จธ์ค] ๊ฒ์ ๋งต ์ต๋จ๊ฑฐ๋ฆฌ'
date: '2023-02-03 00:00:00'
author: ๊ณ ๋ฐ
tags: ์๊ณ ๋ฆฌ์ฆ
categories: Algorithm
---

## 1. ๋ฌธ์ 

`ํ๋ก๊ทธ๋๋จธ์ค`

[๊ณ ๋์  Kit ๊ฒ์ ๋งต ์ต๋จ๊ฑฐ๋ฆฌ](https://school.programmers.co.kr/learn/courses/30/lessons/1844)


<br/>

## 2. ํต์ฌ ์์ด๋์ด

`BFS`

<br/>

## 3. ์ฝ๋

[swift]
```swift
import Foundation

func solution(_ maps: [[Int]]) -> Int {
    var maps = maps
    let n = maps[0].count
    let m = maps.count
    let dx: [Int] = [0,0,-1,1]
    let dy: [Int] = [1,-1,0,0]
    var queue: [(Int, Int)] = []
    queue.append((0,0))
    maps[0][0] = 1
    while !queue.isEmpty {
        let element = queue.removeFirst()
        let x = element.0
        let y = element.1
        for i in 0...3 {
            let dx = x + dx[i]
            let dy = y + dy[i]
            if dx >= 0 && dx < n && dy >= 0 && dy < m {
                if maps[dy][dx] == 0 {
                    continue
                }
                if maps[dy][dx] == 1 {
                    maps[dy][dx] = maps[y][x] + 1
                    queue.append((dx,dy))
                }
            }
        }
    }
    return maps[maps.endIndex - 1][maps.endIndex - 1] == 1 ? -1 : maps[maps.endIndex - 1][maps.endIndex - 1]
}
```

[python]
```python
from collections import deque

def solution(maps):
    n = len(maps[0])
    m = len(maps)
    direction = [(0,1), (0,-1), (1,0), (-1,0)]
    dq = deque()
    dq.append((0,0))
    maps[0][0] = 1
    while dq:
        x,y = dq.popleft()
        for direct in direction:
            dx = x + direct[0]
            dy = y + direct[1]
            if 0 <= dx < n and 0 <= dy < m:
                if maps[dy][dx] == 0:
                    continue
                if maps[dy][dx] == 1:
                    maps[dy][dx] = maps[y][x] + 1
                    dq.append((dx,dy))
    return maps[-1][-1] if maps[-1][-1] != 1 else -1
```

<br/>

## 4. ํ์ด ๊ณผ์ 

ํํ ๋ณด๋ BFS/DFS ํ์ ๋ฌธ์ ์๋ค!

`BFS`๋ก ์์ง ํ์ํ์ง ์์ ๊ฒฝ๋ก (maps[dx][dy] == 1 ์ธ ๊ฒฝ์ฐ) ์ ๋ฒฝ์ ํผํด์ฃผ๋ฉด์ ํ์ํ๋ฉด ๋์๋ค.

๊ทธ๋ ๊ฒ ์ฝ๊ฒ ๋ฌธ์ ๋ฅผ ํผ ๋ค์, DFS๋ก๋ ๋ฌธ์ ๋ฅผ ํ์ด๋ณด๋ ค ํ์๋๋ฐ...

`DFS` ๋ก๋ ๋ฌธ์ ๊ฐ ํ๋ฆฌ์ง ์์๋ค.

<br/>

[python]
```python
def solution(maps):
    n = len(maps[0])
    m = len(maps)
    direction = [(0,1), (0,-1), (1,0), (-1,0)]
    def DFS(x,y):
        if x == n - 1 and y == m - 1:
            return
        for direct in direction:
            dx = x + direct[0]
            dy = y + direct[1]
            if 0 <= dx < n and 0 <= dy < m:
                if maps[dy][dx] == 0:
                    continue
                if maps[dy][dx] == 1 or maps[y][x] + 1 < maps[dy][dx]:
                    maps[dy][dx] = maps[y][x] + 1
                    DFS(dx,dy)
    DFS(0,0)
    return maps[-1][-1] if maps[-1][-1] != 1 else -1
```

์ด DFS ์ฝ๋๊ฐ ์คํจํ๋ ์ด์ ๋ ํ์ํ๋ ๊ฒฝ๋ก๊ฐ ๋๋ฌด๋ ๋ง์์ง๊ธฐ ๋๋ฌธ์ด๋ค.

<br/>

![map.png](map.png)

์ด๋ฐ ํํ์ ๋งต์ด ์๋ค๊ณ  ๊ฐ์ ํ๋ค๋ฉด,

DFS๋ ๊ต์ฐจ๋ก (์, ์ค๋ฅธ์ชฝ, ์๋์ชฝ) ๋ฅผ ๋ชจ๋ 3^n * k (n๋ ์ผ๊ฑฐ๋ฆฌ์ ๊ฐ์, k๋ ์ผ๊ฑฐ๋ฆฌ์ ๊ฒฝ๋ก ๊ฐ์) ์ฐ์ฐ์ผ๋ก ํ์์ ํด์ผํ๊ธฐ ๋๋ฌธ์... ์๊ฐ๋ณต์ก๋๊ฐ ๋งํ๋ ๊ฒ์ด์๋ค.

<br/>

์ด์ฒ๋ผ ๋ฌธ์ ์์ ์ต๋จ ๊ฑฐ๋ฆฌ๋ฅผ ์ ๊ณตํ๋ค๋ฉด (๋ง์ง๋ง ์ข์ฐฉ์ง๊ฐ ์ ํด์ ธ์๊ณ  ๊ฐ์ค์น๊ฐ ์์) BFS๊ฐ ํ์คํ ์ข์ ์ ํ์ด๋ค ๋ผ๊ณ  ๋๊ผ๋ค.

<br/>


```toc

```
