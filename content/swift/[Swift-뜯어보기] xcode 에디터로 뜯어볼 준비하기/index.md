---
emoji: ๐ง
title: '[Swift-๋ฏ์ด๋ณด๊ธฐ] xcode ์๋ํฐ๋ก ๋ฏ์ด๋ณผ ์ค๋นํ๊ธฐ'
date: '2023-02-06 00:00:00'
author: ๊ณ ๋ฐ
tags: Swift
categories: Swift
---

# ๋ค์ด๊ฐ๋ฉด์

<br/>

Swift ๋ open source ์๋๋ค.

์์ฃผ ์ ๊ทผ์ด ์ฌ์ด ํ์ ์ธ์ด์ฃ .

<br/>

![๊ทธ๋ฐ๋ฐ_๋ง์๋๋ค.png](๊ทธ๋ฐ๋ฐ_๋ง์๋๋ค.png)

<center>๊ทธ๋ฐ๋ฐ ๋ง์๋๋ค. </center>

<br/>

์ด ์คํ์์ค ์ฝ๋๋ฅผ ์น์์์ ๋ฏ์ด๋ณด๋ ค๋ฉด.. ์ ๋ง ์์ฒญ ํ๋ค๊ณ  ์ฌ์ค์ ๋ถ๊ฐ๋ฅ์ ๊ฐ๊น๋ค.

<br/>

ํน์ ํ ์๋ฃ๊ตฌ์กฐ, ๊ธฐ๋ฅ์ด ๊ถ๊ธํ๋ฐ ํ๋์ ๋ฉ์๋ ์์์ ๋ค๋ฅธ ์ฌ๋ฌ ๋ฉ์๋ค์ด ์ค์ฒฉ์ผ๋ก ์ฌ์ฉ๋๊ณ  ์๊ณ .. ์ฌ๋ฌ ํ๋กํ ์ฝ์ ์ค์ํ๊ณ .. ํ๋กํ ์ฝ ๋ฉ์๋๋ ์ฌ์ฉํ๊ณ ..

<br/> 

์ด๊ฑธ ์ ๋ง ํ๋ํ๋ ์น์์์ ์ฐพ์๊ฐ๋ฉด์ ํน์ ๋ก์ปฌ์์ ํด๋น swift ํ์ผ์ ์ด์ด์ ๋ฏ์ด๋ณด๊ธฐ๋ ๋ถ๊ฐ๋ฅํ๋ค.

<br/>

๊ทธ๋์ ์ด๋ฒ ํฌ์คํธ์์ Swift ๋ฅผ ๋น๋ํ์ฌ xcode๋ก ์ด์ด ๋ฏ์ด๋ณผ ์ ์๋ ๋ฐฉ๋ฒ์ ์๊ฐํ๊ณ ์ ํ๋ค.

<br/>

# Swift ๋น๋

