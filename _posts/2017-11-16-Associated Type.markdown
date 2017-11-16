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

이런 프로토콜이 있을떄

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
결국 associatedtype은 Container라는 프로토콜을 따르는 클래스가 제네릭을 통해서 원하는 타입으로
함수의 매개변수들을 설정할수 있도록 하기위한것이라고 생각하면 쉽게 이해할수 있을것 같다. 
