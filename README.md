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
  
  
 #### 기본 프로젝트 구조
  - 하나의 프로젝트는 여러 개의 모듈로 이루어진다.
  - 패키지 명: 도메인을 뒤집고 기능별로 정리
 
 
 #### 변수, 함수, 클래스의 접근범위와 접근제한자
 - 스코프 외부에서는 스코프 내부의 맴버를 참조연산자로만 참조가 가능하다
 - 클래스의 맴버를 참조할 때 클래스 외부에서 인스턴스 명에 참조연산자를 사용하여 접근했었었다(.<<이거)
 - 동일 스코프 내에서는 맴버를 공유할 수 있다.
 - 접근 제한자는 스코프 외부에서 스코브 내부에 접근할 때 개발자가 제안할 수 있다.
 - internal : 같은 모듈 내에서만 //클래스 스코프에서는 사용 x
 - 접근 제한자는 개발자는 의도에 따라 외부와 내부에서 사용할 맴버를 분리하여 스코프 외부에서 건들이지 말아야할 기능이나 값들을 안전하게 제한

  #### 고차함수와 람다함수
  - 함수를 마치 클래스에서 만들어낸 인스턴스처럼 취급 한다. 함수를 패러미터로 취급할 수 있고 결과값으로 반환 받을 수 있다.
  - 코틀린에서는 모든 함수를 고차함수로 받아낼 수 있다.
 ```
    fun main() {
      b(::a) //함수 b를 호출하되 함수 a를 패러미터로 넘겨준다. ::>> 일반함수를 고차함수로 변경해주는 연산자
      
      val c: (String) -> Unit = { str -> println("$str 람다함수")} //람다함수
      
    }

    fun a(str: String) { //자료형의 a는 함수의 형식을 넘겨받을 수 있도록 해야하는데
      println("$str 함수 a") 
     }

    fun b(function: (String) -> Unit) {  //자료형의 일종
      function("b가 호출한")
    }
    
    [결과] b가 호출한 함수 a
           b가 호출한 람다함수
 ```   
 
 - 함수의 형식 자료형으로 나타내기
   - (자료형, 자료형, ..) -> 자료형(반환형)
 - 람다함수는 일반함수와 다르게 그 자체가 고차함수 별도의 연산자 없이도 변수에 담을 수 있다.
 
 
 #### 스코프 함수
 - 람다 함수도 일반 함수처럼 여러 구문을 수행할 수 있다.
   - 이 경우 마지막 구문인 결과 값이 반환된다.
 - 람다함수에 패러미터가 없다면 실행할 구문들만 나열하면 된다.
 - 패러미터가 하나 뿐이라면 it을 사용 // val c: (String) -> Unit = { println("$it 람다함수:) }
 - 스코프 함수는 함수형 언어의 특징을 좀더 편리하게 사용할 수 있도록 기본 제공하는 함수
 - 클래스에서 생성한 인스턴스를 스코프 함수에 전달하면 인스턴스의 속성이나 함수를 좀 더 깔끔하게 불러 쓸 수 있다.
   - 코드의 가독성 향상
 - 스코프 함수에는 apply, run, with, also, let 등 이 있다
 - apply는 인스턴스를 생성한 후 변수에 담기 전에 초기화 과정을 수행할 때 많이 사용한다.
 -  ==> 메인함수와 별도로 인스턴스의 변수와 함수를 조작하므로 코드가 깔끔해진다. 
 ```
    fun main() {
      var a = Book("디모의 코틀린", 10000).apply{
           
      //apply를 이용하면 인스턴스를 생성하자마자 그 인스턴스에 참조연산자를 사용하여 apply를 붙이고
      // 중괄호로 람다 함수를 하나 만들어 apply의 스코프 안에서 직접 인스턴스의 속성과 함수를 참조연산자 없이 사용이 가능하다.
      //또한 apply는 인스턴스 자신을 다시 반환하므로 생성되자마자 조작된 인스턴스를 변수에 바로 넣어줄 수 있다. 
      
      name = "[초특가]" + name
      discount()
      }
          
     // 기존 같으면 
      // a.name = "[초특가]" + a.name
      // a.discount()
    }
    
    class Book(var name: String, var price: Int){
       fun discount(){
         price -= 2000
       }
     }
 ```  
 
 - run은 apply처럼 run 스코프 안에서 참조연산자를 사용하지 않아도 된다는 점은 같다.
 - 일반 람다함수처럼 인스턴스 대신 마지막 구문에 결과 값을 반환한다. 
 - 이미 인스턴스가 만들어진 후에 인스턴스의 함수나 속성을 스코프내에서 사용해야할 때 유용하다.

 ```
    fun main() {
      var a = Book("디모의 코틀린", 10000).apply{
        name = "[초특가]" + name
        discount()
      }
      
      a.run{
        println("상품명: ${name}, 가격:${price}원"
      }
    }
    
    class Book(var name: String, var price: Int){
       fun discount(){
         price -= 2000
       }
     }
 ```  
  
