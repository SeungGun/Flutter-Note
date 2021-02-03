<h2>Flutter를 위한 Dart 문법</h2>

<hr>

- About Dart
  * Java와 Javascript를 적절하게 섞은 느낌 (기본적인 Java는 알고 있어야 될 듯)
  * 그렇기에 문장의 끝에는 세미콜론(;)을 붙힌다.

<hr>

<h2>자료형(변수 타입)</h2>

<blockquote>기본 자료형</blockquote>

1. int  - 정수

2. double -  실수

3. String - 문자열 => 문자열을 표현할 때 작은 따옴표(' ') 와 큰 따옴표(" ") 둘다 표현 가능

   문자열에서 변수 접근(?) =>  "$"를 이용한다. 

   ```dart
   var name = '홍길동';
   print('안녕하세요 제 이름은 $name'); // 일반 변수일 때 (그냥 사용)
   
   var person = Person(10,'홍길동');
   print('안녕하세요 제 이름은 ${person.name}'); // 객체일 때 (중괄호로 씌움)
   ```

4. bool - 참/거짓

5. num - int와 double을 포함하는 타입(그냥 모든 범위의 숫자를 담는 자료형)

   

<blockquote>Dart에서는 변수 타입을 추론할 수 있다. </blockquote>

- javascript에서의 var, C++에서의 auto와 동일한듯 하다.

  => **var**  키워드를 사용한다. 

  ```dart
  void main(){
      var a = 6;  // int
      var b = 8.22; // double
      var c = 'String1'; // String
      var d = 'String2'; // String
      var e = true; // bool
  }
  ```

- **dynamic** 키워드

  dynamic도 var와 마찬가지로 타입을 추론을 하는 방식이다. 

  그러나 일반적으로 기본으로 사용할 때는 var를 사용하고, dynamic은 함수와 같이 사용한다.

  (dynamic은 Java에서 Object 와 유사한 느낌

  => 모든 클래스는 Object 클래스를 extends하므로 캐스팅이 가능함 DownCasting)
  
  ```dart
  void main(){
      dynamic c = 10;
      myPrint(c);
      myPrint('Hello');
  }
  myPrint(dynamic v){
      //TODO
}
  ```
  
  

<hr>

<h2>상수</h2>

<blockquote>final, const 키워드</blockquote>

- 상수를 표현하고 싶을 때 사용 

  => 이는 상수화 시켰을 때는 다른 언어들과 마찬가지로 값을 바꿀 수 없음

- Java에서의 final, C/C++에서의 const 와 동일

- 또한 final, const를 쓸 때 Dart에서는 타입을 생략해도 됨.

  ```dart
  void main(){
      const int a = 10;
      final String b = "Test";
      // 값을 바꾸려고 시도하면 에러 발생
      const c = 5; // 타입 생략
      final d = "Hi"; // 타입 생략
  }
  ```

  <blockquote>주의</blockquote>

  **final, const** 키워드는 **var**타입과 같이 사용할 수 없다.

  <blockquote>final vs const (정확한 이해 X)</blockquote>

  **final**은 동적으로 메모리 할당됨 - const 경우 외에 (그렇기에 잘 모르겠으면 그냥 final로 사용)

  **const**는 컴파일 타임에 상태, 메모리에 이미 저장됨 - 재사용할 때 유용

<hr>

<h2>연산자</h2>

<blockquote>산술 연산자</blockquote>

1. +

   덧셈 - 숫자 덧셈 & 문자열 concat 

2. -

   뺄셈

3. *

   곱셈

4. /

   나누기 - 실수(소수점까지)

5. %

   나머지 -  모듈러 연산

6. ~/

   나누기 - 결과값이 정수부분만 나옴(몫)

<blockquote>비교, 논리 연산자</blockquote>

- Java, C/C++와 동일

  ==, !=, >,<, >=, <=, &&, ||, ! 

<hr>

<h2>데이터 타입 검사</h2>

<blockquote>is 키워드</blockquote>

- 이 타입이 이 타입이 맞는가? 하고 확인하는 키워드 

  1. **is**

     같은 타입이면 **true** 리턴 , 다른 타입이면 **false** 리턴

  2. **is!**

     같은 타입이면 **false** 리턴, 다른 타입이면 **true** 리턴

