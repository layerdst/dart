
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

- **다만 var 타입이 변수타입이 확정이 되지 않았을때** 에는 변경이 가능하다.

```java
var speed; 
speed = 20;
speed = '속도';
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
  
## final, const
- 변수 앞에 final 과 const 가 선언이 되면,  최초로 선언된 값이 최종값이 되어버린다. 즉 한번 선언이 되면 수정할 수 없다.
- final 은 런타임 단계에서 값이 지정이되고, const는 컴파일 단계에서 값이 지정이 된다.
  
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
  
```java
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
  
## 생성자
- 자바와 생성자를 만들수 있으나, 다양한 형태로 코드를 작성할 수 있다.
  
```java
class Bicycle{
	int cadence;
	int speed;
	int gear;
}

Bicycle(this.cadence, this.speed, this.gear)
```
  
- 생성자 기본형
  
```java
Bicycle(int cadence, int speed, int gear)
	: this.cadence = cadence,
	this.speed = speed,
	this.gear = gear;
```
  
- 생성자 축약형
  
```java
Bicycle(this.cadence, this.speed, this.gear);
```
  
## 생성자 오버로딩
	- named parameter, named constructor 를 활용한 유연한 인스턴스를 생성자를 통해 만들 수 있다. 이는 자바의 생성자 오버로딩과 비슷하다.
	- Bicycle 생성자 중 cadence 는 필수 요소, speed와 gear 는 선택적으로 오버라이딩 할 수 있는 생성자는 아래와 같다.
	- 생성자를 통한 인스턴스 생성시 클래스에 맞는 name parameter 를 이용하여 쉽게 생성이 가능하다.
	
	```Java
	Bicycle(this.cadence, {this.speed=0, this.gear=0});
	// cadence 필수 요소, speed, gear 는 선택요소
	Bicycle(1,speed:3);
	Bicycle(1,gear:4)
	```
	
	- 세 요소 전부 선택적으로 적용할 수 있는 생성자이다. 이때는 default 값을 모두 적용해줘야 한다.
	
	```java
	Bicycle({this.cadence=0, this.speed=0, this.gear=0})
	// 3가지 전부 선택요소
	Bicycle(cadence:1,speed:3);
	Bicycle(speed:1,gear:3);
	Bicycle(cadence:1,speed:3,gear:3);
	```
	
	- required 를 선언하여 named parameter option 을 필수로 작성해야 하는 생성자를 만들수 있다.
	
	```java
	Bicycle({this.cadence=0, required this.speed, this.gear=0})
	Bicycle(cadence:1,speed:3,gear:3); // speed 는 필수 요소
	```
	
	- named constructor 란 클래스에서 여러 생성자를 가질 수 있는데, 생성자에 이름을 붙여 사용하는 것을 말한다.
	```java
	Bicycle.go(this.cadence)
	: this.gear = 10,
		this.speed = 2;
		
	Bicycle.fromMap(Map input) 
	: this.cadence = input['cadence'],
		this.gear = input['gear'],
		this.speed = input['speed'];
	```
  	
### Getter 와 Setter
- Java 에서는 필드(속성)변수들은 접근제한자와 관계없이 Getter 와 Setter 메소드를 임의르 만들어 사용할 수 있다.
- Dart 에서는 private 로 선언된, 즉 변수 앞에 \_\ 가 붙여진 속성들에 한하여 Getter 와 Setter 메서드로의 접근을 허용한다.
   
```java
class Car{
	int _speed=0;
	
	int get speed => _speed;
	set speed(int speed) => _speed = speed;
}
```
  
- getter  와 Setter 의 사용은 다음과 같다
```java
Car car = Car();
print(car.speed); //10
car.speed=20;
print(car.speed); //20
```
  
## 메소드 오버라이딩
- Dart 에서는  상속이나 implement 했을때 메소드를 오버라이딩 하는 어노테이션은 @override 로 표기한다.
  
```java
@override
void speedUp(int i){
	....
}
```
  
## 상속 (super, this 키워드)
- Dart 는 자바와 유사한 상속형태를 가지고 있다. 부모 클래스로 부터 상속을 받고자 한다면 extends 를 사용하여 선언해주면 된다.
- 자식 클래스는 부모의 필드와 메소드를 물려받아 사용할 수 있다. 때문에 자식 객체에서 super 를 통해 부모의 클래스를 기반으로 생성된 객체는 자식 객체에서도 그대로 쓸수 있다. 
  
```java
class Bicycle {
	int cadence;
	int speed;
	int gear;
	Bicycle(this.cadence, {this.speed = 0, this.gear = 0});
}

class Samcheonlee extends Bicycle {
	String productName;
	int speed;

	Samcheonlee(this.productName, int cadence, int speed, int gear)
	: this.speed = speed,
	super(cadence, gear: gear);
	
	outputString() {
		print({this.productName, this.speed, super.speed});
	}
}
```
  
