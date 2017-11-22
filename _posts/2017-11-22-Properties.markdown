---
layout: post
title:  "Properties"
date:   2017-11-22 15:41:20
author: Jakouk
categories: Swift
---

## Properties

#### 프로퍼티
* 프로퍼티는 크게 저장 프로퍼티, 연산 프로퍼티, 타입 프로퍼티로 나눌수 있다. 

##### 저장 프로퍼티 
- 저장 프로퍼티는 인스턴스의 변수 또는 상수를 의미한다. 
- 클래스, 구조체에서 사용할수 있다. 
- var, let 등의 키워드를 사용해서 변수저장 프로퍼티, 상수저장 프로퍼티가 될수도 있다.
- 구조체 같은 경우는 프로퍼티가 옵셔널이 아니어도 자동적으로 이니셜라이저를 생성하지만 클래스는 옵셔널이 아닌경우 반드시 초기화 해주어야 한다. 
- 초기값을 설정해 두면 이니셜라이저를 구현해줄 필요가 없다. 

```swift
sturct Coordinate {
  var x: Int // 저장 프로퍼티
  var y: Int // 저장 프로퍼티
}
// 기본적으로 이니셜라이저가 있다.
let position: CoordinatePoint = Coordinate(x: 1, y: 2)

class Position {
  var point: CoordinatePoint // 저장 프로퍼티 ( 변수 )
  let name: String // 저장 프로퍼티 ( 상수 )
    
  init(name: String, currentPoint: CoordinatePoint) {
    self.name = name
    self.point = currentPoint
  }
}

```

***
##### 지연 저장 프로퍼티 ( Lazy Stored Properties )
- 지연 저장 프로퍼티는 호출이 있어야 값을 초기화 하며 lazy 키워드를 사용한다.
- 지연 저장 프로퍼티는 var 키워드를 사용하여 변수로 정의한다 
- 다중 쓰레드 환경에서 지연저장 프로퍼티에 동시다발적으로 접근할 때에는 한번만 이니셜라이즈 된다는 보장이 없다. 

###### 사용 할 때
- 클래스 인스턴스의 저장 프로퍼티로 다른 클래스의 인스턴스나 구조체 인스턴스가 사용될때 인스턴스를 초기화 하면서 저장 프로퍼티로 쓰이는 인스턴스들이 한 번에 생성되어야 하거나 굳이 모든 저장 프로퍼티를 사용할 필요가 없을때 쓰면 성능저하나 공간 낭비를 줄일 수 있다. 

```swift
struct CoordinatePoint {
  var x: Int = 0
  var y: Int = 0
}

class Position {
  lazy var point: CoordinatePoint = Coordinate()
  let name: String
    
  init(name: String) {
    self.name = name
  }
}

let personPosition: Position = Position(name: "person")
print(personPosition.point)	// point에 접근할때 CoordinatePoint가 생성된다. 
```
***

##### 연산 프로퍼티 
- 연산 프로퍼티는 값을 저장하는 것이 아니라 특정 연산을 수행한 결과값을 의미한다.
- 클래스, 구조체, 열거형에 쓰일수 있다. 

```swift
struct CoordinatePoint {
  var x: Int // 저장 프로퍼티
  var y: Int // 저장 프로퍼티
    
  var oppositePoint: CoordingatePoint { // 연산 프로퍼티
    // 접근자
    get {
      return CoordinatePoint(x: -x, y: -y)
    }
        
    // 설정자
    set {
      x = -newValue.x
      y = -newValue.y
    }
  }
}
var personPosition: CoordinatePoint = Coordinate(x: 10, y:20)
print(personPosition.oppositePoint)	// -10, -20
person.Position.oppositePoint = CoordinatePoint(x:15, y:10)

// set을 쓰지 않을경우 readonly 프로퍼티가 될수 있다. 
```

***
##### 타입 프로퍼티 
- 각각의 인스턴스가 아닌. 타입 자체에 속하게 되는 프로퍼티를 타입 프로퍼티라고 한다.
- 타입 프로퍼티는 타입 자체에 영향을 미치는 프로퍼티로 인스턴스의 생성 여부와 상관없이 타입 프로퍼티의 값은 하나이다. 

```swift
class AClass {
  static var typeProperty: Int = 0
    
  var instanceProperty: Int = 0 {
    didSet {
      AClass.typeProperty = instanceProperty + 100
    }
  }
    
  static var typeComputedProperty: Int {
    get {
      return typeProperty
    }
    set {
      typeProperty = newValue
    }
  }
}

AClass.typeProperty = 123

let classInstance: AClass = AClass()
classInstance.instanceProperty = 100
print(AClass.typeProperty) // 200
print(AClass.typeComputedProperty) // 100
```
- 클래스 메서드와 비슷한 면이 있는게 타입 프로퍼티 같다. 
***

##### 전역변수, 지역변수
- 전역변수, 지역변수가 존재한다. 
- 전역변수는 저장변수, 연산변수로 구현할 수도 있으며, 프로퍼티 감시자를 구현할수도 있다.
- 전역변수또한 지연 저장 프로퍼티처럼 처음 접근할 때 최초로 연산이 이루어진다. 

#### 프로퍼티 감시자 
- 프로퍼티의 값이 변할 때 값의 변화에 따른 특정 액션을 수행한다. 
- 프로퍼티 감시자는 지연 저장 프로퍼티에는 사용할 수 없으며 오로지 일반 저장 프로퍼티에만 적용할 수 있다.
- 프로퍼티 재정의를 통해 상속된 저장 프로퍼티 또는 연산 프로퍼티에도 적용이 가능하다.
- 저장 프로퍼티에 적용할 수 있으며 부모클래스로부터 상속 받을수 있다. ( 재정의도 가능하지만 부모 클래스의 프로퍼티 감시자도 같이 호출된다.  ) 
- didSet, willSet 키워드로 바뀌는 순간들을 감지할수 있다.
```swift
class Account {
  var credit: Int = 0
  var dollarValue: Double {  // 연산 프로퍼티
    get {
      return Double(credit) // 1000.0
    }
    set {
      credit = Int(newValue * 1000)
      print("잔액을 \(newValue)달러로 변경 중입니다.")
    }
  }
}

class ForeignAccount: Account {
  override var dollarValue: Double {
    willSet {
      print("잔액이 \(dollarValue)달러에서 \(newValue)달러로 변경될 예정입니다.")
    }
    didSet {
      print("잔액이 \(oldValue)달러에서 \(dollarValue)달러로 변경되었습니다.")
    }
  }
}

class ForeignCoinAccount: ForeignAccount {
  override var dollarValue: Double {
    willSet {
      print("코인으로 바뀔 예정")
    }
    didSet {
      print("코인으로 바뀜")
    }
  }
}

let account: ForeignCoinAccount = ForeignCoinAccount()
account.dollarValue = 2

// 코인으로 바뀔 예정 ( 1번 ForeignCoinAccount ) 
// 잔액이 0.0달러에서 2.0달러로 변경될 예정입니다. ( 2번 ForeignAccount )
// 잔액을 2.0달러로 변경 중입니다. ( 3번 Account )
// 잔액이 0.0달러에서 2000.0달러로 변경되었습니다. ( 4번 ForeignAccount )
// 코인으로 바뀜 ( 5번 ForeignCoinAccount )

```
