# 8장-9장

# 8장. 참조 자료형에 대해서 더 자세히 알아봅시다

## 참조 자료형이란?

- 참조 자료형이란 기본 자료형 8가지를 제외한 나머지 모든 타입을 말한다.
  - 기본 자료형 8가지 : byte, short, int, long, float, double, char, boolean
- 참조 자료형과 기본 자료형의 가장 큰 차이는 **new를 사용해 객체를 생성하는지** 여부이다. new 객체 없이도 객체를 생성할 수 있는 참조 자료형은 오로지 `String` 뿐이다.

<br>

## 기본 생성자란? (Default Constructor)

```java
public class ReferenceDefault {
    public static void main(Stirng[] args) {
        ReferenceDefault reference = new ReferenceDefault (); //기본 생성
    }
}
```

- 기본 생성자는 **생성자가 없는 클래스가 컴파일될 때 자동으로 만들어지는 생성자**이다.
- **다른 생성자가 있으면 기본 생성자는 만들어지지 않는다.**
  - actual and formal argument lists differ in length라는 컴파일 오류 발생

<br>

## 생성자는 왜 필요할까?

- 자바의 생성자는 자바 클래스의 **객체(또는 인스턴스)를 생성**하기 위해 존재한다.

<br>

## 생성자에 왜 리턴타입이 없을까?

- **생성자의 리턴 타입은 클래스의 객체**이기 때문이다.
- 생성자는 클래스와 이름이 동일해야 컴파일러가 생성자라고 인식할 수 있다.

<br>

## 생성자는 어디에 선언하는 것이 좋을까?

```java
public class ReferenceString {
    String instanceVariable; // 인스턴스 변수
    public ReferenceString () {} // 생성자
    public ReferenceString (String args) {}

    public String getString() {
        return instanceVariable; // 메소드
    }
}
```

- 생성자는 클래스에서 다른 메소드보다 위에, 가장 윗부분에 선언하는 것이 좋다.
- 보통 클래스 내부에서 **1) 인스턴스 변수**를 선언한 후에 **2) 생성자**를 선언하고 **3) 나머지 메소드**들을 선언하는 것이 암묵적인 규칙이다.

<br>

## DTO, VO란?

### DTO (Data Transfer Object)

- 다른 **서버에 전달하기 위한 목적**으로 만들어진 어떠한 **속성을 갖는 클래스**
- DTO는 VO를 포함하는 개념

<br>

### DTO의 장점

- 자바에서 메소드의 리턴 타입은 한 가지만 선언할 수 있다. 이 때 DTO를 사용하면 DTO의 객체를 리턴해줌 DTO의 객체를 리턴해줌으로써 **복합적인 데이터리턴 가능**
- 왜 배열은 적합하지 않을까?
  - 배열, 문자열 등 서로 다른 타입을 한꺼번에 리턴하기엔 배열은 적절치 않음

<br>

### VO (Value Object)

- DTO와 형태는 동일하지만, VO는 **데이터를 담아두기 위한 목적**으로 사용됨.

<br>

## 생성자가 여러개일 때의 장점은?

```java
public class MemberDTO {
    public String name;
    public String phone;
    public String email;

    public MemberDTO() {
           // 아무 정보도 모를 때
    }

    public MemberDTO(String name) {
        // 이름만 알 때
    }

    public MemberDTO(String name, String phone, String email) {
        this.name = name;
        this.phone = phone;
        this.email = email;
    }
}
```

- 서로 다른 매개변수의 생성사를 통해 **다양한 상황에서 유동적이게 객체를 생성**할 수 있다는 장점이 있다.
- 예를 들어 회원DTO를 만들 때 아무런 정보도 모를 때, 이름만 알때 또는 이름과 전화번호를 알 때 등 각각의 상황에 맞는 객체를 생성할 수 있다.

<br>

## this 예약어란?

- 객체의 변수와 매개 변수의 이름이 동일할 때, this 예약어는 **객체의 변수와 매개 변수를 구분**하기 위해 사용한다.
  - 자바 컴파일러와 개발자에게 어떤 변수를 지정하는지 알려주기 위해 사용(객체의 변수)
