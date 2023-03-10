---
emoji: ๐งถ
title: '[ํ๋ก๊ทธ๋๋จธ์ค] ๋์คํฌ ์ปจํธ๋กค๋ฌ'
date: '2023-01-05 00:00:00'
author: ๊ณ ๋ฐ
tags: ์๊ณ ๋ฆฌ์ฆ
categories: Algorithm
---

## 1. ๋ฌธ์ 

`ํ๋ก๊ทธ๋๋จธ์ค`

[๊ณ ๋์  Kit ๋์คํฌ ์ปจํธ๋กค๋ฌ](https://school.programmers.co.kr/learn/courses/30/lessons/42627)


<br/>

## 2. ํต์ฌ ์์ด๋์ด

`์ ๋ ฌ`, `SFJ` (์ต์ ์์ ์ฐ์  ์ค์ผ์ค๋ง)

<br/>

## 3. ์ฝ๋

[swift] `์ ๋ ฌ`
```swift
func solution(_ jobs:[[Int]]) -> Int {
    var now = 0
    var totalTime = 0
    var sortedJobs = jobs.sorted(by: { ($0[1], $0[0]) < ($1[1], $1[0])})
    
    while !sortedJobs.isEmpty {
        var isRemoved = false
        for i in 0..<sortedJobs.count {
            if sortedJobs[i][0] <= now {
                now += sortedJobs[i][1]
                totalTime += now - sortedJobs[i][0]
                sortedJobs.remove(at: i)
                isRemoved = true
                break
            }
        }
        if !isRemoved {
            now += 1
        }
    }
    return totalTime / jobs.count
}
```

[swift] `Heap`
```swift
func solution(_ jobs:[[Int]]) -> Int {
    var now = 0
    var totalTime = 0
    var cJobs = jobs
    var sortedJobs = Heap (sort: { (lhs: [Int], rhs: [Int]) in
        return (lhs[1], lhs[0]) < (rhs[1], rhs[0])
    })
    while !cJobs.isEmpty || !sortedJobs.isEmpty {
        var tempJobs: [[Int]] = []
        for job in cJobs {
            if job[0] <= now {
                sortedJobs.insert(job)
            } else {
                tempJobs.append(job)
            }
        }
        cJobs = tempJobs
        if !sortedJobs.isEmpty {
            let job = sortedJobs.remove()!
            now += job[1]
            totalTime += now - job[0]
        } else {
            now += 1
        }
    }
    return totalTime / jobs.count
}

```

<br/>

## 4. ํ์ด ๊ณผ์ 

์ฒ์์๋ `์์  ํ์`, `์ต์๊ฒฝ๋ก ํ์` ๋ฌธ์ ์ธ์ค ์์๋ค..

๊ทธ๋ฐ๋ฐ ๋ฌธ์ ์ ์๊ตฌ์ฌํญ๊ณผ ์ ํ์ฌํญ์ ๋ง์กฑํ๋ ์กฐ๊ฑด
- ์์ฒญ๋ถํฐ ์ข๋ฃ๊น์ง ๊ฑธ๋ฆฐ ์๊ฐ์ ์ต์
- ๋จผ์  ์์ฒญ์ด ๋ค์ด์จ ์์๋ถํฐ ์ฒ๋ฆฌ

์ด ๋๊ฐ์ง๋ฅผ ๋ง์กฑ ํ๋ ค๋ฉด `๊ทธ๋ฆฌ๋`์ ๊ฐ์ ์๊ณ ๋ฆฌ์ฆ์ผ๋ก,

- ํ์ฌ ์์ฒญ ์๊ฐ์ ๋ง์กฑํ๊ณ  (์์์ ์์ํ  ์ ์๊ณ )
- ๊ทธ ์ค ๊ฐ์ฅ ๋นจ๋ฆฌ ๋๋๋ ์์

์ ์ ํํ๋ฉฐ ์์์ ์ํํ๋ฉด ๋์๋ค.

<br/>

๊ทธ๋ฐ๋ฐ ์ด๋ค์์ผ๋ก ์ฒ๋ฆฌํ ์ง ๊ฐ์ด ์์กํ [๋ธ๋ก๊ทธ](https://didu-story.tistory.com/323) ๊ธ์ ์ฐธ๊ณ ํ๋ค.

๊ทธ๋ ๊ฒ ํด์ ์์ ๊ฐ์ด `์ ๋ ฌ`์ ์ฌ์ฉํ ์ฝ๋๋ฅผ ์์ฑํ๋๋ฐ, programmers ์์๋ ๋ถ๋ฅ๊ฐ `heap` ์ผ๋ก ๋์ด์์ด์ heap ์ผ๋ก ๋ค์ ํ์ด๋ดค๋ค.


|<center>heap<center/>|<center>sort<center/>|
| :---: | ---: | 
|![heap.png](heap.png)|![sort.png](sort.png)|

๊ทธ๋ฐ๋ฐ sortedJobs ์ tempJobs ์ ๊ฐ๊ฐ append ํ๋ ๋ฐฉ์ ๋๋ฌธ์ธ์ง, ์๊ฐ์ด ์คํ๋ ค ๋ ๊ฑธ๋ ธ๋ค. tempJobs ๋ฅผ ์์ ๊ณ  ๊ตฌํ์ ํ ์๋ ์์ ๊ฒ ๊ฐ์๋ฐ... ํ๋ฒ ๊ณ ๋ฏผ์ ๋ค์ ํด๋ด์ผ๊ฒ ๋ค.

์ด๋ฐ ์ํฉ์ ๋ณด๊ณ  ์ํฉ์ ์๋ง์ ์๋ฃ๊ตฌ์กฐ๋ฅผ ์ฐ๋๊ฒ ์ ๋ง ์ค์ํ๋ค๊ณ  ๋๊ผ๋ค. 

<br/>

## ๊ณ ๋ฏผ ํ (2023.02.26)

tempJobs ๋ฅผ ์์ ๊ณ , ์์ ์๊ฐ์ผ๋ก ์ ๋ ฌ๋ jobs๋ฅผ ๊ธฐ๋ฐ์ผ๋ก heap์ job์ ๋ฃ์ด์ฃผ๋ ์ฝ๋๋ก ์๋กญ๊ฒ ์์ฑํด๋ณด์๋ค.

<br/>

```swift
func solution(_ jobs:[[Int]]) -> Int {
    var now = 0
    var totalTime = 0
    var cJobs = jobs.sorted(by: { $0[0] > $1[0] })
    var sortedJobs = Heap (sort: { (lhs: [Int], rhs: [Int]) in
        return (lhs[1], lhs[0]) < (rhs[1], rhs[0])
    })
    while !cJobs.isEmpty || !sortedJobs.isEmpty {
        while !cJobs.isEmpty && cJobs.last![0] <= now {
            sortedJobs.insert(cJobs.removeLast())
        }
        if !sortedJobs.isEmpty {
            let job = sortedJobs.remove()!
            now += job[1]
            totalTime += now - job[0]
        } else {
            now += 1
        }
    }
    return totalTime / jobs.count
}
```

<br/>

๊ทธ ๊ฒฐ๊ณผ...


<br/>

![refactorHeap.png](refactorHeap.png)

<br/>

์คํ๋ ค ์๊ฐ์ด ๋ ๋์๋ค..ใใ

```swift
var cJobs = jobs.sorted(by: { $0[0] > $1[0] })
```

๋ณด๊ธฐ์๋ ์๋กญ๊ฒ ๋ฆฌํฉํ ๋งํ ์ฝ๋๊ฐ ํจ์ฌ ๊น๋ํ๋ฐ

์ ๋ ฌ์ ํ๋ฒ ๋ ํด์ผํด์ ์๊ฐ์ด ์คํ๋ ค ์ฆ๊ฐํ ๊ฒ ๊ฐ๋ค...

<br/>

๊น๋ + ์ฑ๋ฅ ํฅ์์ ๋ชปํ์ง๋ง

์ค๋๋ง์ ์งฐ๋ ์ฝ๋ ๋ค์ ๋ฏ์ด๋ณด๊ณ  ๊ณ ์ณ๋ณด๋๊น ์ฌ๋ฏธ์์๋ค.

```toc

```
