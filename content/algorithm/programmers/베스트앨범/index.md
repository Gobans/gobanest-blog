---
emoji: ๐งถ
title: '[ํ๋ก๊ทธ๋๋จธ์ค] ๋ฒ ์คํธ ์จ๋ฒ'
date: '2022-12-30 14:00:00'
author: ๊ณ ๋ฐ
tags: ์๊ณ ๋ฆฌ์ฆ ํ๋ก๊ทธ๋๋จธ์ค
categories: Algorithm
---

## 1. ๋ฌธ์ 

`ํ๋ก๊ทธ๋๋จธ์ค`

[๊ณ ๋์  Kit ๋ฒ ์คํธ์จ๋ฒ](https://school.programmers.co.kr/learn/courses/30/lessons/42579)


<br/>

## 2. ํต์ฌ ์์ด๋์ด

Dictionary ๋ฅผ ์ด์ฉํ `ํด์`, `์ ๋ ฌ`.

<br/>

## 3. ์ฝ๋

```swift
import Foundation

func solution(_ genres:[String], _ plays:[Int]) -> [Int] {
    // ์ฅ๋ฅด๋ณ๋ก ์ฌ์ํ์์ ์ดํฉ์ ๊ตฌํ ํ ๋ด๋ฆผ์ฐจ์์ผ๋ก ์ ๋ ฌ
    var genrePlayCountDict: [String:Int] = [:]
    for (genre, play) in zip(genres, plays){
     if genrePlayCountDict[genre] != nil {
         genrePlayCountDict[genre]! += play
     } else {
         genrePlayCountDict[genre] = play
     }
    }
    let sortedGenrePlayCountDict = genrePlayCountDict.sorted(by: {$0.value > $1.value}).map{ $0.key }
    
    // ์ฅ๋ฅด๋ง๋ค ๋ฐ๋ชฉ๋ฌธ์ ๋๋ฉด์ ํด๋น song์ ๊ณ ์  ๋ฒํธ (idx) ๋ฅผ dictionary์ key๊ฐ, ์ฌ์ํ์๋ฅผ value๊ฐ์ผ๋ก ์ ์ฅ
    var bestAlbum: [Int] = []
    for genreName in sortedGenrePlayCountDict {
        var songPlayCountDict: [Int:Int] = [:]
        for (idx, genre) in genres.enumerated() {
            if genreName == genre {
                songPlayCountDict[idx] = plays[idx]
            }
        }
        // ์ฌ์ํ์๊ฐ ๊ฐ์ผ๋ฉด ๊ณ ์ ๋ฒํธ๊ฐ ๋ฎ์ ์์ผ๋ก ์ ๋ ฌ, ๊ทธ์ธ์๋ ์ฌ์ํ์์ ๋ด๋ฆผ์ฐจ์์ผ๋ก ์ ๋ ฌ
        let sortedSongPlayCountDict = songPlayCountDict.sorted{ (f,s) -> Bool in
            if f.value == s.value {
                return f.key < s.key
            }
            return f.value > s.value
        }.map { $0.key }
        // bestAlbum์ ์ต๋ ์๋ก ํ์๊ฐ 2๋ฒ์ด๊ธฐ ๋๋ฌธ์ maxAddCount๋ก ์๋ก ํ์ ์ ์ด
        var maxAddCount = 2
        for songNum in sortedSongPlayCountDict {
            maxAddCount -= 1
            bestAlbum.append(songNum)
            if maxAddCount == 0 {
                break
            }
        }
    }
    return bestAlbum
}

```

<br/>

## 4. ํ์ด ๊ณผ์ 

๋ฌธ์ ์์ ๋ชํํ ๋ฌธ์ ํด๊ฒฐ์ ํ๋ฆ์ ์ค๋ค.

1. ์ํ ๋ธ๋๊ฐ ๋ง์ด ์ฌ์๋ ์ฅ๋ฅด๋ฅผ ๋จผ์  ์๋กํฉ๋๋ค.
2. ์ฅ๋ฅด ๋ด์์ ๋ง์ด ์ฌ์๋ ๋ธ๋๋ฅผ ๋จผ์  ์๋กํฉ๋๋ค.
3. ์ฅ๋ฅด ๋ด์์ ์ฌ์ ํ์๊ฐ ๊ฐ์ ๋ธ๋ ์ค์์๋ ๊ณ ์  ๋ฒํธ๊ฐ ๋ฎ์ ๋ธ๋๋ฅผ ๋จผ์  ์๋กํฉ๋๋ค.

์ด๋ฅผ ๊ทธ๋๋ก ์ฝ๋์ ํ๋ก์ฐ๋ก ์ฎ๊ธด๋ค๋ฉด

1. ์ฅ๋ฅด์ ์ํ ๋ธ๋์ ์ฌ์ํ์๋ฅผ ๊ตฌํ๋ค. ์ด๋ฅผ ์ฌ์ํ์์ ๋ด๋ฆผ์ฐจ ์์ผ๋ก ์ ๋ ฌํ๋ค.
2. ์ ๋ ฌ๋ ์ฅ๋ฅด์ ์์์ ๋ฐ๋ผ ๊ฐ์ฅ ๋ง์ด ์ฌ์๋ ๋ธ๋๋ฅผ ์๋กํ๋ค. <br/>(์ฌ์ ํ์๊ฐ ๊ฐ๋ค๋ฉด ๊ณ ์  ๋ฒํธ๊ฐ ๋ฎ์ ๋ธ๋ ์ฐ์ )

๋ฐ๋ผ์ ํ์ํ ๊ฒ์ `์ฅ๋ฅด๋ณ ์ฌ์ํ์ ๋ด๋ฆผ์ฐจ์ ๋ฐฐ์ด`, `์ฌ์ํ์, ๊ณ ์  ๋ฒํธ๋ฅผ ๊ธฐ์ค์ผ๋ก ์ ๋ ฌ๋ ๋ฐฐ์ด` ์ด ๋๊ฐ์ง์ด๋ค.

์ด ๋ฐฐ์ด๋ค์ ๋ง๋ค๋ `ํด์` ์ `์ ๋ ฌ`๋ฅผ ์ฌ์ฉํ์๋ค.



<br/>

## 5. ๋ค๋ฅธ ์ฌ๋์ ์ฝ๋

```swift
import Foundation

func solution(_ genres:[String], _ plays:[Int]) -> [Int] {
    var playList = [String:(play: Int, music: [Int:Int])]()
    var answer = [Int]()

    for (index, value) in genres.enumerated() {
        if let genre = playList[value]?.play {
            playList[value]?.play = genre + plays[index]
            playList[value]?.music[index] = plays[index]
        } else {
            playList[value] = (play: plays[index], music: [index:plays[index]])
        }
    }

    let rank = playList.sorted(by: { $0.value.play > $1.value.play })

    rank.forEach { song in
        let songRank = song.value.music.sorted{$0.key < $0.key }.sorted { $0.value > $01.value }

        let max = songRank.count > 1 ? 2 : 1
        for i in 0..<max {
            answer.append(songRank[i].key)
        }
    }

    return answer
}

```

ํ๋์ dictionary ์์ ํํ ํํ๋ก play, music ๋๊ฐ๋ฅผ ๋๋ ๊ฒ์ด ์ธ์์ ์ด์๋ค.

์์ฃผ ๊น๋ํ๋ฏ!

<br/>


```toc

```
