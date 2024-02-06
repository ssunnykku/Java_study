(Do it! 자바 완전 정복)
## this , this()메서드
- 클래스 자신의 내부 구성 요소를 호출하는 문법 요소
### this
- 자기 객체를 가리키는 참조 변수명으로 인스턴스 메서드 내부에서 필드를 사용하거나 메서드를 호출할 때 참조 변수명으로 사용한다.
- 생략했을 때 컴파일러가 자동으로 추가해 준다.
- 자신의 객체를 의미
### this() 메서드
- 자신의 또 다른 생성자를 호출하고, 생성자 내에서만 사용할 수 있으며, 항상 첫 줄에 위치해야 한다.
- 자신의 생성자를 의미

## super, super() 메서드
- 상속 관계에서만 사용할 수 있다.
### super
- 부모의 객체를 가리킨다.
- 필드명의 중복 또는 메서드 오버라이딩으로 가려진 부모의 필드 또는 메서드를 호출하기 위해 사용한다.

```java
class A {
   void abc() {
      System.out.println("A 클래스의 abc());
    }
}

class B extends A {
   void abc() {
      System.out.println("B 클래스의 abc()");
   }
   void bcd() {
      abc();                        // this.abc(); -> B 클래스의 메서드
   }
}

class C extends A {
  void abc() {
     System.out.println("C 클래스의 abd()");
    }

  void bcd() {
    super.abc();                 // 부모 클래스 객체의 abc() 메서드 호출
    }
}
```

### super()
- 부모의 생성자를 호출
- this() 처럼 생성자의 내부에서만 사용할 수 있다.
- 반드시 첫 줄에 와야 한다.
- this() 메서드도 생성자의 첫 줄에만 올 수 있으므로 이 둘은 1개의 생성자에서 절대로 같이 쓸 수 없다.
- 모든 생성자의 첫 줄에는 반드시 this() 또는 super()가 있어야 한다. **_만일 아무것도 써 주지 않으면 컴파일러는 super()를 자동으로 삽입한다._** 
- **_즉, 생성자를 호출할 때는 항상 부모 클래스의 생성자가 한 번은 호출된다._**
- 따라서 자식 클래스의 생성자로 객체를 생성할 때 부모 크래스의 객체가 만들어지게 된다.

    ```java
    class A {
      A (int a) {
         System.out.println("A 생성자");
       }
    }
    class B extends A {
    
    }                     // 오류 발생
    ```

    - A 클래스에는 int 값을 매개변수로 받는 생성자가 정의되어있다. 컴파일러는 기본 생성자를 자동으로 추가하지 않는다.
    - B클래스는 컴파일러가 기본 생성자를 자동으로 삽입해 준다. A 클래스를 상속받고 있으므로 첫 줄에 super() 메서드가 자동으로 삽입된다.
    - A 클래스는 기본 클래스 A()를 포함하고 있지 않으므로 오류가 발생한다.
    - 이를 해결하기 위해서는 클래스 B에 생성자를 직접 작성하고 첫 줄에 super(3)과 같이 정수를 입력받는 부모의 생성자를 명시적으로 호출해야 한다.

    ```java
    class A {
       A() {
           System.out.println("A 생성자");
      }
    }
    
    class B extends A {
      B() {
           super();       // 생략했을 때 컴파일러가 자동 추가(부모 클래스의 생성자 호출)
           System.out.println("B 생성자");
        }
    }
    
    class C {
       C(int a) {
           System.put.println("C 생성자");
        }
    }
    
    class D extends C {
      /* 컴파일러가 자동으로 추가해 주는 내용
       D(){
          super();
     }
      */
        D() {
            super(3);
         }
    }
    
    public clas SuperMethod_1 {
       public static void main(String[] args) {
            // A 객체 생성
            A aa = new A();
            System.out.println();
    
            // B 객체 생성
            B bb = new B();
         }
    }
    
    /* 결과
    A 생성자
    
    A 생성자
    B 생성자
    */
    ```

    ```java
    /* this 메서드와 super() 메서드의 혼용 */
    
    class A {
       A() {
           this(3);
           System.out.println("A 생성자 1");
       }
       A(int a) {
            System.out.println("A 생성자 2");
       }
    }
    
    class B extends A {
        B() {
           this(3);
           System.out.println("B 생성자 1");
       }
       B(int a) {
            System.out.println("B 생성자 2");
       }
    }
    
    public class SuperMethod_2 {
         //  A 객체 생성 
         A aa1 = new A();
         System.out.println();
         A aa = new A(3);
         System.out.println();
    
         // B 객체 생성
         B bb1 = new B();
         System.out.println();
         B bb2 = new B(3);
       }
    }
    
    /* 결과
    A 생성자 2
    A 생성자 1
    
    A 생성자 2
    
    A 생성자 2
    A 생성자 1
    B 생성자 2
    B 생성자 1
    
    A 생성자 2
    A 생성자 1
    B 생성자 2
    */
    ```