> macOS ๊ธฐ์ค ์ํ ๋ฐฉ๋ฒ์! <br/> ๋ค๋ฅธ OS ๋ [์ด๊ณณ](https://github.com/apple/swift/blob/main/docs/HowToGuides/GettingStarted.md) ๊ฐ์ด๋๋ฅผ ์ฐธ์กฐํด์ผํจ.

<br/>

Swift ๋ ์ฌ๋ฌ OS, Architecture ๋ฅผ ์ง์ํ๊ณ  ์๋ค. ๊ทธ๋ฆฌ๊ณ  ์ฌ๋ฌ ํ๊ฒฝ์ ๋ง์ถฐ ๋น๋๋ฅผ ํ  ์ ์๋๋ก ๋น๋ ์คํฌ๋ฆฝํธ๋ฅผ ์ ๊ณตํด์ค๋ค.

๋ค๋ง ๋น๋์ ํ์ํ Swift์ Dependency์ ์ปดํ์ผ ํด์ ์ง์  ์ค์นํด์ผํ๋ค.

ํ๋์ฉ ํด๋ณด์!

<br/>

## ์ค๋น๋ฌผ

1. python 3
2. Git 2.x
3. ๋์คํฌ ์ฉ๋ 5GB ~ 70 GB (๋๋ ๋น๋ ํ 65GB ์ฌ์ฉ์ค์ด๋ค.)
4. ์๊ฐ... ๋น๋ํ๋๋ฐ 20 ~ 30๋ถ ์ ๋ ๊ฑธ๋ฆผ
5. CMake, Ninja

<br/>

์ด์ค [CMake](https://cmake.org) ์ [Ninja](https://ninja-build.org) ๋ ์๋์ ๊ฐ์ ๋ช๋ น์ด๋ก ์ค์น ๊ฐ๋ฅ.

```
brew install cmake ninja
```

<br/>

> ๋ง์ฝ swift ์คํ์์ค์ ๊ธฐ์ฌํ  ๋ชฉ์ ์ด๋ผ๋ฉด ๋ ๋ค๋ฅด๊ฒ ์ํ์ ํด์ค์ผํจ. [์ด๊ณณ](https://github.com/apple/swift/blob/main/docs/HowToGuides/GettingStarted.md) ๊ฐ์ด๋๋ฅผ ์ฐธ์กฐ.


<br/>

## ํ๋ก์ ํธ ๋ฐ๊ธฐ

<br/>

์ค๋น๋ฅผ ๋ค ํ์ผ๋ Swift์ ํ์ํ Dependency๋ค์ ๋ฐ์๋ณด์.

<br/>

```
mkdir swift-project
cd swift-project
```

์ ๋นํ ๊ณณ์ swift-project ํด๋๋ฅผ ๋ง๋ค๊ณ  ๋ค์ด๊ฐ์ฃผ์.

<br/>

```
git clone https://github.com/apple/swift.git swift
cd swift
utils/update-checkout --clone
```

๊ทธ๋ฆฌ๊ณ  swift๋ฅผ ํด๋ก ํ ํ `utils/update-checkout --clone` ๋ช๋ น์ด๋ก Dependency๋ค์ ํด๋ก ํด์ฃผ์.

<br/>

๊ทธ ํ 

```
ls ..
```

๋ช๋ น์ด๋ก ์์ ํด๋์ ๋ฐ์์ง Dependency๋ฅผ ํ์ธํด๋ณด๋ฉด

<br/>

![terminal_ls.png](terminal_ls.png)

์ด๋ฐ์์ผ๋ก ๋ง์ ํ์ผ๋ค์ด ๋ฐ์์ง ๊ฒ์ ํ์ธํ  ์ ์๋ค.

<br/>

๊ทธ ๋ค์

```
utils/build-script --skip-build-benchmarks \
  --skip-ios --skip-watchos --skip-tvos --swift-darwin-supported-archs "$(uname -m)" \
  --release-debuginfo --swift-disable-dead-stripping
```

์ด ๋ช๋ น์ด๋ก ToolChain ์ ๋ง๋ค์ด์ฃผ๊ณ 

<br/>

```
utils/build-script --swift-darwin-supported-archs "$(uname -m)" --xcode --clean
```

์ด ๋ช๋ น์ด๋ก xcodeproj ํ์ผ์ ์์ฑํ  ์ ์๋ค.


<br/>

๊ทธ ๋ค์ swift-project ํด๋์์ ์์ฑ๋ 

build -> Xcode-MinSizeRelAssert -> swift-macosx-arm64 -> stlib ์์ xcodeproj๋ฅผ ์ด์ด์ฃผ๋ฉด ๋๋ค.

<br/>

๊ทธ๋ฌ๋ฉด ์ด๋ ๊ฒ swift source ํ์ผ๋ค์ ๋ณผ ์ ์๋ค.

![sources.png](sources.png)


๋นจ๊ฐ์์ผ๋ก ๋์ด์๋ ํ์ผ๋ค์ .gyb ํ์ฅ์๋ฅผ ๊ฐ์ง ๋์๋ค์ธ๋ฐ..

Swift team ์์ ๋น๋ ์ ๋ธ๊ฐ๋ค๋ฅผ ์ค์ด๋ ค๊ณ  ์ด๋ฐ ํ์ฅ์๋ฅผ ์ฌ์ฉํ ๊ฒ์ด๋ผ๊ณ  ํ๋ค.

https://forums.swift.org/t/what-are-swift-gyb-files/303

<br/>

๊ทผ๋ฐ ์๋ ๋น๋๋ฅผ ํ๋์ง ์ ๋ชจ๋ฅด๊ฒ ๋ค..

์ผ๋จ ๊นํ์์ ๋ณด๋๊ฑธ๋ก..ใ

<br/>

์๋ฌดํผ ์ฌ๊ธฐ๊น์ง ํ์ผ๋ฉด ์ด์  ์์ค ํ์ผ๋ค์ jump to definition ์ผ๋ก ๋ฏ์ด๋ณผ ์ ์๋ค!!

![jumpToDefinition.png](jumpToDefinition.png)


๐๐๐๐

<br/>

# ๋๋ฒ๊ทธ

์ถ๊ฐ๋ก Swift๋ฅผ ๋๋ฒ๊ทธํ๋ฉด์ ํ์คํ์ ํ๋ ค๋ฉด ์ถ๊ฐ์ ์ธ ์ํ์ด ํ์ํ๋ค.

[์ด๊ณณ](https://github.com/apple/swift/blob/main/docs/HowToGuides/GettingStarted.md)์์ Using Ninja with Xcode ์น์์ **'Create an empty Xcode project in the workspace, using the External Build System template.'**
 ์ด ํํธ๋ถํฐ ๋ฐ๋ผํ๋ฉด ๋๋ค.

<br/>

๋๋ ์ผ๋จ ์์ค์ฝ๋๋ฅผ ๋๋ฌ๋ณด๋ ๊ฒ์ด ๋ชฉํ์๊ธฐ์ ์ด ์ ๋๋ก๋ง ์ํ์ ํ๋ค!

```toc

```
