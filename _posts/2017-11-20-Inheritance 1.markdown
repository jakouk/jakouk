---
layout: post
title:  "Inheritance 1"
date:   2017-11-20 16:39:20
author: Jakouk
categories: Swift
---

## Inheritance 1 ( Class of Swift )

#### 상속이란 
* 다른 클래스에 정의되어있는 특성들을 받아서 쓸수 있는 것을 말한다. 

#### 클래스와 상속 
* 메서드나 프로퍼티등은 다른 클래스로 부터 상속을 받을수 있다. 
	- 다른클래스로부터 상속받은 클래스는 **자식클래스**
	- 자식클래스에게 자신의 특성을 물려준 클래스는 **부모클래스** 라고 표현한다. 
	- 다른 클래스로부터 상속을 받지 않은 클래스를 **기반클래스**라고 부른다. 

#### 기반클래스
* 클래스를 생성할 경우에는 **이니셜라이저**를 꼭 만들어야 한다. 
* 프로터피를 **정의와 동시**에 **초기화**를 하는 경우에는 이니셜라이저를 만들지 않아도 된다. 

기반 클래스 Person 
```swift
class Person {
   var name: String = ""
   var age: Int = 0
        
   var introduction: String {
      return "이름: \(name). 나이 : \(age)"
   }
        
   func speak() {
      print("가나다라마바사")
   }
}
    
let yagom: Person = Person()
yagom.name = "yagom"
yagom.age = 99
print(yagom.introduction)	// 이름 : yagom. 나이 : 99
yagom.speak() 				// 가나다라마바사
```

#### 클래스 상속의 기본 문법
* 클래스 이름 옆에 콜론을 쓰고 상속받을 클래스의 이름을 쓰면 된다. 
```swift
class name: Super class {
   // code
}
```
* 인스턴스 메서드, 타입 메서드, 인스턴스 프로퍼티, 타입 프로퍼티, 서브스크립트등 모든 특성을 상속받아 사용할수 있다. 

Person 클래스를 상속받은 Student 클래스
```swift
class Student: Person {
   var grade: String = "F"
        
   func study() {
      print("Study hard..."
   }
}
    
let yagom: Person = Person()
yagom.name = "yagom"
yagom.age = 99
print(yagom.introduction)	// 이름 : yagom. 나이 : 99
yagom.speak()	// 가나다라마바사
    
let jay: Strudent = Student()
jay.name = "jay"
jay.age = 10
jay.grade = "A"
print(jay.introduction)		// 이름 : jay. 나이 : 10
jay.speak()	 // 가나다라마바사
jay.study()	 // Study hard...
```

#### 재정의 ( Override )
* 부모클래스의 특성을 그대로 사용하는게 아니라 새롭게 정의해서 사용할수 있다. 
* 새로운 정의 앞에 override라는 키워드를 사용해서 새롭게 정의하면 된다. 
* 부모클래스의 특성을 그래서 사용할때는 super 키워드를 사용하면 된다. 

 메서드 재정의 
```swift 

class Person {
    var name: String = ""
    var age: Int = 0
        
     func speak() {
       print("가나다라마바사")
     }
}
     
class Student: Person {
   override func speak() {
       print("저는 학생입니다.")
   }
}
     
class UniversityStudent: Student {
   override func speak() {
      super.speak()
      print("대학생이죠")
    }
}
     
let yagom: Person = Person()
yagom.speak() // 가나다라마바사
     
let jay: Student = Student() 
jay.speak() // 저는 학생입니다.
     
let jenny: UniversityStudent = UniversityStudent()
jenny.speak() // 저는 학생입니다. 대학생이죠. 
 ````
 
 프로퍼티 재정의 
 * 읽기 전용 프로퍼티를 상속 받아서 읽기,쓰기가 가능한 프로퍼티로 재정의 할수도 있다. 
```swift
class Person {
   var name: String = ""
   var age: Int = 0
   var koreanAge: Int {
      return self.age + 1
   }
   var introduction: String {
      return "이름 : \(name). 나이 : \(age)"
   }
}
    
