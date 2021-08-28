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
  
  
  
  
  
  
  

