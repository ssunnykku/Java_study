(Do it! 자바 완전 정복 12장 추상클래스와 인터페이스)
## 인터페이스
### 인터페이스의 정의와 특징
- 인터페이스: 내부의 모든 필드가 public static final로 정의되고, static과 default 메서드 이외의 모든 메서드는 public abstract로 정의된 객체지향 프로그래밍 요소
```java
interface 인터페이스명 {
    public static final 자료형 필드명 = 값;
    public abstract 리턴 타입 메서드명();
}
```
```java
interface A {
    public static final int a = 3;
    public abstract void abc();
}
```
- 인터페이스 내에서 필드, 메서드에 사용 가능한 제어자(modifier)가 확정되어 있으므로 필드와 메서드 앞의 제어자를 생략해도 컴파일러가 자동으로 각각의 제어자를 삽입한다.
```java
interface B {
    int a = 3;    // 생략해도 자동으로 public static final
    void abc();   // 생략해도 자동으로 public abstract
}
public class InterfaceCharacteristics {
    public static void main(String[] args) {
        // static 자동 추가됨
        System.out.println(A.a);        // 결과: 3
        System.out.println(B.b);        // 결과: 3  클래스명이나 인터페이스명으로 접근 가능
        
        // final 자동 추가 확인
        // A.a = 5;                 // 불가능
        // B.b = 5;                 // 불가능
    }
}
```

### 인터페이스의 상속
- implements(구현한다) 키워드를 사용한다.
- 다중 상속이 가능하다.
  - 클래스의 경우 두 부모 클래스에 동일한 이름의 필드 또느느 ㄴ메서드가 존재할 경우 이를 내려받으면 충돌이 발생한다.
  - 인터페이스에서는 모든 필드가 public static final로 정의되어 있어 실제 데이터값은 각각의 인터페이스 내부에 존재, 즉 저장 공간이 분리되어 다중 상속이 가능하다.
  - 메서드도 모두 미완성이며 자식 클래스 내부에서 완성해 사용한다.

```java
/**클래스가 인터페이스를 상속하는 구조*/
class 클래스명 implements 인터페이스명, ..., 인터페이스명 {
    // 내용
}
```
```java
/**클래스와 인터페이스를 동시에 상속하는 구조 */
class 클래스명 extends implements 인터페이스명 , ...., dlsxjvpdltmaud {
    // 내용
}
```
```java
/**인터페이스가 인터페이스를 상속할 때*/
인터페이스 extends 인터페이스 {
    // ...
}
```
- 인터페이스는 클래스를 상속할 수 없다.
```java
interface A {
    public abstract void abc();
}
interface B {
    void bcd();   // public abstract 자동 추가
}
class C implements A {
    public void abc() {      // 클래스가 인터페이스를 상속할 경우 반드시 인터페이스의 미완성 메서드를 이용한 완성된 메서드를 포함해야 한다.
        // ...
    }
}

/*public -> default 불가능 (접근 범위가 좁아져 오류 발생)
class D implements B {
    void bcd() {
    }
}
 */

```

### 인터페이스 타입의 객체 생성 방법
- 방법 1. 인터페이스를 일반 클래스로 상속해 객체 생성: 여러 개의 객체를 생성해야 할 때 유리
```java
interface A {
    int a = 3;
    void abc();
}
class B implements A {
    public void abc() {
        System.out.println("방법 1. 자식 클래스 생성자로 객체 생성");
    }
}
public class CreateObjectInterface_1 {
    public static void main(String[] args) {
        // 객체 생성
        A b1 = new B();
        A b2 = new B();
        
        // 메서드 호출
        b1.abc();        // 실행 결과: 방법 1. 자식 클래스 생성자로 객체 생성
        b2.abc();       // 실행 결과: 방법 1. 자식 클래스 생성자로 객체 생성
    }
}
```
- 방법 2. 익명 이너 클래스 사용: 1개의 객체만 생성할 때 사용시 유리
```java
interface A {
    int a = 3;
    void abc();
}
public class CreateObjectOfInterface_2 {
    public static void main(String[] args) {
        // 객체 생성
        A a1 = new A() {
            public void abc() {
                System.out.println("방법 2. 익명 이너 클래스를 이용한 객체 생성");
            }
        };
        A a2 = new A() {
            public void abc() {
                System.out.println("방법 2. 익명 이너 클래스를 이용한 객체 생성");
            }
        };
        // 메서드 호출
        a1.abc();      // 실행 결과: 방법 2. 익명 이너 클래스를 이용한 객체 생성
        a2.abc();       // 실행 결과: 방법 2. 익명 이너 클래스를 이용한 객체 생성
    }
}
```