```dart
void main(){
    int a = 20;
    if(a is int)
    {
        print('a is int type');
    }
    else
    {
        print('a is not int type');
    }
    /** ------------------------- **/
    int b = 232;
    if(b is! double)
    {
        print('b is not double type');
    }
    else
    {
        print('b is double type');
    }
    
    //결과 값 
    // a is int type
    // b is double type
}
```

* var 타입에 대해서는?

  var 타입으로 선언 및 초기화를 한 변수는 내부적으로 값에 해당하는 데이터 타입으로 간주한다.

  ```dart
  void main(){
      var a = 10;
      if(a is int)
      {    
          print('a is int type');
      }
      else
      {
          print('a is not int type');
      }
      // 결과
      // a is int type
  }
  ```

  **주의!** 

  - **a is var 와 같은 문장은 그 자체가 성립하지 않는다. (is 뒤에 var는 올 수 없다.) **

* **num** 타입에 대해서는?

  num은 하나의 타입이지만 int와 double을 포함한 타입이다. 

  **num >= int, double 이고, int, double => num이고, num => num이다. **

<hr>

<h2>데이터 타입 변환</h2>

<blockquote>as 키워드</blockquote>

- 타입변환은 int, String, double등 데이터 타입을 다른 타입으로 변환을 하는 것이다.

  (물론 타입마다 연관이 있어야 변환 가능)

  => 서로 관계가 있으면 변환이 가능하고, 상위 타입으로 변환이 가능하다.

  그럴 때 "타입 캐스팅"을 할 때 사용하는 것이 **"as"** 키워드이다. 

  **하지말아야할 주의할 점**

  1. 동일 타입 캐스팅(불필요)

  2. 업캐스팅(적절하지 못함) - sub를 super로 타입 캐스팅 하는 경우 

     ```dart
     void main(){
         int n = 10;
         double d = n; // 에러 
         //Java에서는 이렇게 해도 문제가 없지만
         // 플러터에서는 암시적으로 int의 상위 타입인 double로 타입캐스팅을 시도하려고 하면 에러 발생함
         //그렇기에
         double d = n as double; //이렇게 명시적인 타입 캐스팅을 해줘야함 
         
         //또한 그렇기에 num 타입으로 바꿔주면 더 간편함
         num d = n;
     }
     ```

<hr>

<h2>컬렉션</h2>

> Java에서의 Collection Framework

<span style="color:red">Dart에서는 Array(배열)이라는 자료구조가 없다.</span>

1. **List** 

   ```dart
   void main(){
       List<String> items = ['a','b','c'];
       print(items);
   }
   ```

   2번째 방법

   ```dart
   void main(){
       var items = [1,2,3];
       print(items);
   
       // var는 타입추론이라서 List도 가능함
   }
   ```

   >  **List**에 접근 하는 방법 

   - Java에서 배열에 접근하듯이 인덱스로 접근

   ``` items[0]```

   - List이기 때문에 Java에서 사용했던 것 처럼 여러가지 method 사용 가능

      

2.  Set

   > 중복 값이 없는 구조

   ```dart
   void main(){
       Set<String> itemSet = {1,2,3};
       print(itemSet);
   }
   ```

   List와 마찬가지로 var를 통해 추론

   ```dart
   void main(){
       var itemSet = {1,2,3};
       print(itemSet);
   }
   ```

3.  Map

   > Key와 Value 쌍으로 가지는 구조 json 형태

   ```dart
   void main(){
       var itemMap = {
           'key1': 1,
           'key2': 2,
           'key3': 3,
       };
   }
   ```

> Spread operation



<hr>

<h2>함수, 메소드</h2>

- 기본 함수 형태는 Java와 동일하다

  리턴 타입 함수이름(파라미터){

  }

> Parameter - Option, Required

- 우선 기본 예시를 하나 만들어 본다.

  ```dart
  void main(){
      something('name');
  }
  void something(String name){
      
  }
  ```

  파라미터의 이름을 지정을 해서 사용하는 경우는 option으로 변경해줘야 한다. 

- 파라미터에 중괄호를 씌워주면 option으로 변경된다. 

