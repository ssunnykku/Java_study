(DO it! 자바 완전 정복)
## 생성자
- 생성자(constructor): 객체를 생성하는 역할을 지닌 클래스의 내부 구성 요소로
객체 내에 포함되는 필드의 초기화를 주로 수행
## 특징
### 문법적 규칙
1. 반드시 클래스명과 동일한 이름으로 지어야 한다.
2. 메서드와 비슷한 구조이지만 리턴 타입이 없다.("리턴하지 않는" void와는 다른 이야기임)

```java
class A {
    A() {
        // ...
    }
}
```

### 기본 생성자의 자동 추가
- 생성자를 포함하지 않는 클래스에게 컴파일러가 기본 생성자를 추가해준다. 그래서 생성자를 만들지 않아도 `A a = new A()`와 같이 생성자를 호출해 객체를 만들 수 있다.
여기서 기본생성자는 입력매개변수가 없는 생성자를 말한다.
  - 클래스 : 붕어빵 기계
  - 객체 : 붕어빵
  - 생성자 : 붕어빵을 찍는 기능
  - 모든 클래스는 생성자를 포함해야 한다.

### 생성자의 동작 과정
- 생성자 호출되면 객체가 내부적으로 생성된다.
- 생성자의 실행문, 즉 생성자의 중괄호 안은 객체가 생성된 이후 할 일이 작성되는 부분이다.
- 일반적으로 여기에서 필드를 초기화한다.

```java
class C {
    int m;
    void work() {
        System.out.println(m);
    }
    C(int a) {         // -> 입력매개변수를 포함하고 있는 생성자 정의
        m = a;        // 입력매개변수로 전달된 값으로 필드 초기화
    }
}

public class DefalutConstructor {
    public static void main(String[] args) {
        // 클래스의 객체 생성
        // C c = new C();     // 기본 생성자 호출 불가능
        
        C c = new C(3);       // 직접 정의한 생성자를 호출해 객체 생성
        
        // 메서드 호출
        c.work();         // 출력 : 3
    }
}

```

### 생성자와 객체의 생성 방법
- 생성자의 모양에 따라 객체를 생성하는 방법이 결정된다.
- 생성자도 메서드처럼 오버로딩을 할 수 있다. 

```java
class A {
    A() {
        System.out.println("첫 번째 생성자");
    }
    A(int a) {
        System.out.println("두 번째 생성자");
    }
    A(int a, int b) {
        System.out.println("세 번째 생성자");
    }
    public class ConstructorOverloading {
        public static void main(String[] args) {
            A a1 = new A();
            A a2 = new A(3);
            A a4 = new A(3, 5);
        }
    }
}

/**
 * 실행 결과
 * 첫 번째 생성자
 * 두 번째 생성자
 * 세 번째 생성자
 */

```