### 인터페이스의 필요성
(예시) 그래픽카드 드라이버 교체
```java
/**A사 그래픽카드 드리이버 설치*/
class Graphic_Impl implements Graphic {
    public void brightness(int value) {...}
    public void contrast(double value) {...}
    public void display() {...}
}
```
```java
/**B사 그래픽카드 드리이버 설치*/
class Graphic_Impl implements Graphic {
    public void brightness(int value) {...}
    public void contrast(double value) {...}
    public void display() {...}
}
```
```java
interface Graphic {
    void brightness(int value);
    void contrast(double value);
    void display();
}
```
```java
/**애플리케이션*/   
Graphic g = new Graphic_Impl();
g.brightness(80);
g.contrast(90.3);
g.display();  
```
- 인터페이스 사용으로 그래픽 카드 변경이 용이하다. 그래픽 카드를 교체해도 애플리케이션은 수정할 필요가 없다.

### 디폴트 메서드와 정적 메소드
#### 자바8이 등장하며 인터페이스에 추가된 기능
##### 1. 디폴트 메서드가 포함될 수 있게 되었다.
  - 기존에 100개의 자식 클래스를 가진 인터페이스가 있다고 했을 때, 인터페이스 내에 메서드를 추가하면 이전에 만들어 사용하던 모든 자식 클레스에서 오류가 발생하게 된다. 새롭게 추가된 메서드를 구현하지 않았기 때문이다.
  - default 메서드로 인터페이스 내부에 메서드를 삽입하면 위와 같은 문제를 해결할 수 있다.
```java
interface 인터페이스명 {
    public default 리턴 타입 메서드명 {     // public 생략 가능
        // 메서드 내용
    }
}
```
```java
interface A {
    void abc();
    default void bcd() {
      System.out.println("A 인터페이스의 bcd()");
    }
}
class B implements A {
    public void abc() {
      System.out.println("B 클래스의 abc()");
    }
}
class C implements A {
  public void abc() {
    System.out.println("C 클래스의 abc()");
  }
  public void bcd() {               // 인터페이스 A의 디폴트 메서드 오버라이딩
    System.out.println("C 클래스의 bcd();");
  }
  
  public class DefaultMethod_1 {
    public static void main(String[] args) {
      // 객체 생성
      A a1 = new B();
      A a2 = new C();
      
      // 메서드 호출
      a1.abc();             // B 클래스의 abc()
      a1.bcd();             // A 인터페이스의 bcd()         
      a2.abc();             // C 클래스의 abc()
      a2.bcd();             // C 클래스의 bcd()
    }
  }
}

```
- 디폴트 메서드는 인터페이스 내부에 속하는 일반 메서드처럼 동작하기 때문에 자식 클래스에서 부모 인터페이스의 디폴트 메서드도 호출할 수 있다.
```java
부모 인터페이스명.super.디폴트 메서드명
```
- 클래스의 경우 부모 클래스의 메서드를 호출할 때 ```super.부모메서드명```로 호출하는데 인터페이스의 메서드를 호출할 때는 super앞에 부모 인터페이스명까지 붙는다.(인터페이스는 다중상속이 가능하기 때문임)
```java
/**자식 클래수에서 부모 인터페이스의 디폴트 메서드 호출*/
interface A {
    default void abc() {
      System.out.println("A 인터페이스의 abc();");
    }
}
class B implements A {
    public void abc() {
        A.super.abc();   // 부모 인터페이스 A의 abc()메서드 호출
        System.out.println("B 클래스의 abc()");
    }
}
public class DefaultMethod_2 {
  public static void main(String[] args) {
    // 객체 생성
    B b = new B();
    
    // 메서드 호출
    b.abc(); // B 객체의 abc()를 호출할 때 A 인터페이스의 abc() 메서드가 먼저 호출됨
    
    // 실행 결과
    // A 인터페이스의 abc()
    // B 클래스의 abc()
  }
}
```

##### 2. static 메서드를 포함할 수 있다.
``` 
인터페이스명.정적 메서드명
```
```java
interface A {
    static void abc() {
      System.out.println("A 인터페이스의 정적 메서드 abc()");
    }
}
public class StaticMethod {
  public static void main(String[] args) {
    // 정적 메서드 호출
    A.abc();            // 실행 결과: A 인터페이스의 정적 메서드 abc()
  }
}
```