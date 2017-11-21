---
layout: post
title:  "Inheritance 2"
date:   2017-11-21 15:56:20
author: Jakouk
categories: Swift
---

## Inheritance 2 ( Class of Swift )

#### Initializer
- 프로터피들의 초기화를 해주는 설정하는 일을 수행함. 

##### 기본 이니셜라이저
- 기본이니셜라이저는 프로퍼티 기본값으로 프로퍼티를 초기화해서 인스턴스를 생성한다. 
- 기본이니셜라이저를 지키고 싶으면 사용자정의 이니셜라이저를 extention으로 만들어 주면 된다.

##### 사용자 지정 이니셜라이저
- 사용자지정 이니셜라이저를 만들면 기본 이니셜라이저를 따로 만들지 않는이상 사용할수 없다.
- 초기화 과정에서 옵셔널로 설정된 프로퍼티는 꼭 초기화하지 않아도 된다. 
- 상수로 선언된 프로퍼티는 인스턴스를 초기화하는 과정에서만 값을 할당할수 있다 

##### 멤버 이니셜라이저
- 구조체에서만 쓸수 있는 이니셜라이저이다. 

##### 실패 가능한 이니셜라이저
- 초기화를 실패할 경우 nil을 반환하는 이니셜라이저
```swift
init?() {
  if ( 조건문 ) {
    return nil
  }
}
```
***
#### Class Initializer
- 클래스에서는 지정 이니셜라이저와 편의 이니셜라이저로 역활을 구분한다. 

##### Designated Initializer ( 지정 이니셜라이저 )
- 클래스의 주요 이니셜라이저로 모든 클래스는 하나이상의 지정 이니셜라이저를 가진다. 
- 지정 이니셜라이저는 부모클래스의 이니셜라이저를 호출해야 한다. ( 모든 프로퍼티가 부모와 같으면 굳이 할 필요가 없을수도 있다. )
- 클래스의 모든 프로퍼티를 초기화해야 하는 임무를 갖고 있다.
```swift
init( 매개변수 ) {
  // 코드    
}
```

##### Convenience Initializer ( 편의 이니셜라이저 )
- 편의 이니셜라이저는 클래스 설계자의 의도대로 외부에서 사용되길 원할때 인스턴스 생성코드를 작설할 때 수고를 덜 때 유용하게 사용할수 있다. 
```swift
convenience init( 매개변수 ) {
  // 코드
}
```

***
#### 클래스의 초기화 위임 
1. 자식클래스의 지정 이니셜라이저는 부모클래스의 지정 이니셜라이저를 반드시 호출해야 합니다.
3. 편의 이니셜라이저는 자신이 정의된 클래스의 다른 이니셜라이저를 반드시 호출해야 합니다.
4. 편의 이니셜라이저는 궁극적으로는 지정 이니셜라이저를 반드시 호출해야 합니다. 

##### 클래스 2단계 초기화 ( Safty- Checks )
1. 자식 클래스의 지정 이니셜라이저가 부모클래스의 이니셜라이저를 호출하기 전에 자신의 프로퍼티를 모두 초기화했는지 확인합니다.
2. 자식클래스의 지정 이니셜라이저는 상속받은 프로퍼티에 값을 할당하기 전에 반드시 부모클래스의 이니셜라이저를 호출해야합니다.
3. 편의 이니셜라이저는 자신의 클래스에 정의된 프로퍼티를 포함하여 그 어떤 프로퍼티라도 값을 할당하기 전에 다른 이니셜라이저를 호출해야 합니다.
4. 초기화 1단계를 마치기 전까지는 이니셜라이저는 인스턴스 메서드를 호출할 수 없습니다. 또 인스턴스 프로퍼티의 값을 읽어들일 수도 없습니다. self 프로퍼티를 자신의 인스턴스를 나타내는 값으로 활용할 수도 없습니다. 

##### 초기화 과정
1. 최상위 클래스까지 안전확인을 하면서 도달.
2. 최하위까지 커스터마이징 하면서 도달.
***

#### 이니셜라이저 상속
- 다른 메서드들과 똑같이 상속받을 이니셜라이저 앞에 override 키워드를 사용하여 상속 받는다. 
- 상속받은 이니셜라이저안에 super init이 있어야 하며 super init 보다 앞쪽에서 자식클래스에서 추가된 프로퍼티를 초기화해야한다. 

```swift
clsss Peron {
    var name: String
    var age: Int
    
    // 지정 
    init(name: String, age: Int) {
      self.name = name
      self.age = sge
    }
    
    // 편의
    conveniencce init(name: String) {
    	self.init(name:name, age: 0)
    }
    
    init?(age: Int) {
    	if age < 0 {
        return nil
      }
        
        self.name = "Unknown"
        self.age = age
    }
}

class Student: Person {
      var major: String
    
    // 상속된 지정 이니셜라이저  
    override init(name: String, age: Int) {
      self.major = "Swift"
      super.init(name: name, age: age)
    }
    
    // 편의 
    convenience init(name: String) {
    	self.init(name: name, age: 7)
    }
    
    // 상솓된 실패가능 이니셜라이즈 
    // 실패가능 이니셜라이즈를 받아서 실패하지 않는 이니셜라이즈로 재정의도 가능하다. 
    override init(age: Int) {
    	self.major = "Swift"
        super.init()
    }	
}
```
##### 이니셜라이즈 자동상속

- 자식클래스에서 별도의 지정 이니셜라이저를 구현하지 않는다면, 부모클래스의 지정 이니셜라이저가 자동으로 상속된다.
- 부모클래서의 지정이니셜라이저를 자동으로 상속받은 경우나 부모클래스의 지정 이니셜라이저를 모두 재정의하여 부모클래스와 동일한 지정 이니셜라이저를 모두 사용할수 있으면 부모의 편이 이니셜라이저가 모두 자동으로 상속된다. 

##### 요구 이니셜 라이즈 
- required 수식어를 클래스의 이니셜라이저 앞에 명시해주면 이 클래스를 상속받은 자식클래스에서 반드시 해당 이니셜라이저를 구현해 주어야 한다. 
- 일반 이니셜라이저를 상속받아 요구 이니셜라이저로 재정의 할수도 있다. 
- 요구 이니셜라이저를 일반 이니셜라이저로 바꿀수는 없다. 

```swift
class Person {
  var name: String
    
  init() {
    self.name = "Unknown"
  }	
}

class Student: Person {
    var major: String = "Unknown"
    
    init(major: String) {
    	self.major = majo
        super.init()
    }
    
    // init()을 상속받아 요구 이니셜라이저로 재정의 
    required override init() {
    	self.major = "Unknown"
        super.init()
    }
    
    // 요구 편의 이니셜라이저를 만듬 
    required convenience init(name: String) {
    	self.init()
        self.name = name
    }
}

class UniversityStudent: Student {
    var grade: String
    
    init(grade: String) {
    	self.grade = grade
        super.init()
    }
    
    // Student 클래스에서 요구하였으므로 구현해주어야 한다.
    required init() {
    	self.grade = "F"
        super.init()
    }
    
    // Student 클래스에서 요구하였으므로 구현해주어야 한다.
    required convenience init(name: String) {
    	self.init()
        self.name = name
    }
}	

```

***
#### 참조
- 스위프트 프로그래밍 ( 야곰 지음 )
