(이것이 자바다 ch5 참조 타입)
## 참조 타입
### 데이터 타입 분류
- 기본 타입(primitive type) 참조 타입(reference type)
- 참조 타입 : 객체(object)의 번지를 참조하는 타입으로 배열, 열거, 클래스, 인터페이스 타입이 있다.
- 객체(object) : 데이터(필드)와 메소드로 구성된 덩어리
- 변수들은 모두 스택(stack)이라는 메모리 영역에 생성된다.
0 기본 타입 변수는 스택(stack)영역에 값 자체를 저장하지만 참조 타입으로 선언된 변수는 힙 메모리 영역의 객체가 저장된 번지를 저장하고 이 번지를 통해 객체를 참조한다.

### 메모리 사용 영역(Runtime Data Area)
1. 메소드 영역(Method Area)
   + 바이트 코드 파일을 읽은 내용이 저장되는 영역
   + 클래스별로 상수, 정적 필드, 메소드 코드, 생성자 코드 등이 저장된다.
2. 힙 영역(Heap Area)
   + 객체가 생성되는 영역
   + 객체의 번지는 메소드 영역과 스택 영역의 상수와 변수에서 참조할 수 있다.
3. 스택 영역 (Stack Area)
    + 메소드를 호출할 때마다 생성되는 프레임(Frame)이 저장되는 영역
    + 메소드 호출이 끝나면 프레임은 자동 제거된다.
    + 프레임 내부에는 로컬 변수 스택이 있는데 여기에서 기본 타입 변수와 참조 타입 변수가 생성되고 제거된다.

### 참조 타입 변수의 ==, != 연산
- 참조 타입 변수의 값은 객체의 번지이므로 번지를 비교하게 된다. 번지가 같다면 동일한 객체를, 다르다면 다른 객체를 참조하는 것이다.

### Null과 NullPointerException
- 참조 타입 변수의 초기값으로 null이 사용될 수 있다. null로 초기화된 참조 변수는 스택 영역에 생성된다.
```java
String refVar1 = "자바";
String refVar2 = null;  // 아직 번지를 저장하고 있지 않다는 의미

refVar1 == null; // 결과: false
refVar1 != null; // 결과: true

refVar2 == null; // 결과: true
refVar2 != null; // 결과: false
```

- NullPointerException
  - 변수가 null인 상태에서 객체의 데이터나 메소드를 사용하려 할 때 이 예외가 발생한다.
  - 변수에 null을 대입하면 번지를 잃게 되므로 더이상 객체를 사용할 수 없게 된다.
  - 객체를 참조하지 않으면 자바는 해당 객체를 쓰레기로 취급하고 쓰레기 수집기(Garvage Collector)를 실행시켜 자동으로 제거한다.
```java
int[] intArray = null;
intArray[0] = 10;   //NullPointerException
```

### 문자열(String) 타입
- String 변수를 선언하고 변수에 문자 리터럴을 대입하면 문자열은 String 객체로 생성되고, 객체의 번지가 각각 대입된다.

#### 문자열 비교
- 자바는 문자열 리터럴이 동일하다면 String 객체를 공유하도록 설계되어 있다. 다음과 같이 name1과 name2 변수에 "홍길동"을 대입할 경우, name1과 name2 변수에는 동일한 String 객체의 번지가 저장된다.
```java
String name1 = "홍길동";
String name2 = "홍길동"
```
new-  연산자: 새로운 객체를 만드는 연산자, 객체 생성 연산자
```java
String name3 = new String("홍길동");
String name4 = new String("홍길동");
```
- new 연산자로 직접 String 객체를 생성하고 대입한 위 예제의 경우 name3과 name4 변수는 서로 다른 String 객체의 번지를 가지게 된다.
```java
name1 == name2    // 결과: true
name3 == name4    // 결과: false
```
```java
boolean result1 = str1.equals(str2);
boolean result2 = str1.equals(" ");
```
- 번지와 상관 없이 내부 문자열을 비고 할 때에는 String 객체의 equals() 메소드를 사용한다.

#### 문자 추출
```java
String subject = "자바 프로그래밍";
char charValue = subject.charAt(3);   // 결과: '프'
```
- charAt(인덱스) : 인덱스의 문자를 리턴한다.

#### 문자열 찾기
```java
String subject = "자바 프로그래밍";
int index = subject.indexOf("프로그래밍");  // 결과: 3
```
- indexOf(문자열): 문자열이 시작되는 인덱스를 리턴한다. 주어진 문자열이 포함되어 있지 않으면 -1을 리턴한다.
- 문자열의 포함 여부를 확인하려면 contains()를 활용한다.

### 배열(Array) 타입
#### 배열
- 연속된 공간에 값을 나열시키고, 각 값에 인덱스(index)를 부여해 놓은 자료구조이다.
- 같은 타입의 값만 관리한다.
- 배열의 길이는 생성과 동시에 결정되며 늘리거나 줄일 수 없다.
- 배열 변수는 참조 변수이다. 힙 영역에 생성되고 배열 변수는 힙 영역의 배열 주소를 저장한다.
- 배열 변수도 null로 초기화할 수 있다.
```java
타입[] 변수;
변수 = { 값0, 값1, 값2, 값3, ... };  // 컴파일 에러
```
- 배열 변수를 미리 선언한 후에는 값 목록을 변수에 대입할 수 없다.
```java
변수 = new 타입[] { 값0, 값1, 값2, 값3, ... };
```
- 배열 변수를 선언한 시점과 값 목록이 대입되는 시점이 다르다면 new 타입[]을 중괄호 앞에 붙여준다.
```java
// 메소드 선언: 매개변수가 이미 선언되어 있고, 호출 시 값 목록을 제공한다.
void printItem(int[] scores) { ... }

// 잘못된 메소드 호출
printItem( {95, 85, 90} );  // 컴파일 에러

// 올바른 메소드 호출
printItem( new int[] {95, 85, 90} );
```

#### 객체를 참조하는 배열
```java
String[] languages = new String[3];
languages[0] = "Java";
languages[1] = "Java";
languages[2] = new String("Java");

System.out.println(languages[0] == languages[1]);     // true: 같은 객체를 참조
System.out.println(languages[0] == languages[2]);     // false: 다른 객체를 참조
System.out.println(languages[0].equals(languages[2]));     // true: 문자열이 동일
```
- new 연산자로 생성된 String 객체는 다른 번지에 저장된다.

#### 배열 복사

```java
System.arraycopy(원본 배열, 원본 배열 복사 시작 인덱스, 새 배열, 새 배열 붙여넣기 시작 인덱스, 복사 항목 수);
```