- with은 run과 동일한 기능을 가지지만 단지 인스턴스를 참조 연산자 대신 패러미터로 받는다.
- a.run {...} >>>>> with(a)


- also/let
  - 처리가 끝나면 인스턴스를 반환 >> **apply / also**
  - 처리가 끝나면 최종 값을 반환 >> **run / let**
  - 차이점 >> apply와 run이 참조 연산자 없이 인스턴스의 변수와 함수를 사용할 수 있었다면, 
  - also와 let은 마치 패러미터로 인스턴스를 넘긴것처럼 it을 통해서 인스턴스를 사용할 수 있다.
  - 이 두 함수는 왜 굳이 패러미터를 통해서 인스턴스를 사용하는지?
    - 같은 이름의 변수나 함수가 스코프 밖에 중복되어 있는 경우 혼란을 방지


#### 오브젝트
- 싱글톤 패턴을 언어 차원에서 지원
- object는 인스턴스를 생성하지 않고 그 자체로 객체이므로 생성자를 사용하지 않음.
- 최초 사용시 자동으로 생성되어 코드 전체에서 공용으로 사용
  - 프로그램이 종료되기 전까지 공통적으로 사용될 내용들을 묶어 만드는게 좋다.
- 기존 클래스에서도 오브젝트를 만들 수 있다. ( Companion object )
  - static 맴버와 비슷

#### 익명객체와 옵저버 패턴
- 이벤트가 발생할 때마다 즉각적으로 처리할 수 있도록 만드는 프로그래밍 패턴을 옵저버 패턴으로 부른다.
- 옵저버 패턴을 구현할 때는 두 개의 클래스가 필요하다.
  - 하나는 이벤트를 수신, 하나는 이벤트의 발생 및 전달
  - 두 클래스 간의 통신은 B에서 이벤트가 발생했을 때, A에서 이벤트를 처리
    - A에서 B를 참조할 수 있지만 B는 A를 참조할 수 없다.
      - 그래서 이 사이에 **인터페이스**를 만든다. >> 옵저버 / 리스너(코틀린에서는)
      - 이렇게 이벤트를 넘겨주는걸 **콜백**이라고 한다.
      - 실전 프로젝트에서 사용된 것 같음 !
 ```
  프레그먼트, 액티비티 >> 요청을 보내는 형태로 작성
  뷰랑 프래그먼트를 나눠놓고 서비스에서 뷰를 통해 프레그먼트와 서비스가 서로 데이터를 주고받는다.
  그래서 프래그먼트에서 서비스를 떼어냈는데 서비스에서 프래그먼트로 다시 접근할 방법이 없으니까 HomeFragmentView(뷰) 만들어서 접근을 해준다.
 ```
- 옵저버 패턴은 이벤트를 기반으로 동작하는 모든 코드에서 광범위하게 쓰는 코드이므로 구조를 이해하는 것이 중요하다.
 
 
#### 클래스의 다형성

- 다운 캐스팅에는 as와 is가 필요하다.
- as는 변수를 호환되는 자료형으로 변환해주는 캐스팅 연산자로 코드 내에서 사용할 시 자료형을 즉시 변환하고 반환해준다.
- is는 변수가 자료형에 호환되는지를 먼저 체크한 후 변환하는 캐스팅 연산자로 조건문 내에서 사용된다.
 ```
  fun main(){
   var a = Drink()
   a.drink()  // 음료를 마십니다.
   
   var b : Drink = Cola() // b는 Drink 타입의 변수이지만 콜라에 인스턴스를 담았으므로 콜라에서 오버라이드 된 함수가 실행된다.
   b.drink()  // 음료 중에 콜라를 마십니다.
   
   //washDishes를 호출하기 위해서는 as나 is를 통해 다운 캐스팅을 해주어야 한다. 
   if (b is Cola){
     b.washDishes()
   }
   
   var c = b as Cola
   c.washDishes()
   b.washDishes() //as를 사용하면 반환값 뿐만 아니라 변수 자체도 다운 캐스팅
  }
  open class Drink {
    var name = "음료"
    
    open fun drink() {
      println("${name}를 마십니다.")
    }
  }
  
  class Cola: Drink() {
    var type = "콜라"
    
    override fun drink() {
      println("${name}중에 ${type}를 마십니다")
    }
    
    fun washDishes() {
      println("${type}로 설거지를 합시다")
    }
 ```