class Student: Person {
  var grade: String = "F"
        
   override var introduction: String {
      return super.introduction + " " + "학점 : \(self.grade)"
   }
        
   override var koreanAge: Int {
      get {
         return super.koreanAge
      }
      set {
          self.age = newValue - 1
      }
   }
}
    
let yagom: Person = Person()
yagom.name = "yagom"
yagom.age = 55 // 오류발생 ( 읽기 전용 프로퍼티 )
yagom.koreanAge = 56
print(yagom.introduction)	// 이름 : yagom. 나이 : 55
print(yagom.koreanAge) // 56
    
let jay: Student = Student()
jay.name = "jay"
jay.age = 14
jay.koreanAge = 15
print(jay.introduction) // 이름 : jay. 나이 : 14 학점 : F
print(jay.koreanAge) // 15
```

프로퍼티 감시자 재정의 
* 읽기전용 프로퍼티는 프로퍼티 감시자를 재정의 할수 없다. 
* 프로퍼티 감시자를 재정의 하더라도 조상클래스에 정의된 프로퍼티 감시자도 동작한다. 
* 프로퍼티의 접근자와 프로퍼티 감시자는 동시에 재정의 할수 없다. 
* 둘다 동작되길 원한다면 재정의하는 접근자에 프로퍼티 감시자의 역할을 구현해야 한다. 

```swift 
class Person {
   var name: String = ""
   var age: Int = 0 {
   didSet {
        print("Person age: \(self.age)")
      }
   }
   var koreaAge: Int {
      return self.age + 1
   }
        
   var fullName: String {
      get {
          return self.name
        }
      set {
           self.name = newValue
        }
    }
}
    
class Student: Person {
  var grade: String = "F"
        
  override var age: Int {
      didSet {
         print("Student age: \(self.age)")
      }
   }
        
   override var koreanAge: Int {
       get {
           return super.koreanAge
       }
       set {
           self.age = newValue - 1
       }
       didSet { } // 오류 ( 감시자나 접근자 둘중 하나만 재정의 가능 )
    }
    override var fullName: Sting {
       didSet {
           print("Full Name: \(self.fullName)")
        }
    }
}
    
class UniversityStudent: Student {
   override var koreanAge: Int {
      didSet {
           print("koreanAge");
      }	
   }
}
    
    
let yagom: Person = Person()
yagom.name = "yagom"
yagom.age = 55 // Person age : 55
yagom.fullName = "Jo yagom"
print(yagom.koreanAge) // 56
    
let jay: Student = Student()
jay.name = "jay"
jay.age = 14 // Person age : 14 Student age : 14
jay.koreanAge = 15 // Person age : 14 Student age : 14
jay.fullName = "Kim jay" // Full Name : Kim jay
    
``` 
결과 
* 읽기 전용 프로퍼티를 상속 받아서 읽기 쓰기가 가능한 프로퍼티로 재정의 할수 있다. 
* 읽기 쓰기가 가능한 프로퍼티로 재정의한 프로퍼티는 프로퍼티 감시자를 사용할수 있다. 
* 재정의 할때는 프로퍼티 감시자나 프로퍼티 설정자 둘중 한가지만 재정의 할수 있다. 
* 감시자를 재정의 할 경우 상위에 있는 감시자도 같이 실행된다. 

서브스크립트 재정의
* 서브스크립트는 부모클래스 서브스크립트의 매개변수와 반환 타입이 같아야 한다.

재정의 방지
* 자식클래스에서 몇몇 특성을 재정의할수 없도록 제한하고 싶을경우 특성앞에 final 키워드를 명시하면 된다.
* ex) final var, final func, final class func ...

```swift 
class Person {
   final var name: String = ""
        
   final func speak() {
      print("가나다라마바사")
   }
}
    
final class Student: Person {
   // 오류 
   // final을 사용하여 프로퍼티 상속을 막음 
   override var name: String { 
			
   }
}
    
    // 오류 Student class 앞에 final을 사용하여 클래스 상속을 막음 
class UniversityStudent: Student {
    
}