- `this.name` == "**이 객체**의 name이라는 변수"

<br>

## Method Overloading이란?

- 메소드 오버로딩이란 **메소드의 이름을 같도록 하고 매개 변수만 다르게 하는 것**을 말한다.
- **하나의 메소드 이름**을 사용하면서 **여러 기능을 제공**한다.

<br>

### Method Overloading의 장점은?

- 하나의 메소드 이름만 기억하면 되므로 오류의 가능성을 많이 줄일 수 있다.
- 코드를 봤을 때 메서드의 이름이 같으면 같은 기능을 하겠구나라고 쉽게 예측이 가능하다.
- 매개변수에 따라 매번 다른 메소드를 호출하지 않아도 된다.
- `"같은 역할을 하는 메소드는 같은 메소드 이름을 가져야 한다."`는 모토로 사용함
- 예시 ) System.out.println
  - int, string, char 등 어떤 타입을 출력해도 항상 똑같은 메서드명 사용

<br>

## 자바에서 메소드가 종료되는 조건은?

- 메소드의 모든 문장이 실행됐을 때
- return 문장에 도달했을 때
- 예외가 발생(throw)했을 때

<br>

## static 메소드란?

- static 메소드는 **객체를 생성하지 않고 바로 호출할 수 있는 메서드**이다.

<br>

## static 메소드는 클래스 변수만 사용할 수 있다.

```java
public class Test {
    String name = "Suna"; // 인스턴스 변수

    public static void staticMethod() {
        System.out.pritln(name); // ERROR!
    }
}
```

- static 메소드는 앞에 **static 키워드가 붙은 클래스 변수**만 사용할 수 있다.
- 만약 static 메소드 안에서 **인스턴스 변수**를 호출하면 **"non-static variable name cannot be referenced from a static context"**라는 에러 메시지가 출력된다.
- 해결 방법은 1) static Method에서 static 키워드를 빼거나, 2) 인스턴스 변수를 static으로 선언해야 한다.
- 하지만 2번 방법은 조심해야 한다. **클래스 변수가 되면, 모든 객체에서는 하나의 값을 바라본다**.

<br>

## 클래스 변수는 모든 객체에서 하나의 값을 바라본다.

```java
public class Test {
    static String name;
    public class Test(String name) {
            this.name = name;
    }

    public static void staticMethod() {
        Test test1 = new Test("one");
        Test test2 = new Test("two");

        System.out.println(test1.name); // one
        System.out.println(test1.name); // two
    }
}
```

- name 변수가 static으로 선언한 클래스 변수이기 때문에 위 코드를 실행시키면 one, two가 출력된다.

<br>

## static 블록이란?

```java
public class StaticBlock {
    static int data=1;
    public StaticBlock() {}

    static {
        System.out.println("Static Block 1");
    }

    static {
        System.out.println("Static Block 2");
    }
}
```

- **객체가 생성되면서 딱 한 번만 호출**되어야 하는 코드가 있을 때 사용함
  - 객체가 생성되기 전에 딱 한 번만 호출되고, 이후에는 호출되지 않음
  - 클래스에 대한 참조가 발생하자마자 호출됨
- **클래스 내에 선언**되어 있어야 하며, **메소드 내에서는 선언할 수 없음**
- static 블록은 **여러 개**를 선언할 수 있으며 **선언된 순서**대로 블록들이 차례대로 호출됨
- **생성자가 호출되기 전에 static 블록들이 호출됨**
- static 블록 내에서는 **static한 것들만 호출할 수 있음**

<br>

## Pass By Value, Pass By Reference

### Pass By Value