#### 캐스팅을 줄여주는 제너릭
- 클래스나 함수에서 사용하는 자료형을 외부에서 지정할 수 있는 제너릭
- 캐스팅 -> 프로그램의 속도를 저하시킨다.
- 타입을 자동으로 추론


#### 리스트
 ```
  fun main(){
    val a = listOf("사과", "딸기", "배")
    for(i in a)
    {
      print("${i}") // 리스트 모든 요소 출력
    }
    
    var b = mutableListOf(6, 3, 1)
    println(b) // [6, 3, 1]
    b.add(4) //4 추가
    println(b) // [6, 3, 1, 4]
    
    b.add(2,8) // 인덱스 2번 자리에 8 추가
    println(b) // [6, 3, 8, 1, 4]
    
   
    b.removeAt(1) //1번 요소 삭제
    println(b) // [6, 8, 1, 4]
    
    b.shuffle()
    println(b) // [1, 4, 6, 8]
    
    b.sort()
    println(b)
  }
 ```


#### 문자열을 다루는 법
 ```
  fun main(){
  
    val test1 = "Test.Kotlin.String"
    println(test1.toLowerCase()) // 소문자로 변횐
    println(test1.toUpperCase()) // 대문자로 변환
    
    val test2 = test1.split(".") // .을 기준으로 나누기  // [Test, Kotlin, String]
    
    test2.joinToString() // 그냥 합쳐짐 //Test, Kotlin, String
    test2.joinToString("-") // 그 문자열을 사이에 넣어줌 // Test-Kotlin-String
    
    test1.substring(5..10) // 그 부분만 출력 //Kotlin
  }
 ```
 
 - .isNullOrEmpty() // 널이거나 Empty이면 true
 - .isNullOrBlank() // 공백상태(blank)도 감지
 - .startsWith("java") // java로 시작하는 문자열이 있으면 true
 - .endsWith(".kr")
 - .contains("lin") // 포함되면 true
 
 
 
 #### null 값을 처리하는 방법? 동일한지를 확인하는 방법?
 - ?. (null safe operator) // 참조연산자를 실행하기 전에 객체가 null인지 확인부터하고 객체가 null이면 뒤따라오는거 실행 x
 - ?: (elvis operator) // 객체가 null이 아니라면 그대로 사용하지만 null이러면 연산자 우측의 객체로 대체
 - !!. (non-null assertion operation) // 참조연산자를 사용할 때 null여부를 컴파일시 확인하지 않도록 하여 런타임시 널포인터에러가 나도록 방치
 - null safe 연산자 (?.)는 스코프 함수와 사용하면 더욱 편리하다. // a?.run{ ~ } // 널체크에 if문 대신 사용
 - 객체의 동일성 판단 (===)


#### 함수의 argument를 다루는 방법과 infix 함수
 - 함수를 더 다양한 방법으로 사용할 수 있는 기능
 - overloading: 같은 스코프 안에서 같은 함수의 이름을 여러 개 만들 수 있다. 
 - 같은 자료형을 개수에 상관없이 패러미터로 받고 싶을 때 사용하는 vararg
 ```
  fun main(){
    sum(1,2,3,4) // 10
  }
  
  fun sum(vararg num: Int){
    var sum = 0 
    
    for(n in num){ //vararg가 붙은 패러미터는 배열처럼 for문으로 참조할 수 있다
      sum += n
    }
  }
 ```
 - 연산자처럼 쓸 수 있는 infix 함수
 ```
  fun main(){
    println( 6 multiply 4 ) // 6은 this , 4는 x에 해당
    // = println(6.multiply(4))
  }
  
  // 적용할 클래스가 자기 자신이므로 클래스 이름은 쓰지 않는다.
  infix fun Int.multiply(x: Int): Int = this * x // 자료형.이름
 ```

#### 중첩클래스와 내부클래스
- 중첩 클래스는 형태만 내부에 있을 뿐 실질적으로는 외부 클래스의 내용을 공유할 수 없다.
 ```
  class Outer{
    class Nested{
      //외부 클래스의 내용을 공유할 수 없음.  
    }
  }  //class Outer, class Outer.Nested 별개
 ```
