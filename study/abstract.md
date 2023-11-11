(Do it! 자바 완전 정복 11장 자바 제어자2)
## abstract 제어자
- abstract: 추상적인
- "추상적": 구체적이지 않다.
- 상 메서드: 중괄호가 없는 메서드로 ```abstract 리턴 타입 메서드명 ();``` 형태이다.
### 일반 클래스와 비교
```java
/**일반 클래스를 상속해 오버라이딩 수행*/
class Animal {
    void cry() {}
}
class Cat extends Animal {
    void cry() {
        System.out.println("야옹");
    }
}
class Dog extends Animal {
    void cry() {
        System.out.println("멍멍");
    }
}
public class AbstractModifier_1 {
    public static void main(String[] args) {
        // 객체 생성
        Animal animal1 = new Cat();
        Animal animal2 = new Dog();
        
        // 메서드 호출
        animal1.cry();  // 야옹
        animal2.cry();  // 멍멍
    }
}
```
- Animal 클래스 내의 cry() 메서드가 아무런 기능을 수행하지 않는다면, 즉 중괄호 안을 비워둘 것이라면 중괄호 자체가 없는 미완성 메서드인 추상 메서드로 정의하는 것이 효율적이다. 
- 추상 메서드를 1개 이상 포함하고 있는 클래스는 반드시 추상 클래스로 정의해야 한다. 즉, Animal클래스의 cry()메서드를 추상 메서드로 바꾸면 Animal 클래스는 반드시 추상 클래스여야 한다.
```java
/**추상 클래스와 추상 메서드*/
abstract class Animal {
    abstract void cry();
}
class Cat extends Animal {
    void cry() {
        System.out.println("야옹");
    }
}
class Dog extends Animal {
    void cry() {
        System.out.println("멍멍");
    }
}
public class AbstractModifier_2 {
    public static void main(String[] args) {
        // 객체 생성
        Animal animal1 = new Cat();
        Animal animal2 = new Dog();

        // 메서드 호출
        animal1.cry();  // 야옹
        animal2.cry();  // 멍멍
    }
```

### abstract 제어자의 장점: 문법 오류를 잡아줄 수 있다.
```java
/**일반 클래스로 정의*/
class Animal {
    void cry() {}
}
class Cat extends Animal {
    void cRy() {            // 오타 발생
        System.out.println("야옹");
    }
}
```
```java
Animal animal1 = new Cat(); 
animal1.cry();          // 출력 없음
```
- 일반 클래스로 정의시 아무런 출력값도 발생하지 않는다. 오타로 인해서 본래 목적이었던 오버라이딩이 되지 않고 cRy()라는 새로운 메서드가 정의되었다.
```java
/**추상 클래스로 정의*/
abstract class Animal {
    abstract void cry();
}
class Cat extends Animal { 
    void cRy() {             // 오타 발생 ➡️ 오류 발생
        System.out.println("야옹"); 
    }                 
}            
```
- 추상 클래스의 경우는 오타 발생으로 인해 오류가 발생했다.
- 클래스 내부에 추상 메서드가 1개라도 있다면, 해당 클래스는 추상 메서드를 일반 메서드로 오버라이딩하거나 자신을 추상 클래스로 정의하여아 한다.
- Cat 클래스는 오버라이딩도 하지 않고, 자신을 추상 클래스로 정의하지 않았으므로 오류가 발생한다.
- 만일 acb()라는 추상 메서드를 포함하고 있는 추상 클래스가 있을 때 '이를 상속한 모든 자식 클래스 내부에는 항상 abc() 메서드가 정의되어 있다'는 것이 보장된다.

