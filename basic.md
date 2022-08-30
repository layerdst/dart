# 변수와 타입


## 원시타입과 참조타입

* JAVA 에서 데이터 타입은 **원시타입과 참조타입**으로 나뉘는데, Dart 는 모두 **참조타입**이다.

* 다만, JAVA 에서는 참조타입에는 기본값인 null 을 선언할 수 있으나, Dart 도 null을 선언할수 있다. **다만  \” ? \” 와 같은 null 조건 연산자를 타입 뒤에 붙여 주어야 한다.**

```java
- JAVA
Integer x = null; //java

- Dart
int x = null // 컴파일 에러
int? y = null // nullable 
```

## 타입추론
- Dart 에서는 Java 10 상위 버전에서 등장하는 **var, dynamic, Object  키워드로** 타입 추론이 가능하다. 때문에 명시적으로 타입을 선언하지 않아도 된다.
- var 는 초기값이 있으면 변수 타입이 확정이  되고, 변경이 불가하다.
```java
var speed = 10; 
speed = 20;
speed = '속도'; // 컴파일 에러
```
- dynamic 초기값과 무관하게 타입을 변경할 수 있다. Object 와 달리 모든 메서드와 속성을 가지고 있다.
```java
dynamic speed = 10; 
speed = 20;
speed = '속도'; 
```
- Object 도 dynamic 과 마찬가지로 초기값과 무관하게 타입 변경을 할 수 있으나, Object 클래스에 있는 속성과 메서드만 사용이 가능하다.
```java
dynamic name = 1000;
name = "이름";
println(name.length); // 2


Object objSpeed = 20; 
objSpeed = '속도';
println(objSpeed.length) // 컴파일에러
```

## null safety

-  자바 8부터 Optional 이라는 Wrapper 클래스의 등장했다. null이 될 수 있는 객체를 감싸면서 NPE 를 회피할 수 있는 방법으로 떠오르고 있다.
```java
Optional<String> value = Optional.ofNullable(data);
String name = value.orElse("none");

//data 가 null 이면 비어있는 객체를 반환하는데, 기본값을 none 을 리턴하게 하였다.

```
- Dart 에서는 변수 선언시 참조타입 뒤에 \"?\" 를 선언해주면 null safety를 바로 적용할 수 있다.
```java

nullSafety(int? v){
	if(v==null){print("널이에요")}
}


main() {
	int? nullableInt = null; 
	nullSafety(nullableInt); //널이에요
}

```
- 이외에도 Dart 는 late, type promotion 등으로 체크가 가능하다. 해당 내용은 아래의 이 [블로그](https://medium.com/flutter-korea/flutter%EC%9D%98-null-safety-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-dd4ee1f7d6a5)를 참조한다.  


## 템플릿 리터럴(javascript)
- Dart 는 자바스크립트에서의 템플릿 리터럴과 유사한 기능을 하는 문법이 있다.
```javascript
-javascript
var a = "십";
var b = "오";
console.log(`Fifteen is ${a+b}`);


- Dart
var a = "십";
var b = "오";

print(a + b +'is Fifteen'); //십오 is Fifteen
print('$a$b is Fifteen'); //십오 is Fifteen
print('${a+b} is Fifteen'); //십오 is Fifteen
```

## 접근제한자
- Dart 의 접근 제한자는 public, private  만 존재한다. 
- public 은 어플리케이션 내에서 모든 접근이 가능하며, 선언은 **아무것도 하지 않는것이다**.
- private 는 Java 와 달리 같은 패키지, 같은 클래스 내에서만 접근이 가능하며, 선언 방법은 변수명 앞에 \" _ \" 를 붙여준다
```java
var _name = "이름"; //private 접근제한
```

### 메소드 
- 일반적인 언어들과 유사하나, 자바스크립트의 함수인 1급 객체의 쓰임과 유사하다