- option으로 변경되면서 option으로 씌워진 파라미터의 이름을 이 함수를 호출할 때 지정하고 값을 넘겨줘야한다. 

  ```dart
  void main(){
      something(name: '홍길동'); //name 파라미터 지정과 함께 값 지정
  }
  void something({String name}){ //option이 된 name 파라미터
      
  }
  ```

- 또한 option을 지정하는 경우는 여러가지를 넣을 때에도 유용하다.

  ```dart
  void main(){
      something(age : 10); //name 파라미터 지정과 함께 값 지정
  }
  void something({String name, int age}){ //option이 된 name 파라미터
      
  }
  ```

  위와 같이 option이기 때문에 파라미터에 대해서 모두 넣어줄 필요가 없다.

  - Java에서 메소드를 오버로딩을 하는데, 이 option을 처리함으로써 오버로딩할 필요가 없다.

- 또한, 어떤 파라미터는 필수인데, 어떤 파라미터는 option인 경우 

  필수인 파라미터는 일반적인 형태로 쓰고 option인 경우는 중괄호 안에 넣어주면 된다. 

  ```dart
  void main(){
      something('홍길동',age : 10); 
      // name 파라미터는 필수므로 그대로 넣어주고, 
      // option인 age는 파라미터 이름을 지정해서 값을 줘야한다.
  }
  void something(String name, {int age}){ 
      //name 파라미터는 필수이고 age 파라미터는 option이다.
     
  }
  ```

- 넘겨주지 않아도 어떤 값은 꼭 가지고 있어야될 경우 (default 값)

  ```dart
  void main(){
      something('홍길동'); 
  	//option인 age를 넣어주지 않아도 age는 기본으로 default 값을 가지게 된다.
  }
  void something(String name, {int age = 10}){ 
  	//option인 age 파라미터에 default 값으로 10을 줌
  }
  ```

- option중에서는 반드시 넣어줘야 하는 option을 지정하고 싶을 때

  @required 키워드를 파라미터 앞에 붙여주면 된다.

  ```dart
  void main(){
      something('홍길동', age : 10); 
  	//option인 age를 넣어주지 않아도 age는 기본으로 default 값을 가지게 된다.
  }
  void something(String name, {@required int age}){ 
  }
  ```

> Method는 Dart에서 일급 객체이다.(first-class object)

```dart
child : Button(onPressed : something, ) //입력과 출력이 같은 메소드인 경우 
```

> 익명 함수

- 그저 이름만 없는 함수이다. 

  ```dart
  void something(){
      
  }
  
  child : Button(onPressed : (){
      
  } ) 
      
      /**위와 같이 
      	(){
      	
  		}
  		이런 구조를 가지는 함수 
  	**/
  ```

> 람다식 

- 한줄로 작성되어 있는 메소드는 "=>"로 표현할 수 있다. 

  ```dart
  String get name{
      return _name;
  }
  // 람다식으로 변경
  String get name => _name; 
  ```

  

<hr>

<h2>?와 ??</h2>

> ?? 키워드

- null 처리를 위한 키워드 

  Dart에서는 변수에 값을 초기화 시키지 않으면 null값이 들어있다. 

  ```dart
  a = b ?? c;
  ```

  이는 **b가 null이 아니면 a에 할당한다. 아니면 c를 할당한다. 라는 의미이다. **

- ??= 

  ```dart
  a ??= b;
  ```

  이는 **a가 null이면 b를 할당한다**라는 의미이다.



> ? 키워드

- 이것도 마찬가지로 null 처리를 위한 키워드이다. (특히 객체의 멤버 메소드호출에 대해서 )

  일단 Java에서 한 객체를 생성하고 멤버에 접근을 할텐데 만약 이 객체가 null을 참조하고 있으면

  멤버에 접근할 수 없게 되어 Runtime 에러가 발생한다. 이를 방지하기 위한 기법이다. 

  ```dart
  a?.test();
  ```

  이는 **a가 null이 아니면 실행한다** 라는 의미이다. 

  **Ex)**

  ```dart
  void main(){
      String name;
      print(name?.toLowerCase());
  }
  ```

  null이 아닐때만 메소드를 호출한다. 

<hr>

<h2>Class</h2>

