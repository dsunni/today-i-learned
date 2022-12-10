# 5장~7장

# 리터럴과 메모리

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e7a10f55-83fb-415e-a671-a62ba61da668/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221210%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221210T122406Z&X-Amz-Expires=86400&X-Amz-Signature=addd874e838d477e253e6bc19687c45bc7b8d592cf627494a19f79c576c9fecd&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

## 리터럴이란?

```java
int a = 10; // 리터럴.
int b = 10;
```

- 리터럴이란 변하지 않는 데이터 그 자체, 쉽게 상수를 말한다.
- 리터럴의 종류에는 원시타입과 String이 있다.

<br>

## 리터럴과 Heap 메모리

- 출처 : [https://yoo11052.tistory.com/50](https://yoo11052.tistory.com/50)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b331e6c9-e8a3-4117-b179-b739b0961f42/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221210%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221210T122602Z&X-Amz-Expires=86400&X-Amz-Signature=42ef7b0d6694961a6fcca57a384d89f43b0b1cc98b32a9f7517b5e50024d0c3c&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6964754d-d0b9-4e24-9366-50343fa27c30/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221210%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221210T122611Z&X-Amz-Expires=86400&X-Amz-Signature=26fc1fd3c6977959b9604ea57e1c41fbbdaa7f7fb6b981ab3df28489d6d2d78f&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- 10이라는 값을 **Heap** 메모리의 **Constant Pool**이라는 메모리 영역에 할당함
- 똑같은 값을 또 호출했을 때 새로운 메모리를 할당하지 않고 전에 할당했던 메모리 주소를 넘겨주게됨
  - a == b가 true인 이유도 a와 b가 똑같은 메모리 주소를 가리키고 있기 때문

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a095847e-91fc-4434-a2ed-bdc14eec5bb4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221210%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221210T122633Z&X-Amz-Expires=86400&X-Amz-Signature=200bbe8001f17c4bbc22b60ec49601e0c7f9430f5352b877f31150a9a436dec0&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- `String` 의 경우 따로 관리하고 있는 String Constant Pool 영역에 할당함

<br>

## 접미사 L(long), F(float)의 의미

- 문자열 리터럴을 제외하고 byte, short, int, long, float, double, boolean, char 리터럴은 **스택**이라는 특정한 메모리 공간에 일시적으로 적재된 후 변수라는 메모리 공간에 저장됨

### 1) 정수형 데이터

- 정수형 데이터는 약 21억이 넘어가는 크기가 아닌 이상 그 이하의 수는 **기본적으로 4 byte** 크기로 스택 메모리 공간에 적재됨
- 21억 이상의 리터럴 값은 큰 수를 표현하기 위해 8 byte 크기의 메모리 공간이 필요
- JVM에게 4byte가 아닌 **8byte의 메모리 공간을 할당**해달라고 명시하기 위해 `접미사 L`을 작성함
  - long n = 100000000000L

<br>

### 2) 실수형 데이터

- 실수형 데이터는 기본적으로 8yte 크기로 스택 메모리 공간에 적재됨 (4byte를 두개로 나눠서 저장)
- 그러나 4 byte로 표현하는 실수형 리터럴은 JVM에게 8 byte가 아닌 **4 byte 크기의 메모리 공간을 할당**해달라고 명시하기 위해 `접미사 F`를 작성함
  - float a = 10.231;

<br>

<br> 

# 5장. 계산을 하고 싶어요

## 형 변환 (Casting)

- 형변환이란 서로 다른 타입 사이에 변환하는 작업을 하는 것을 말한다.
- 기본 자료형, 참조 자료형 모두 형변환 가능
  - 기본 자료형 중 boolean 타입만 형변환 불가능
- 형 변환에는 암시적 형 변환(Implicit Conversion)과 명시적 형 변환 (Explicit Conversion)

<br>

### 암시적 형변환 (Implicit Conversion)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b8647f28-831a-48d1-a17d-af2b558336e9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221210%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221210T122743Z&X-Amz-Expires=86400&X-Amz-Signature=f4a5a236c8ffe7852265f3ead23479c3832d59d8723a9893a2d5a257a80aad40&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

```java
byte a = 12;

// 1 byte -> 2 byte
short b = a;

// 2 byte -> 4 byte
int c = b;

// 4 byte -> 8 byte
long d = c;

float a = 1.12F;
// 4 byte -> 8 byte
double b = a;
```

- 형 변환 접두사를 사용하지 않아도 자동적으로 형 변환되는 것을 말함
- **더 큰 범위의 자료형으로 변환**하기 때문에 표현할 수 있는 값의 범위에 대한 제약이 없음
- 메모리 공간 크기 기준이 아니라 **값의 표현 범위 기준으로 변환됨**

<br>

### 명시적 형변환 (Explicit Conversion)

```java
int a = (int) 100000000000L;

long b = 1000;
int a = (int) b;

float a = 32.123F;
int b = (int) a;
```

- **더 작은 범위의 자료형으로 변환 시 데이터 손실이 발생** 가능한 것을 인지하고 **형 변환을 한다고 명시**함
- 정수 → 실수로 명시적 형 변환을 할 경우에 int 범위를 넘지 않는 이상 정수 부문만 추출함. 만약 정수 범위를 넘으면 데이터가 변질됨

<br>

<br>

# 7장. 여러 데이터를 하나에 넣을 수는 없을까요?

## 배열이란?

```java
int[] intArr = new int[7];
```

- 배열은 **한가지 타입**에 대해서 **하나의 변수에 여러 개의 데이터를 넣을 수 있는 자료구조**이다.
- 배열도 **참조 자료형**이기 때문에 신규로 생성시 new 키워드를 붙여야함
- 배열 **초기화**시 **배열의 크기와 값을 지정**해 주어야함
  - 값을 초기화하지 않은 참조 자료형은 null이 됨

<br>

## 배열을 출력하면 어떻게 나올까?

```java
System.out.println(new String[0]); // [Ljava.lang.String;@1412ed
```

- `[L` : 가장 앞의 `[` 는 해당 객체가 배열이라는 의미이며 `L` 은 해당 배열은 참조 자료형이라는 의미이다.
- `java.lang.String`  : 어떤 타입의 배열인지 알려줌

<br>

## 2차원 배열

```java
arr = new int[2][];
```

- 2차원 배열 arr[][]에서 arr[0]은 int 배열, arr[0][0]은 int 값을 의미한다.

<br>

## 자바 main() 메소드의 String[] args

```java
public static void main(String[] args) {
    // main method
}

// main method에 a b c d 라는 파라미터를 String[] args로 받는다.
$ java ArrayMain a b c d 
```

- 자바 main() 메소드에 파라미터를 넘겨주고 싶으면 자바 실행시 넘겨주면 된다.