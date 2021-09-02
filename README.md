# 📌 MyKotlinStudy
> 부족하다고 느꼈던 코틀린 문법 기초부터 공부하기    

### 📌 Kotlin 

#### 표기법
- 클래스 이름
 - 파스칼 표기법: 모든 단어를 대문자로 시작 
- 함수나 변수 이름
 - 첫 단어만 소문자로 시작
 
#### 변수 선언
- var: 일반적으로 통용되는 변수, 언제든지 읽기 쓰기가 가능함
- val: 선언시에만 초기화 가능 중간에 값을 변경할 수 없음. 변경하지 말아야할 값
- 클래스에 선언된 변수: Property(속성)
- 이 외의 Scope 내에 선언된 변수: Local Variable(로컬 변수)
- 코틀린은 기본 변수에서 null을 허용하지 않음 >> null pointer excaption 원천적으로 차단해줌
- 변수가 선언되지 않은 걸 사용하고 싶을 경우 
  - **var a:Int? = null** 자료형 뒤에 ?를 붙여 null을 허용하는 nullable 변수로 선언해 줄 수 있다.
  - nullable 변수는 값이 null인 상태로 연산을 사용할 시 null pointer excaption이 발생하므로 주의해서 사용
 
#### 형변환과 배열
 - 코틀린은 암시적 형변환을 지원하지 않음

#### 타입추론과 함수
- fun aa(a: Int): Int >> Int로 반환하도록 한다.
- 단일 표현식 함수: 반환형의 타입추론이 가능하므로 반환형을 생략할 수 있다.
```
 fun add(a: Int, b: Int, c: Int): Int {
    return a+b+c
 }
 
 ---------------->
 
  fun add(a: Int, b: Int, c: Int) = a + b + c
  
  ```
  
  #### 조건문과 비교연산자
  ```
    fun doWhen (a: Any){ //Any: 어떤 자료형이든 상관없이 호환되는 코틀린 최상위 자료형
      when(a) {
        1 -> "어쩌고"
        "Hi" -> "음"
        is Long -> "Long"
        !is Long -> "!Long"
      }
    }
  ```
  - 등호나 부등호의 사용은 불가능
  - when에서 결과를 변수에 받아 출력하기
  ```
    fun doWhen (a: Any){ //Any: 어떤 자료형이든 상관없이 호환되는 코틀린 최상위 자료형
      var result = when(a) {
        1 -> "어쩌고"
        "Hi" -> "음"
        is Long -> "Long"
        !is Long -> "!Long"
      }
    }
  ``` 


  #### 흐름제어와 논리 연산자
 - 내부 반복문에서 조건을 체크하여 break를 하더라도 외부 반복문에서 또 다시 조건을 체크하여 모든 반복문을 수동으로 종료해야 한다.
   - 코틀린에서는 외부 반복문에 레이블 이름과 @기호를 달면 레이블이 달린 반복문을 기준으로 즉시 break 시켜준다.
```
    for( i in 1..10 ) {
      for( j in 1..10 ) {
        // 내부 반복문
        if ( i == 1 && j == 2 ) break
      }
      // 외부 반복문
    }
 
 ---------------->
     loop@for( i in 1..10 ) {
      for( j in 1..10 ) {
        // 내부 반복문
        if ( i == 1 && j == 2 ) break@loop
      }
      // 외부 반복문
    }
  ``` 
  
  #### 클래스의 기본 구조
  
  ```
    fun main() {
     var a = Person("이름1", 1990)
     var b = Person("이름2", 1997)
     var c = Person("이름3", 2004)
     
     a.introduce()
     b.introduce()
     c.introduce()
     }
     
     class Person(var name:String, val birthYear:Int){
       fun introduce() {
         println("안녕하세요, ${birthYear}년생 ${name}입니다.")
         }
     }
  ``` 
  - 코틀린은 객체지향 언어를 기반으로 함수형 언어의 장점을 흡수한 실용적인 언어이다.
  
  
 #### 클래스의 생성자
 - 인스턴스 생성시 구문을 수행하는 기능을 넣을 수 없었다 >> init 함수를 통해 구현이 가능
 - init함수는 패러미터나 반환형이 없는 특수한 함수. 생성자를 통해 인스턴스가 만들어질 때 호출되는 함수
   ```
    fun main() {
     var a = Person("이름1", 1990)
     var b = Person("이름2", 1997)
     var c = Person("이름3", 2004)
     }
     
     class Person(var name:String, val birthYear:Int){
       init {
         println("안녕하세요, ${this.birthYear}년생 ${this.name}입니다.")
         }
     }
    ```   
  
- 클래스를 만들 때 기본으로 선언(기본 생성자) + 필요에 따라 추가적으로 선언(보조 생성자)
- 보조 생성자는 기본 생성자와 다른 형태의 생성자를 제공하여 인스턴스 생성 시 편의를 제공하거나 추가적인 구문을 수행하는 기능을 제공하는 역할
- 보조 생성자를 만들 때는 반드시 기본 생성자를 통해 속성을 초기화 해주어야 한다.

   ```
    fun main() {
     var a = Person("이름1", 1990)
     var b = Person("이름2", 1997)
     var c = Person("이름3", 2004)
     var d = Person("이름4")  // 1997로 출력 (보조 생성자)
     var e = Person("이름4")  // 1997로 출력 (보조 생성자)
     var f = Person("이름4")  // 1997로 출력 (보조 생성자)
     }
     
     class Person(var name:String, val birthYear:Int){
       init {
         println("안녕하세요, ${this.birthYear}년생 ${this.name}입니다.")
         }
       constructor(name:String) : this(name, 1997){
         println("보조 생성자가 사용")
       }
     }
  ```      
#### 클래스의 상속
  - 코틀린은 상속 거부가 기본 옵션


#### 오버라이딩과 추상화
   ```
    fun main() {
     var t = Tiger()  //인스턴스 만들기
     t.eat //실행하기
     }
     
     open class Animal { //상속이 가능하게 open
       fun eat() {
         println("음식을 먹습니다.")
       }
     }
     
     class Tiger : Animal() //위의 클래스를 상속받음
     //여기서 println("고기를 먹습니다.")를 실행하고 싶어도 위에서 음식을 먹습니다를 했기 때문에 실행 x
     // 서브 클래스에서는 함수를 재구현할 수 없다. 하지만
  ```   
  - 수퍼클래스에서 open이 붙은 함수는 서브클래스에서 오버라이드를 붙여 재구현하면 된다.
    
     ```
    fun main() {
     var t = Tiger() 
     t.eat 
     }
     
     open class Animal { 
       open fun eat() { //여기에 open이 붙는다면 재구현이 허용된다.
         println("음식을 먹습니다.")
       }
     }
     
     class Tiger : Animal() {
       overrride fun eat(){ //override
         println("고기를 먹습니다.")
       }
     }

  ```   
  
  - 추상화: 선언부만 있고 기능이 구현되지 않음
  - 인터페이스 >> 코틀린에서는 속성, 추상함수, 일반함수를 가질 수 있다.
    - 다만 추상함수는 생성자를 가질 수 있지만 인터페이스는 가질 수 없다.
    - 인터페이스에서 구현부가 있는 함수는 open 함수로 간주한다.
    - 구현부가 없는 함수는 abstract 함수로 간주한다. 
    - 별도의 키워드가 없어도 서브클래스에서 구현 및 재정의가 가능하다. 
  

  