- inner : 내부클래스
- 혼자서 객체를 만들 수는 없고 외부 클래스에 객체가 있어야만 생성과 사용이 가능한 클래스
- 내부 클래스는 외부클래스 객체안에서 사용되는 클래스이므로 외부 클래스의 속성과 함수의 사용이 가능하다.

 ```
    fun main(){
      Outer.Nested().introduce()   // Nested Class
      
      val outer = Outer()
      val inner = outer.Inner()
      
      inner.introduceInner()      // Inner Class
      inner.introduceOuter()      // Outer Class
      
      outer.text = "Changed Outer Class"
      inner.introduceOuter()      // Changed Outer Clas
    }
  
    class Outer{
      var test = "Outer Class"
    class Nested{
      fun introduce(){
        println("Nested Class")
      }
    }
    
    inner class Inner {
      var text = "Inner Class"
      
      fun introduceInner(){
        println(text)
      }
      
      fun introduceOuter(){ /OuterClass에 있는 text 속성을 출력하기
        println(this@Outer.text) // Outer 클래스와 Inner 클래스에 같은 이름의 속성이나 함수가 있다면 this@Outer.text로 참조
      } / 
    }
  
 ```
- 중첩클래스와 내부클래스는 클래스 간의 연계성을 표현하여 코드의 가독성 및 작성 편의성이 올라갈 수 있으므로 적절한 상황에서 사용

#### Data Class 와 Enum Class
- Data Class: 데이터를 다루는 데에 최적화된 class로 5가지 기능을 내부적으로 자동으로 생성해준다.
  - equals()의 자동구현: 내용의 동일성을 판단 
  - hashcode()의 자동구현: 객체의 내용에서 고유한 코드를 생성
  - toString()의 자동구현: 포함된 속성을 보기쉽게 나타냄
  - copy()의 자동구현: 객체를 복사하여 똑같은 내용의 새 객체를 만듦
    - 아무 패러미터가 없으면 똑같은 내용으로 생성함. 
    - val a = Data("A", 7)
    - val b = a.copy()  // 또는 val b = a.copy("B")
  - componentX()의 자동구현: 속성을 순서대로 반환함
    - Data("A", 7) // "A" --> **component1()**, 7 --> **component2()**
    - 이 함수는 사용자가 직접 호출하기 위한 함수가 아닌 배열이나 리스트 등의 데이터 클래스에 객체가 담겨있을 때 이 내용을 자동으로 꺼내 쓸 수 있는 기능을 지원하기 위한 함수

 ```
    fun main(){
      val a = General("A",212) // 일반 Class ==> 제대로 구현 X
      println(a == General("A",212)) // 일반 Class ==> 제대로 구현 X
      println(a.hashCode())  // 일반 Class ==> 제대로 구현 X
      println(a)  // 일반 Class ==> 제대로 구현 X
      
      val b = Data("B", 306)
      println(b ==  Data("B", 306))
      println(b.hashCode())
      println(b)
      
      println(b.copy())
      println(b.copy("C"))
      println(b.copy(id=618)
    }
    
    class General(val name: String, val id: Int)
    data class Data(val name: String, val id: Int)
  
 ```

 ```
    fun main(){
      
      val list = listOf(Data("A",212), Data("B", 306), Data("C", 618))
      //이 리스트레 담긴 Data 객체의 내용을 for문에서 모두 순회하려면 두 개의 속성을 받을 수 있는 이름을 지정하여 in 앞에 써준다.
      
      for((a, b) in list){  // a --> component1(), b --> component2()
        println("${a}, ${b}") //속성 모두 출력
      }
      
    }
    
    class General(val name: String, val id: Int)
    data class Data(val name: String, val id: Int)
  
 ```

- Enum Class: 열거형의 준말
```
  enum class Color{
    RED, BLUE, GREEN 
  } // 여러 개를 선언
  Color.RED  //하나의 상태 선택해서 나타냄
```
  - Enum Class는 관행적으로 상수를나타낼 때 사용하는 대문자로 기술
  - 또한 enum의 객체들은 고유한 속성을 가질 수 있다.
    - enum class에서 생성자를 만들어 속성을 받도록 하면 객체를 선언할 때 속성도 선언할 수 있다.
  - 일반 클래스처럼 함수도 선언할 수 있다.
    - 객체를 선언한 후 ;(새미콜론)을 추가하고 함수를 작성한다.
```
  enum class Color(val num:Int){
    RED(1), 
    BLUE(2), 
    GREEN(3); //새미콜론 추가
    
    fun isRed() = this == Color.RED
  } 
```





