---
emoji: ๐ง
title: '[API] Screen time: Device activity ์ฌ์ฉํด๋ณด๊ธฐ'
date: '2023-02-14 00:00:00'
author: ๊ณ ๋ฐ
tags: API
categories: API
---

## ScreenTime API

WWDC21 ์์ ScreenTime API ๊ฐ ์ฒ์์ผ๋ก ๋ฑ์ฅํ๋ค.

[Meet the Screen Time API](https://developer.apple.com/videos/play/wwdc2021/10123/)

ScreenTime API ๋ ์์ฝํ์๋ฉด ์ฌ์ฉ์์ Device (์์ด๋ค) ๋ด๋ถ์ ์ฑ ์คํ์ ์ ์ดํ๋๋ฐ ์ฌ์ฉํ  ์ ์๋ API ์ด๋ค.

<br/>

๊ทธ ํ WWDC22 ์์ ์กฐ๊ธ ๊ธฐ๋ฅ์ด ์ถ๊ฐ๋๊ณ  ํ์ฅ๋์๋ค.

์๋ ์์ด๋ค์ Device๋ฅผ ์ ์ดํ๋ ๊ฒ์ ํ์ ๋ Family Controls๊ฐ ๊ฐ์ธ์ Device๋ฅผ ์ ์ดํ  ์ ์๋๋ก ๊ธฐ๋ฅ์ด ํ์ฅ๋์๊ณ , Device Activity๋ก ์ฌ์ฉ์๊ฐ ์ฌ์ฉํ ์ฑ๋ค์ ์ ๋ณด๋ฅผ ๋ถ๋ฌ์ฌ ์ ์๊ฒ ๋์๋ค.

์ด๋ฒ ํฌ์คํ์์๋ Device Activity๋ฅผ ์ด์ฉํ์ฌ ์ฌ์ฉ์๊ฐ ์ฌ์ฉํ ์ฑ๋ค์ ์ ๋ณด๋ฅผ ๋ถ๋ฌ์ค๋ ๋ฐฉ๋ฒ์ ๋ํด์ ์๊ฐํ๊ฒ ๋ค.


<br/>

## ๊ธฐ๋ณธ ์ํ

Device Activity์ ์ฌ์ฉ๋๋ view๋ SwiftUI๋ก ๊ตฌ์ฑ๋์ด์๋ค.

SwiftUI๋ก ํ๋ก์ ํธ๋ฅผ ๋ง๋ค์ด์ฃผ์.

<br/>

ํ๋ก์ ํธ๋ฅผ ๋ง๋  ํ family controls์ ๋ํ ๊ถํ์ ์ถ๊ฐํด์ผํ๋ค.

<br/>

![capablity.png](capablity.png)

Target์ Signing & Capablities๋ฅผ ์ถ๊ฐํ์.

<br/>

๊ทธ ๋ค์ ๊ถํ์ ์์ฒญํ๋ ์ฝ๋๋ฅผ ์ฑ ์คํ์์ ๋ฃ์ด์ฃผ์

```swift
import FamilyControls
import DeviceActivity

AuthorizationCenter.shared.requestAuthorization(for: .individual)
```

<br/>

์ด์  DeviceActivityReportExtension ์ ์ถ๊ฐํด์ค์ผํ๋ค.

ํด๋น ๊ธฐ๋ฅ์ ์๋๋ฐ์คํ ๋์ด ์ฌ์ฉ๋๊ธฐ ๋๋ฌธ์ ์์ฒด์ ์ธ target์ ์ฝ๋๋ฅผ ์ถ๊ฐํ์ฌ ์ฌ์ฉํ  ์ ์๊ณ  extension์ผ๋ก ๋ ๋ค๋ฅธ ํ๊ฒ์ผ๋ก ์ถ๊ฐํด์ค์ผํ๋ค.

<br/>

![DeviceActivityReportExtension.png](DeviceActivityReportExtension.png)

<br/>

xcode์ ์๋จ (File -> New -> Target) ์ผ๋ก target template์ ์ ํํ์ฌ ์ถ๊ฐํ  ์ ์๋ค.

DeviceActivityReportExtension์ ์ ํํ์ฌ ์ถ๊ฐํด์ฃผ์.

<br/>

๊ทธ๋ฌ๋ฉด DeviceActivityReport๋ฅผ ์ฌ์ฉํ  ์ ์๋ ๊ธฐ๋ณธ ํํ๋ฆฟ์ ์๋์ผ๋ก ์์ฑํด์ค๋ค.

ํด๋น ํํ๋ฆฟ์ ์ฃผ์์ผ๋ก ์ค๋ช์ด ์ ์จ์ ธ์์ผ๋ ์ฐธ๊ณ ํด์ ์ปค์คํํ๋ฉด ๋๋ค.

<br/>

๋ค์ ์๋ ํ๋ก์ ํธ๋ก ๋์๊ฐ์, DeviceActivityReport View๋ฅผ ๋์๋ณด์.

<br/>

```swift
import SwiftUI
import FamilyControls
import DeviceActivity

@main
struct ScreenTimePracticeApp: App {
    
    @State private var context: DeviceActivityReport.Context = .totalActivity
    @State private var filter = DeviceActivityFilter(
        segment: .daily(
            during: Calendar.current.dateInterval(
                of: .weekOfYear, for: .now
            )!
        ),
        users: .all,
        devices: .init([.iPhone, .iPad])
    )
    
    init() {
        Task{
            try await AuthorizationCenter.shared.requestAuthorization(for: .individual)
        }
    }
    
    var body: some Scene {
        WindowGroup {
            DeviceActivityReport(context, filter: filter)
        }
    }
}
```

<br/>

DeviceActivityReport์์๋ `context`์ `filter`๊ฐ ํ์ํ๋ค.

context๋ ์ฐ๋ฆฌ๊ฐ DeviceActivityReportExtension์ ์ถ๊ฐํ์ฌ ์ปค์คํํ๋ view๋ฅผ ์๋ณํ๊ธฐ์ํด ์ฌ์ฉ๋๋ค.

filter๋ DeviceActivityReportExtension์์ `makeConfiguration` ๋ฉ์๋ ์์ ๋ฐ์์ค๋ ๋ฐ์ดํฐ(DeviceActivityResults<DeviceActivityData>)๋ฅผ ํํฐ๋ง ํด์ฃผ๊ธฐ์ํด ์ฌ์ฉ๋๋ค.

<br/>


์ฌ๊ธฐ๊น์ง๊ฐ DeviceActivityReport๋ฅผ ์ฌ์ฉํ๊ธฐ ์ํ ๊ธฐ๋ณธ์ ์ธ ์ํ์ด๋ค.

<br/>


## ๋ฌธ์ ์ ๊ณผ ๋์๋ฐฉ์

<br/>

### ๋ฐ์ดํฐ ๋ฒ๊ทธ?

์ฌ์ฉ์๊ฐ ์ฌ์ฉํ ์ฑ ๋ฐ์ดํฐ๋ฅผ ๋ฐ์์ค๋ ๋ถ๋ถ์ `makeConfiguration` ๋ฉ์๋์ ์๋ค.

<br/>

```swift
 func makeConfiguration(representing data: DeviceActivityResults<DeviceActivityData>) async -> TotalActivityView.Configuration
```

<br/>

๊ทธ๋ฐ๋ฐ data๋ฅผ ๋ฐ์์ ๋ณด๋ฉด CategoryActivity์ localizedDisplayName์ด ํญ์ nil๋ก ํ์๋๋ ๋ฒ๊ทธ๊ฐ ์๋ค.

https://developer.apple.com/forums/thread/709692

์ฐพ์๋ณด๋ ๊ฐ์ ์ด์๋ฅผ ๊ฒช๋ ์ฌ๋์ด ์๋ค.

<br/>

๋๋ฌธ์ ์ฑ ์นดํ๊ณ ๋ฆฌ๋ฅผ ํน์ ํ๊ธฐ ์ํด์๋ [FamilyActivityPicker](https://developer.apple.com/documentation/familycontrols/familyactivitypicker)๋ฅผ ์ฌ์ฉํ์ฌ report๋ฅผ ๋ณด๊ธฐ ์  ์นดํ๊ณ ๋ฆฌ๋ฅผ ์ง์ ํด์, ํด๋น ์นดํ๊ณ ๋ฆฌ ๋ฐ์ดํฐ๋ง ๋ณด์ฌ์ฃผ๋ ๊ฒ์ ์ ์ถฉ์์ผ๋ก ์ฌ์ฉํด์ผํ  ๋ฏ ํ๋ค.

<br/>

์๋๋ฉด ์ ๋ชจ๋ฅด์ง๋ง shield extension ์์๋ ์นดํ๊ณ ๋ฆฌ ์ด๋ฆ๋ค์ ๋ฐ์์ฌ ์ ์๋ค๊ณ  ํ๋๋ฐ, ์ด๊ฑธ ์ฌ์ฉํ๋ ๊ฒ๋ ํ๋์ ๋ฐฉ๋ฒ์ผ ๊ฒ ๊ฐ๋ค.

<br/>

### ๋๋ฒ๊ทธ์ ์ด๋ ค์

target์ผ๋ก ์ถ๊ฐํ DeviceActivityReportExtension๋ ๊ทธ๋ฅ ์คํํด์๋ ๋๋ฒ๊นํ  ์ ์๋ค.

๋์ ์ xcode ์๋จ (Debug -> Attach to process -> ํด๋น DeviceActivityReportExtension) ์ผ๋ก ๋๋ฒ๊น ๋ชฉ๋ก์ ์ถ๊ฐํด์ฃผ๋ฉด lldb๋ก ๋๋ฒ๊นํ  ์ ์๋ค.

```toc

```
