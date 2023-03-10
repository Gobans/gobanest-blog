---
emoji: ๐งถ
title: '[ํ๋ก๊ทธ๋๋จธ์ค] ๋ ๋งต๊ฒ'
date: '2023-01-02 00:00:00'
author: ๊ณ ๋ฐ
tags: ์๊ณ ๋ฆฌ์ฆ ํ๋ก๊ทธ๋๋จธ์ค
categories: Algorithm
---

## 1. ๋ฌธ์ 

`ํ๋ก๊ทธ๋๋จธ์ค`

[๊ณ ๋์  Kit ๋ ๋งต๊ฒ](https://school.programmers.co.kr/learn/courses/30/lessons/42626)


<br/>

## 2. ํต์ฌ ์์ด๋์ด

`ํ`์ ์ด์ฉํ `์ฐ์  ์์ ํ`

<br/>

## 3. ์ฝ๋

> [python]

```python
import heapq

def solution(scoville, k):
    heap = []
    for num in scoville:
        heapq.heappush(heap, num)
    mix_cnt = 0
    while heap[0] < k:
        try:
            heapq.heappush(heap, heapq.heappop(heap) + (heapq.heappop(heap) * 2))
        except IndexError:
            return -1
        mix_cnt += 1
    return mix_cnt

```

[์ฝ๋ ์ถ์ฒ](https://itholic.github.io/kata-more-spicy/)

<br/>

## 4. ํ์ด ๊ณผ์ 

> [python]

```python
def solution(scoville, K):
    lowestScoville = min(scoville)
    is_made = False
    cnt = 0
    if lowestScoville >= K:
        return 0
    while len(scoville) >= 2:
        scoville.sort(reverse=True)
        newScoville = scoville.pop() + (scoville.pop() * 2)
        scoville.append(newScoville)
        cnt += 1
        if min(scoville) >= K:
            is_made = True
            break
    print(scoville)
    if is_made:
        return cnt
    return -1

```

ํ๋ก์ฐ๋ฅผ ๋ค์๊ณผ ๊ฐ์ด ์๊ฐํ๋ค.

    1. ์ค์ฝ๋น ์ง์๊ฐ ๊ฐ์ฅ ๋ฎ์ ๋ ๊ฐ์ ์์ ์กฐํฉ
    2. ๊ณต์: newScoville = lowestScoville + (lowestSecondScoville * 2)
    3. ํด๋น ๋์์ ๋ชจ๋  ์์์ ์ค์ฝ๋น ์ง์๊ฐ K ์ด์์ด ๋ ๋๊น์ง ๋ฐ๋ณต.
    4. -> ์ต์ ๋ฐ๋ณต ํ์๋ฅผ ๋ฆฌํด
    5. ๋ง๋ค ์ ์๋ ๊ฒฝ์ฐ -1 ๋ฆฌํด

ํ์ ์ด์ฉํ `์ฐ์  ์์ ํ` ๋ฅผ ์๋ชฐ๋ผ์ ์๊ฐ์ด๊ณผ ๋  ๊ฒ์ ์์ํ์ง๋ง, `์ ๋ ฌ` ์ ์ฌ์ฉํด ์ผ๋จ ํ์๋ค.

์ญ์๋ ์๊ฐ์ด๊ณผ์๊ณ , ๋ธ๋ก๊ทธ๋ฅผ ์ฐธ๊ณ ํ๊ธฐ๋ก ํ๋ค.

[์๊ณ ๋ฆฌ์ฆ](https://suyeon96.tistory.com/31)

๋ณด๊ณ  ์ด๋ค ๊ฒ์ธ์ง ๋์ถฉ ์ดํด๋ฅผ ํ๋๋ฐ, ํ๋ฒ Swift ๋ก heap ์ ์ด์ฉํด ์ฐ์ ์์ ํ๋ฅผ ๊ตฌํํด๋ด์ผ๊ฒ ๋ค๊ณ  ์๊ฐํ๋ค.

์ผ๋จ ํ์ด์ฌ์ ๋ค๋ฅธ์ฌ๋์ ์ฝ๋๋ฅผ ์ ์๋๋ฐ, ํด๋น ์ฝ๋๋ฅผ ๋ฐํ์ผ๋ก Swift ๋ก heap์ ์ด์ฉํด ์ฐ์ ์์ํ๋ฅผ ๊ตฌํํด๋ณด๊ธฐ๋ก ํ๋ค.

<br/>

> [swift]

```swift
import Foundation

func solution(scoville: [Int], k: Int) -> Int {
    var pq = PriorityQueue(sort: <, elements: scoville)
    var cnt = 0
    while let peek = pq.peek, peek < k {
        if let lowestScoville = pq.dequeue(), let secondLowestScoville = pq.dequeue() {
            let newScoville = lowestScoville + (secondLowestScoville * 2)
            pq.enqueue(newScoville)
        } else {
            return -1
        }
        cnt += 1
    }
    return cnt
}

// Below structs are used data strcutre. 'PriorityQueue' and 'Heap'

struct PriorityQueue<Element: Equatable> {
    private var heap: Heap<Element>

    init(sort: @escaping (Element, Element) -> Bool,
        elements: [Element] = []) {
        heap = Heap(sort: sort, elements: elements)
    }

    var isEmpty: Bool {
        return heap.isEmpty
    }

    var peek: Element? {
        return heap.peek()
    }

    mutating func enqueue(_ element: Element) {
        heap.insert(element)
    }

    mutating func dequeue() -> Element? {
        return heap.remove()
    }

}



struct Heap<Element: Equatable> {
    var elements: [Element] = []
    let sort: (Element, Element) -> Bool

    init(sort: @escaping (Element, Element) -> Bool, elements: [Element] = []) {
        self.sort = sort
        self.elements = elements

        if !elements.isEmpty {
            for i in stride(from: elements.count / 2 - 1, through: 0, by: -1) {
                siftDown(from: i)
            }
        }
    }

    var isEmpty: Bool {
        return elements.isEmpty
    }

    var count: Int {
        return elements.count
    }

    func peek() -> Element? {
        return elements.first
    }

    func leftChildIndex(ofParentAt index: Int) -> Int {
        return (2 * index) + 1
    }

    func rightChildIndex(ofParentAt index: Int) -> Int {
        return (2 * index) + 2
    }

    func parentIndex(ofChildAt index: Int) -> Int {
        return (index - 1) / 2
    }

    mutating func remove() -> Element? {
        guard !isEmpty else {
            return nil
        }
        elements.swapAt(0, count - 1)
        defer {
            siftDown(from: 0)
        }
        return elements.removeLast()
    }

    mutating func remove(at index: Int) -> Element? {
        guard index < elements.count else {
            return nil
        }
        if index == elements.count - 1 {
            return elements.removeLast()
        } else {
            elements.swapAt(index, elements.count - 1)
            defer {
            siftDown(from: index)
            siftUp(from: index)
            }
        return elements.removeLast()
      }
    }

    mutating func insert(_ element: Element) {
        elements.append(element)
        siftUp(from: elements.count - 1)
    }

    func index(of element: Element, startingAt i: Int) -> Int? {
        if i >= count {
            return nil
        }
        if sort(element, elements[i]) {
            return nil
        }
        if element == elements[i] {
            return i
        }
        if let j = index(of: element, startingAt: leftChildIndex(ofParentAt: i)) {
            return j
        }
        if let j = index(of: element, startingAt: rightChildIndex(ofParentAt: i)) {
            return j
        }
        return nil
    }

    mutating func siftDown(from index: Int) {
        var parent = index
        while true {
            let left = leftChildIndex(ofParentAt: parent)
            let right = rightChildIndex(ofParentAt: parent)
            var candidate = parent // 4
            if left < count && sort(elements[left], elements[candidate]){
                candidate = left // 5
            }
            if right < count && sort(elements[right], elements[candidate]) {
                candidate = right // 6
            }
            if candidate == parent {
                return // 7
            }
        elements.swapAt(parent, candidate) // 8
        parent = candidate
        }
    }

    mutating func siftUp(from index: Int) {
        var child = index
        var parent = parentIndex(ofChildAt: child)
        while child > 0 && sort(elements[child], elements[parent]) {
            elements.swapAt(child, parent)
            child = parent
            parent = parentIndex(ofChildAt: child)
        }
    }

}


```

heap ๊ณผ priorityQueue ์ ๊ตฌํ์ `Data Structures and Algorithms in Swift - Implementing practical data structures with Swift 4` ๋ฅผ ์ฐธ๊ณ ํ์๋ค.


```toc

```