- 위 클래스에서 부모와 자식 클래스중 speed는 같은 필드이다. 이를 this 로 생성하여 저장할때에는 자식의 클래스 필드가 우선순위를 갖게된다. (부모 객체의 speed 객체는 여전히 유효하다. 이는 super 를 활용하여 불러올수 있다.
  
```java
	Samcheonlee s = Samcheonlee("외발", 2, 3, 4);
	s.outputString();
		
	// 외발 + 3 + 0
```
  
## 인터페이스
- Dart 에서는 **인터페이스 조차도 클래스**이다. 키워드가 별도로 존재하지 않기 때문에 빈 메소드나 필드를 가진 클래스를 생성하여, implements 를 해주면 된다.
- implements 받은 클래스는 인터페이스로 정의된 클래스의 모든 필드와 메소드를 재정의하기 때문에 강력한 구현체로 봐야한다.
- 다중 implements 도 가능하기 때문에 유연한 기능확장도 가능하다.
  
```java
class V{
	String? name;
	greet() => print('hello ${this.name}');
}

class SC implements V{
	String? name;
	greet() => print('hello ${this.name} SCV go sir');
}
```
  
## Enum 타입
  
```java
enum Driver{
	taxi,
	bus
}

void main{
	Driver driver = Driver.taxi;
	print(Driver.values.toList()); [Driver.taxi, Driver.bus]
}
```
  
## null 조건 연산자
- 사칙연산은 타언어와 매우 유사하다. 굉장히 특이한 null 연산자가 있는데, 변수가 null 값이면 지정한 값을 입력해주고, 그렇지 않으면 기본값이 들어가는 것이다.
  
```java
int number;
number ?? = 4;
print(number); // 4

int number1 =2;
number1 = 4;
print(number1); //2
```
  
## /= 연산자
- /= 연산자는 double 로 형변환이 일어나게 된다. 때문에 기존에 int 로 선언되어 있는 변수라면 에러가 발생한다.
  
```java
int number = 2;
number /= 2; // 컴파일 에러
```
  
## 형 판별 연산자(is)
- 해당 변수가 어떤 자료형인지 판단하기 위해서 is 연산자를 사용한다.
  
```java
int b = 3;
print(b is int); //t
print(b is String); //f
print(b is bool); // f
print(b is! String); //t 
```
  
## List  선언(크기가 고정되지 않는 리스트)
- Dart 의 리스트는 java의 DTO 데이터 타입이 정의되지 않더라도 선언이 가능하다. 
- 리스트의 크기가 선언되지 않는 리스트(add, removeAt 관련 메소드 사용가능)
   
```java
List<String> tempList1 = ['a', 'b','c'];
List temp3 = new List.from([
	'a', 'b', 'c'
]);

List temp = [];
List temp1 = new List();

List memberList = [
	{
	'id' : 0,
	'name' : 'a'
	},
	
	{
	'id' : 1,
	'name' : 'b'
	},

	{
	'id' : 1,
	'name' : 'c'
	},
]

tempList1.add('g');
tempList1.removeAt(1); // index 1인 값 제거
tempList1.addAll(['e','e'])

```
  
## List 선언(크기가 고정된 리스트)
- 리스트의 크기가 선언된 리스트 (add, remove 관련 메소드 사용불가), 저장된 데이터를 수정하기 위해서는 리스트 인덱스에 직접 선언하여 할당해주어야 한다.
  
```java
List<String> tempList = List.filled(3,null,growable:false); //null 로 채워진 크기 3의 리스트
tempList[0] = a;
tempList[1] = b;
```
  
## List  메소드
- Dart 메소드의 기능들은 다음과 같다
  
```java
print(tempList1.first); //a
print(tempList1.isEmpty); //false
print(tempList1.isNotEmpty); //true
print(tempList1.length); //3
print(tempList1.last); //c
print(tempList1.reversed); //(c,b,a)
```

### List 탐색
  
```
var item = memberList.firstWhere((item) =>item['id'] ==1 );
var index = memberList.indexWhere((item)=>item['id']==1);
print(index); //1

var index2 = [10, 20, 30].indexOf(20); //1
var getValue = [10, 20, 30].contain(20); // true 

memberList.remove(10);
memberList.removeAt(1);
memberList.removeWhere((e)=>e==50);
```
  
### List Loop
  
```java
memberList.forEach((item){
	print(item) //{id:0, name:a.....}
});

var newList = memberList.map((item){
	return item['name'];
});
print(newList); // (a, b, c)

var fold = memberList.fold(0, (t, e){
	return t+e['id']; // 0번째 부터 마지막까지 id 값을 더하기
});
print(fold);

var reduce = [1,2,3,4,5].reduce((t,i)=> t+i);
print(reduce);
```
   
## Map 선언
  
- 맵의 선언은 아래의 선언방법들이 있는데, price 맵처럼 형을 지정해주는 것이 좋다. 맵의 key 값은 항상 unique 해야한다.
```java
Map dic2 = {}
Map dic3 = new Map();

Map dic = {
	'a' : '에이',
	'b' : '비'
};

Map dic = new Map.from({
	'apple' : '사과',
	'banana' : '바나나'
});

Map<String, int> price={
	'a' : 10,
	'b' : 20,
	'c' : 30
}

```
  
## Map 메소드
  
```java
dic2.addAll({
	'c': '씨',
	'd': '디'
});

print(dic['a']); //에이
dic['a'] = '씨';
print(dic['a']); // 씨
print(dic.keys.toList()); // 키를 전부다 출력
print(dic.values.toList()); // value를 전부다 출력
```

