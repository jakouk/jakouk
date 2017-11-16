---
layout: post
title:  "Associated Type ( 프로토콜 연관 타입 )"
date:   2017-11-16 17:12:20
author: Jakouk
categories: Swift
---

# Associated Type ( 프로토콜 연관 타입 )

#### Associated Type 이란
* 프로토콜에서 사용될 수 있는 플레이스홀더 이름이다.
* 제네릭에서 어떤 타입이 타입이 들어올지 모를 때, 타입 매개변수를 통해 ' 종류는 알 수 없지만, 어떤 타입이 여기에 쓰일 것이다' 라고 표현해주었다면 연관 타입은 타입 매개변수의 그 역활을 프토토콜이 수행할 수 있도록 만들어진 기능이다.

#### Conatiner 프로토콜 정의
```swift
protocol Container {
associatedtype ItemType
var count: Int { get }
mutating func append(_ item: ItemType )
subscript(i: Int) -> ItemType { get }
}
```

이런 프로토콜이 있을때

```swift
class MyContainer: Container {
var items: Array<Int> = Array<Int>()

var count: Int {
  return items.count
}

func append(_ item: Int) {
  items.append(item)
}

subscript(i: Int) -> Int {
  return items[i]
}
```
Container 프로토콜을 따르는 MyContainer라는 클래스는 모든 요구사항을 충족한다.
간단하게 말해서 프로토콜에서 사용하는 제네릭타입이라고 이해하면 쉬울것 같다.
