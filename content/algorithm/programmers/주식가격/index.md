---
emoji: ๐งถ
title: '[ํ๋ก๊ทธ๋๋จธ์ค] ์ฃผ์๊ฐ๊ฒฉ'
date: '2022-12-31 14:30:00'
author: ๊ณ ๋ฐ
tags: ์๊ณ ๋ฆฌ์ฆ
categories: Algorithm
---

## 1. ๋ฌธ์ 

`ํ๋ก๊ทธ๋๋จธ์ค`

[๊ณ ๋์  Kit ์ฃผ์๊ฐ๊ฒฉ](https://school.programmers.co.kr/learn/courses/30/lessons/42584)


<br/>

## 2. ํต์ฌ ์์ด๋์ด

`Queue` ๋ฅผ ์ด์ฉํ ๋ฐ๋ณต๋ฌธ.

`startIndex`, `endIndex` ๋ฅผ ์ฌ์ฉํ์ฌ ๋ฐฐ์ด ์ฌ๋ผ์ด์ฑ.

**์ฃผ์: endIndex ๋ ์ค์  ์ฌ์ฉํ  ์ ์๋ Index + 1 ์ ๋ฐํํจ**

๊ทธ๋์ `..<` ์ ๊ฐ์ด ์ฐ๋ผ๋๋ฐ, ์ ์ด๋ ๊ฒ ๊ตฌํ๋์์๊น? ์..

![endIndex.png](endIndex.png)


<br/>

## 3. ์ฝ๋

Python

```python
from collections import deque

def solution(prices):
    answer = []
    dPrice = deque(prices)
    while dPrice :
        price = dPrice.popleft()
        sec = 0
        for q in dPrice:
            sec += 1
            if price > q:
                break
        answer.append(sec)
    return answer

```

<br/>

Swift
```swift
func solution(prices: [Int]) -> [Int] {
    var answer: [Int] = []
    let dPrice: [Int] = prices
    var index = dPrice.startIndex
    let lastIndex = dPrice.endIndex
    while (index < lastIndex) {
        let price = dPrice[index]
        var sec = 0
        for q in dPrice[index + 1..<lastIndex] {
            sec += 1
            if price > q {
                break
            }
        }
        index += 1
        answer.append(sec)
    }
    return answer
}
```

Swift ์๋ ํ์ด์ฌ์ `Queue` ๊ฐ ์์ด์ `startIndex`, `endIndex` ๋ฅผ ์ด์ฉํ์ฌ ๋ฐฐ์ด ์ฌ๋ผ์ด์ฑ์ ํ๋ค.

<br/>

## 4. ํ์ด ๊ณผ์ 

์ผ๋จ ํด๋น ๋ฌธ์ ์์ Swift ์ฑ์ ์ ์ง์ํ์ง ์์๊ธฐ ๋๋ฌธ์, ํ์ด์ฌ์ผ๋ก ๋จผ์  ๊ตฌํํ ํ Swift ์ฝ๋๋ก ๋ฐ๊ฟจ๋ค.

```python
from collections import deque

def solution(prices):
    answer = [0] * len(prices)
    dPrice = deque([])
    for idx, price in enumerate(prices):
        dPrice.append((price, 0, idx))
        for _ in range(len(dPrice)):
            element = dPrice.popleft()
            newElement = (element[0], element[1] + 1, element[2])
            answer[newElement[2]] = element[1]
            if element[0] <= price:
                dPrice.append(newElement)
    return answer

```

answer ๋ฐฐ์ด์ ๋ฏธ๋ฆฌ ๋ง๋ค์ด ๋๊ณ , ์ฃผ์ ๊ฐ๊ฒฉ์ deque ์ ์ฐจ๋ก๋๋ก ๋ฃ์ด๊ฐ๋ฉฐ ๋ฐ๋ณต๋ฌธ์ผ๋ก ๊ฐ๊ฒฉ์ ๊ฒ์ฆ & answer ๋ฐฐ์ด์ ์๋ฐ์ดํธ ํ๋ ค๊ณ  ํ๋๋ฐ ํด๋น ๋ฐฉ์์์ ๋นํจ์จ์ ์ธ ์ฝ์๊ณผ ์ญ์ ๊ฐ ์ผ์ด๋ฌ๊ณ , ์๊ฐ์ด๊ณผ๋ฅผ ์ด๋ํ๋ค.

๊ทธ๋ฆฌ๊ณ  ๊ธธ์ ์์ด์ ์ด๋ป๊ฒ ํ์ด์ผํ ์ง ๊ฐ์ด ์์กํ๋ค..

๊ทธ๋์ ๋ค๋ฅธ ์ฌ๋์ ์ฝ๋๋ฅผ ์ฐธ๊ณ ํ๋ค. [์ฐธ๊ณ  ์ฝ๋](https://velog.io/@soo5717/ํ๋ก๊ทธ๋๋จธ์ค-์ฃผ์๊ฐ๊ฒฉ-Python)๋ฅผ ๋ฐํ์ผ๋ก ์๋จ์ ํ์ด ์ฝ๋๊ฐ ์์ฑ๋์๋ค. ๋ถํ์ํ ์ฝ์, ์ญ์  ์์ด ํจ์ฌ ๊ฐ์ํ ๋์๋ค.

๋ฌธ์ ๋ฅผ ๋ณด๊ณ  ์ต์ ํ ๋ ์ฝ๋๋ฅผ ๋ฐ๋ก ์๊ฐํ๊ธฐ๋ ์ด๋ ค์ด ๊ฒ ๊ฐ๋ค. ์๋ง ๋ด๊ฐ ๊ตฌํ์ ๊ธ๊ธํ์ฌ ๊น๊ฒ ํ๋ก์ฐ๋ฅผ ์ ํ์ง ์์์ ์๊ธฐ๋ ๋ฌธ์ ๊ฐ ์๋๊น ๋ฐ์ฑํ๋ค. ๋ค์์๋ ๋ฌธ์ ๋ฅผ ํ๋

<strog>

1. ๋ฌธ์  ํด๊ฒฐ์ ํ์ํ ํ๋ก์ฐ๋ฅผ ์๊ฐํ๋ค.
2. ํด๋น ํ๋ก์ฐ์ ์ ํฉํ ์๋ฃ๊ตฌ์กฐ, ์๊ณ ๋ฆฌ์ฆ์ ์๊ฐํ๋ค.
3. ์ถ๊ฐ์ ์ผ๋ก ํ์ํ ๋ณ์๋ฅผ ์๊ฐํ๋ค.

</strong>
์ด๋ ๊ฒ ์ฝ๋๋ฅผ ์์ฑํ๊ธฐ ์ ์ ์๊ฐ์ ํ ํ ํ์ด์ผ๊ฒ ๋ค.

<br/>

## 5. ๋ค๋ฅธ ์ฌ๋์ ์ฝ๋

```python
def solution(prices):
    length = len(prices)
    
    # answer์ max๊ฐ์ผ๋ก ์ด๊ธฐํ  
    answer = [ i for i in range (length - 1, -1, -1)]
    
    # ์ฃผ์ ๊ฐ๊ฒฉ์ด ๋จ์ด์ง ๊ฒฝ์ฐ ์ฐพ๊ธฐ
    stack = [0]
    for i in range (1, length):
        while stack and prices[stack[-1]] > prices[i]:
            j = stack.pop()
            answer[j] = i - j
        stack.append(i)
    return answer

```


[์ด๊ณณ](https://velog.io/@soo5717/ํ๋ก๊ทธ๋๋จธ์ค-์ฃผ์๊ฐ๊ฒฉ-Python)์ ์๋ ์ฝ๋์ธ๋ฐ, stack ์ ์ฌ์ฉํ์ฌ ํ์ํ ๋๋ง ์ฐ์ฐํ๋๊ฒ ๊ธฐ๋ฐํ๊ณ  ์ข์ ๋ฐฉ๋ฒ์ด์๋ค. ์์ฃผ ์ฐฝ์์ ์ด์ผ..


<br/>


```toc

```
