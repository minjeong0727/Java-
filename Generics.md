# ✏️지네릭스란? 


### 1️⃣ 정의
지네릭스는 다양한 타입의 객체들을 다루는 메서드나 컬렉션 클래스에 컴파일 시의 타입체크를 해주는 기능이다.

### 2️⃣ 왜 사용하는가?
- 클래스 내부에서 특정(Specific)타입을 미리 지정해주는 것이 아닌 사용자 필요에 의해 지정할 수 있는 일반(Generic)타입이기 때문이다.
- 정확히 말하자면 원하는 타입의 경계를 미리 명시해줌으로써 타입체크를 해주고, 형변환을 줄여준다.
- 지네릭스의 장점
  - 타입 안전성을 제공한다.
  - 타입체크와 형변환을 생략할 수 있으므로 코드가 간결해 진다.
  - 코드의 재사용성이 높아진다.

### 3️⃣ 사용방법

```
  public class ClassName <T, K> { ... }
   
  public class Main {
  	public static void main(String[] args) {
  		ClassName<String, Integer> a = new ClassName<String, Integer>();
  	}
  }

```

**타입	설명**
|코드    | 설명 | 
|----- | ------ |
| `<T>` | Type    |
| `<E>` | Element |
| `<K>` | Key     |
| `<V>` | Value   |
| `<N>` | Number  |


-> 기호의 종류만 다를 뿐 '임의의 참조형 타입'을 의미하는 것이다.

**📍주의사항: static에서는 지네릭스를 사용할 수 없다**

지네릭스는 객체를 생성할때 객체별로 다른 타입을 지정하는 것은 적절하다.

왜냐하면 지네릭스의 목적이 인스턴스별로 각자 타입을 지정해 다르게 동작하려고 만든 기능이기 때문이다.

따라서, 모든 객체에 동일하게 동작해야하는 static멤버에 타입 변수 T를 사용할 수 없다.
T는 인스턴스 변수로 간주되기때문이다!!!!(static멤버는 인스턴스변수를 참조할 수 없음)



### 4️⃣ 제한된 지네릭 클래스(와일드 카드)
이제까지는 지네릭의 타입을 T로 지정하여 참조타입으로 만들었다. 
그런데 만약 특정 범위 내로 경계선을 만들어 타입의 종류를제한하고 싶으면 어떻게 할까?

-> 이때 필요한것이 extends와 super, 그리고 ?(물음표)와일드카드다.

#### 1. 와일드 카드란?
    - <?> : 제한이 없는 모든 타입을 뜻한다. 따라서 '?'만으로는 Object타입과 다를게 없으므로 경계값을 지정해 주어야한다.
    - 그 경계선을 지정해주는 것이 extends와 super다.

#### 2. extends와 super
    - <? extends T> : 와일드카드의 상한 제한, 
    - <? super T> : 와일드카드의 하한 제한

```
<K extends T>	// T와 T의 자손 타입만 가능 (K는 들어오는 타입으로 지정 됨)
<K super T>	// T와 T의 부모(조상) 타입만 가능 (K는 들어오는 타입으로 지정 됨)
 
<? extends T>	// T와 T의 자손 타입만 가능
<? super T>	// T와 T의 부모(조상) 타입만 가능
<?>		// 모든 타입 가능. <? extends Object>랑 같은 의미


```    

**📍 주의점: < K extends T > 와 < ? extends T > 는 다르다.**

-> 유형경계를 지정하는 것은 같지만 K는 특정 타입으로 지정이 되지만 , ? 는 타입이 지정되지 않는다는 의미다.


```
/*
 * Number와 이를 상속하는 Integer, Short, Double, Long 등의
 * 타입이 지정될 수 있으며, 객체 혹은 메소드를 호출 할 경우 K는
 * 지정된 타입으로 변환이 된다.
 */
<K extends Number>
 
 
/*
 * Number와 이를 상속하는 Integer, Short, Double, Long 등의
 * 타입이 지정될 수 있으며, 객체 혹은 메소드를 호출 할 경우 지정 되는 타입이 없어
 * 타입 참조를 할 수는 없다.
 */
<? extends T>	// T와 T의 자손 타입만 가능

```    

-> 특정 타입의 데이터를 조작하고자 하는 경우에는 K같이 특정 제네릭 인수로 지정을 해주어야 한다.



예)

