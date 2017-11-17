---
layout: post
title:  "Protocol Composition ( & )"
date:   2017-11-16 17:12:20
author: Jakouk
categories: Swift
---

# Protocol Composition ( & )

#### Protocol Composition 이란
* 하나의 매개변수가 여러 프로토콜을 모두 준수하는 타입이어야 한다면 하나의 매개변수에 여러 프로토콜을 한 번에 조합하여 요구할 수 있다.

#### 프로토콜 조합
```swift
protocol Named {
  var name: String { get }
}

protocol Aged {
  var age: Int { get }
}

struct Persion: Named, Aged {
  var name: String
  var age: Int
}

struct Car: Named {
  var name: String
}

func celebrateBirthday(to celebrator: Named & Aged) {
  print("Happy birthday \(celebrator.name) !! Now you are \(celebrator.age)")
}

let yagom: Person = Person(name: "yagom", age: 99)
celebrateBirthday(to: yagom)  // Happy birthday yagom!!! Now you are 99

let myCar: Car = Car(name: "Boong Boong")
celebrateBirthday(to: myCar)   // 오류 발생!! Aged를 충족시키지 못합니다!

```

celebrateBirthday 함수의 celebrator라는 매개변수는 Named & Aged를 충족해야만 한다는 것이다.

#### 참조 
* 스위프트 프로그래밍 ( 야곰 지음 )