- 기본적인 구조는  Java와 동일하다 .

  <u>객체를 생성할 때 Java에서는 **new**키워드를 쓰는데 Dart에서는 생략이 가능하다.</u>

  ```dart
  void main(){
      var person = Person(); 
  }
  class Person{
  	String name;
  	int age;
  }
  ```

  > 생성자

  ```dart
  class Person{
      String name;
      int age;
      Person(this.name, this.age);
  }
  ```

  - 생성자에도 위에서 말한 함수의 특징 중 하나인 option도 넣을 수 있다. 

> 접근 제어자

- 클래스내에서 멤버를 그냥 쓰면 **public**이다. 
- 클래스내에서 멤버이름 앞에 _(underscore)를 붙여주면 **private**가 된다.



> getter, setter

* Generate 메뉴에서 Getter, Setter 만들 수 있음



> cascade

- 반복 작업 여러번 할 때 사용

  ".." (점 두개)를 사용 

  객체 생성하고 바로 실행시켜줘야될 부분을 축약한다는 느낌? 

  객체 생성하고 값 초기화할 때 사용?

  ```dart
  var person = Person();
  person.setName('홍길동');
  person.setAge(10);
  
  var person2 = Person();
  ..setName('홍길동')
  ..setAge(10); 
  // 위 두가지는 동일한 구문 
  ```



> implements

- Java와 다르게 Dart에서는 클래스를 implements하여 Java의 interface처럼 사용할 수 있다. 

  (그렇기에 Dart에는 interface가 없다.)

- 이렇게 사용하였을 때는 implements를 해야하는 클래스의 멤버를 @override 키워드와 함께 오버라이딩 된다. 

  ```dart
  class Employee implements Person{
      @override
      int age;
      
      @override
      String name;
      
      @override
      void setAge(int age){
          
      }
      
      @override
      void setName(String name){
          
      }
  }
  
  class Person{
  	int age;
      String name;
      void setAge(int age){
          this.age = age;
      }
      void setName(String name){
          this.name = name;
      }
  }
  ```

  - 위의 경우는 필드에 값이 없으면 안되기 때문에 멤버변수까지 오버라이딩된다.

  - 변수에 **초기값이 있거나 생성자가 있으면** 멤버변수는 오버라이딩할 필요가 없다.



> mixin - with 키워드

- 위와 같이 클래스를 implements를 하면 조건에 맞는 멤버들을 모두 오버라이딩 해야한다. 

  선택적으로 오버라이딩을 하고싶을 때 사용하는 것이 **with**키워드이다. 

  ```dart
  class Employee with Person{
      @override
      void setName(String name){ //setName 메소드만 오버라이딩
          
      }
  }
  ```



<hr>

<h2>Future, async, await</h2>

- 버튼 클릭을 했는데 네트워크 요청을 해야한다. 이는 비동기로 실행이 되어야한다. 
- 그러한 메소드들을 Future형태이다. (언제 끝나는지 모름)

**Future 타입으로 리턴받는 형태**

```dart
void main(){
	print('시작');
    networkRequest();
    print('끝');
}
Future networkRequest() async{ //나중에 비동기로 끝나는 
    print('요청 시작');
    await Future.delayed(Duration(seconds : 3)); //await : 기다리게 함 
    print('요청 끝'); // 이 코드는 위의 코드가 끝나야만 실행된다. (3초 후에 출력)
    //await가 없으면 위의 Future 코드는 비동기로 작동한다. 
}

//결과

// 시작
// 요청 시작
// 끝
// 요청 끝
```



<hr>

<h2>Stream</h2>

**아직 어려우니 정리 X **

- 또 다른 비동기 처리 
  - Future 같은 경우는 한번 요청하고 끝내야하는 경우
  - Stream 같은 경우는 계속해서 상태를 보고 있는 경우

**setState는 전체를 다시 그리는데,**

**Stream 객체를 활용하면 그 부분만 다시 그려진다.**

- 성능면에서 좋다.



<hr>

<h2>주석</h2>

- 클래스나 메소드를 문서화하고 싶다면 Slash 3개 (///) 

  => 그 부분을 호출했을 때 정보가 주석까지 나옴 

- 그렇지 않으면 Slash 2개 (//)

- 범위 주석 /**  **/ 



<hr>

<h2>Reference</h2>

<a>https://www.youtube.com/watch?v=J_cQyPGyHRI</a>

<a>https://blockdmask.tistory.com/394?category=415337</a>