![JPEG 이미지-47F7-B3B6-F0-0](https://github.com/minjeong0727/Java-/assets/174947594/e14d4c65-60af-4472-acb7-f0567877d4ba)


상한과 하한그림을 나타낸 것이다.

만약, 
![image](https://github.com/minjeong0727/Java-/assets/174947594/8a5c2e6d-7385-4c5a-8fd4-ce429af9f93f)

이렇게 상속 관계를 갖는다면

 

1. <K extends T>, <? extends T>

이 것은 T 타입을 포함한 자식(자손) 타입만 가능하다는 의미

```
<T extends B>	// B와 C타입만 올 수 있음
<T extends E>	// E타입만 올 수 있음
<T extends A>	// A, B, C, D, E 타입이 올 수 있음
 
<? extends B>	// B와 C타입만 올 수 있음
<? extends E>	// E타입만 올 수 있음
<? extends A>	// A, B, C, D, E 타입이 올 수 있음


```   

 

2. <K super T>, <? super T>

이 것은 T 타입의 부모(조상) 타입만 가능하다는 의미




```   
<K super B>	// B와 A타입만 올 수 있음
<K super E>	// E, D, A타입만 올 수 있음
<K super A>	// A타입만 올 수 있음
 
<? super B>	// B와 A타입만 올 수 있음
<? super E>	// E, D, A타입만 올 수 있음
<? super A>	// A타입만 올 수 있음




```   

---

# 📚이펙티브 자바 _5장.지네릭스

### item26. Raw 타입은 사용하지 말라
- 클래스와 인터페이스의 선언에 타입 매개변수가 쓰이면 이를 지네릭 클래스 혹은 지네릭 인터페이스라고 한다.
예를 들어 List인터페이스 List<E>는 원소의 타입을 나타내는 타입 매개변수 E를 받는다.

- 지네릭타입은 매개변수화 타입을 정의해주어야한다. 매개변수화 타입은 지네릭 타입에 실제 타입을 지정한 것으로 'List<String>'을 뜻한다.
  
- 만약 지네릭 타입을 사용할 때 타입 매개변수를 정의하지 않으면 지네릭 타입은 Raw Type이 되는데 예를 들어 'List', 이것이 문제가 될 수 있다.

  **왜 Raw타입을 사용하면 안되는가?**
  - Raw 타입을 사용하면 컴파일러가 타입 체크를 할 수 없다. 예를 들어 'List'에 'String'과 'Integer'를 섞어 넣어도 컴파일러가 오류를 잡아주지 않는다.
  - 반면,'List<Integer>'처럼 타입을 명시하면 컴파일 시점에 잘못된 타입이 들어가는 것을 막을 수 있다.
  - 따라서 지네릭 타입을 사용할때는 항상 타입 매개변수를 지정하여 타입 안전성을 확보하고(타입 변환 불필요), 컴파일 시점에 오류를 잡을 수 있도록 하자!!!

- 추가 설명
  > ### 지네릭 타입의 구분
  > 1. 매개변수화 타입(Parameterized Type): 타입 매개변수를 지정한 지네릭 타입이다.
  >    <pre><code>List<String> stringList = new ArrayList<>();</code></pre>
  >   
  > 2. Raw타입(Raw Type): 타입 매개변수를 지정하지 않은 지네릭 타입
  >    <pre><code>List rawList = new ArrayList();</code></pre>
  >
  > ### Raw 타입을 쓰면 안되는 이유
  > 1. 컴파일 시 타입 체크 불가
  >    
  > Raw 타입을 사용하면 컴파일러가 타입 체크를 할 수 없습니다. 따라서 잘못된 타입의 객체를 추가하더라도 컴파일러가 이를 잡아내지 못합니다.
  >  
  >  <pre><code>
  >  List rawList = new ArrayList();
  >  rawList.add("Hello");
  >  rawList.add(123);  // 컴파일러가 오류를 잡아내지 못함
  > </code> </pre>  
  >
  >  2. 런타임 오류 발생 가능
  >     
  >  Raw 타입을 사용하면 런타임에 ClassCastException이 발생할 수 있습니다. 이는 프로그램의 안정성을 저해하고, 예기치 않은 오류를 발생시킬 수 있습니다.
  >  <pre><code>
  >  List rawList = new ArrayList();
  >  rawList.add("Hello");
  >  rawList.add(123);
  >  
  >  String str = (String) rawList.get(0);  // 정상
  >  Integer num = (Integer) rawList.get(1);  // 정상
  >  String anotherStr = (String) rawList.get(1);  // ClassCastException 발생
  ></code></pre>  
  > 3. 코드 가독성 및 유지보수성 저하
  >
  >  Raw 타입을 사용하면 코드의 의도가 불명확해지고, 유지보수가 어려워집니다. 매개변수화 타입을 사용하면 코드의 의도를 명확하게 전달할 수 있습니다.
  >  
  > <pre><code>
  >  List<String> stringList = new ArrayList<>();
  >  stringList.add("Hello");
  > // stringList.add(123);  // 컴파일 오류 발생
  >  </code></pre>


### item27. 비검사 경고를 제거하라

### item28. 배열보다는 리스트를 사용하라


#### 배열은 공변이지만 지네릭인 리스트는 불공변이다.
- 배열의 공변성
  - 공변성이란, 한 타입의 배열이 다른 타입의 배열로 간주될 수 있다는 의미다. 예를 들어 'Long[]'배열은  'Object[]' 배열로 취급될 수있다는 것이다.
  - 이로 인해 런타임 오류가 발생할 수 있다.

  <pre><code>
    Object[] array = new Long[1];
    array[0] = "efwaf"; // 런타임 오류 발생
  </code></pre>
  
  -> 'Long[]'배열을 'Object[]'배열로 취급했기 때문에 컴파일은 성공하지만, 문자열 "efwaf"를 넣으려고 하면 런타임 오류가 발생한다.->잘못된 오류
 - 지네릭 리스트의 불공변성
   - 불공변성이란 한 타입의 리스트가 다른 타입의 리스트로 취급될 수 없음을 의미한다. 예를 들어 'List<Long>'는 'List<Object>'로 간주될 수 없음을 의미한다.
   - 이로 인해 컴파일 오류가 발생한다.

```
  List<Object> list = new ArrayList<Long>();  // 컴파일 오류 발생
list.add("타입이 달라 넣을 수 없다.");

```



#### 배열은 실체화된다.
- 배열 런타임에 타입을 검사하지만, 지네릭 리스트는 컴파일 시점에 타입을 검사하여 런타임 오류를 줄일 수 있다.
 - 배열의 실체화: 배열은 런타임 시점에 자신이 담을 수 있는 타입을 검사한다. 예를 들어, 'String[]'배열은 오직 'String'타입의 요소만 담을 수 있다.
 - 지네릭의 타입 소거 : 지네릭은 컴파일 시점에 타입 정보를 검사하고, 런타임 시점에는 타입 정보가 소거된다. 즉, 런타임에는 타입 정보가 사라지기 때문에 런타임 오류를 줄일 수 있다. 





