- 메소드의 매개변수로 전달되는 모든 **기본 자료형**은 Pass By Value이다.
- Pass By Value는 **값을 전달**하는 작업이고, **호출되기 전과 후에 데이터가 변경되지 않는다**.
- 참조 자료형인 String 또한 매개변수로 전달해도 기존 값이 변경되지 않는다.
  - `str = “변경된 값”` 과 같이 따옴표로 값을 할당하면 new를 사용해 **새로운 객체를 생성**하는 것과 같기 때문
  - 다른 참조 자료형들도 호출된 메소드에서 새로운 객체를 생성하여 처리하면 기존 값이 바뀌지 않는다.

<br>

### Pass By Reference

- **참조 자료형**은 값이 아닌 **객체에 대한 참조(Reference)가 전달**되는 Pass By Reference이다.
- 메소드의 매개변수로 참조 자료형을 넘길 경우에는 메소드 안에서 **객체의 상태를 변경한 결과에 영향을 받는다.**

<br>

## 자바의 임의 개수의 매개변수 (Arbitrary Number Of Arguments)

```java
public class MethodVarargs {
    public static void main(String args[]) {
        MethodVarargs args = new MethodVarargs ();
        test(1,2,3,4,5);
    }

    public void test(int...numbers){
        // numbers를 배열로 인식.
    }
}
```

- `타입... 변수명`
- **매개 변수의 개수가 정확하지 않을 때 사**용됨
  - ex) printf 함수
- 하나의 메소드에서 **한 번만 사용 가능**하고 여러 매개변수가 있다면 **가장 마지막에 선언**해야 함

<br>

<br>

# 9장. 자바를 배우면 패키지와 접근 제어자는 꼭 알아야 해요.

## 패키지란?

- 클래스를 구분하는 폴더와 비슷한 개념

<br>

## 패키지 이름 규칙

### java

- 자바 기본 패키지

### javax

- 자바 확장 패키지

### org

- 일반적으로 비영리단체 (오픈소스) 패키지

### com

- 일반적으로 영리단체 (회사) 패키지

<br>

## import 예약어란

- **다른 패키지**에 있는 클래스를 찾기 위해 사용하는 예약어

<br>

## import static이란

```java
import static c.javapackage.sub.SubStatic.subStaticMethod;

public class PackageStatic {
    public sttaic void main(String[] args) {
        subStaticMethod();
    }
}
```

- **static한 변수(클래스변수)와 static 메소드**를 사용할 때 용이
- import static로 static한 변수나 메소드를 지정하면 **클래스 이름을 지정하지 않아도 사용**할 수 있다.
- 만약 자신의 클래스에 중복된 static method, class가 있다면 **자신의 클래스의 method, class가 우선**이다.

<br>

## import하지 않아도 사용 가능한 패키지는?

### java.lang 패키지

- String, System 클래스

### 같은 패키지

<br>

<br>

## 자바의 4가지 접근제어자는?

```java
public class AccessModifier {
        public void publicMethod() {}
        protected void protectedMethod() {}
        void defaultMethod() {}
        private void privateMethod() {}
}
```

### public

- 누구나 접근 가능

### protected

- **같은 패키지** 내 또는 **상속받은 경우**에만 접근 가능

### default (package-private)

- 아무런 접근제어자를 적지 않을 때 붙는 디폴트 접근제어자
- **같은 패키지** 내에서만 접근 가능

### private

- **해당 클래스** 내에서만 접근 가능

<br>

## 접근제어자는 왜 사용할까?

- 구현한 메소드를 **다른 개발자들이 마음대로 호출하면 안 될 경우** 접근제어자로 통제 가능
- 예를 들어 **변수**의 경우 직접적으로 접근해서 변수를 변경하지 못하게 하고 꼭 **메소드를 통해서만 변경 혹은 조회만 가능하게 구현**할 때 사용한다.
  - 변수 - private
  - 조회/변경 메서드 - public

<br>

## 클래스 접근 제어자 선언시 유의점

```java
public class FirstPublic {

}

public class SecondPublic {

}
```

- 위 코드는 컴파일 에러가 난다. “class SecondPublic is public, should be declared in a file named SecondPublic.java”
- **public으로 선언된 클래스**가 소스 내에 있다면, 그 **소스 파일의 이름은 public인 클래스 이름과 동일**해야 한다.