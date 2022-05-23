# [Java] Optional Class



### NullPointerException(NPE)

개발을 하다보면 자주 접할 수 있는 예외중 하나이다.

이를 피하기 위해서는 해당 객체가 null인지 검사하는 로직을 추가해야하는데 null 검사를 해야하는 변수가 많은 경우 코드가 복잡해지고 로직이 상당히 번거롭다. 

그래서 null 대신 초기값을 사용하기도 한다.

```java
List<String> list = someInstance.getList();	// null
if(list != null){
    list.sort();
}
```

<br>



## Optional이란?

Java8에서는 Optional\<T\> 클래스를 사용해 NullPointerException을 방지할 수 있도록 도와준다.

Optional\<T\>는 null이 올 수 있는 값을 감싸는 Wrapper클래스로, 참조하더라도 NPE가 발생하지 않도록 도와준다.

```java
public final class Optional<T> { 
    // If non-null, the value; if null, indicates no value is present 
    private final T value;
    
    ... 
}
```

이처럼 Optional 클래스는 value에 값을 저장하기 때문에 value가 null이더라도 바로 NPE가 발생하지 않으며 추가로 활용할 수 있는 각종 메서드를 제공해준다.

<br>



### Optional.empty()

Optional 클래스는 내부에 static변수로 EMPTY 객체를 미리 생성해서 가지고 있다.

이를 활용하면 빈 객체를 여러번 생성해줘야 하는 경우에도 1개의 EMPTY객체를 공유하여 메모리를 절약할 수 있다.

``` java
public final class Optional<T> { 
    
    private static final Optional<?> EMPTY = new Optional<>();
    private final T value;
    
    private Optional() { this.value = null; }
    
    ...
}

// 활용법
Optional<SomeClass> optional = Optional.empty();
```

<br>



### Optional.of()

만약 어떤 데이터가 null이 절대 아니라면 Optional.of()로 Optional객체를 생성할 수 있다.

```java
Optional<String> optional = Optional.of("it's Not Null");
```

Optional.of()로 null인 값을 저장하려고 하면 NPE가 발생한다.

<br>

### Optional.ofNullable()

값이 null일 수도 있는 값을 저장하는 경우에는 Optional.ofNullable()로 Optional객체를 생성할 수 있다.

이후 값을 가져와야 하는 경우 orElse() 또는 orElseGet() 메서드를 이용해 값이 없는 경우라도 안전하게 값을 가져올 수 있다.

```java
Optional<String> optional = Optional.ofNullable(someMethod());
String data = optional.orElse("anonymouse") // 값이 없다면 annonymouse를 리턴하라는 뜻.
```

<br>



#### orElse() vs orElseGet()

orElse()는 null일 때 대체할 파라미터를 받는다.

orElseGet()은 null일 때 대체할 함수형 인터페이스를 받는다.

둘의 차이는 orElse의 파라미터로 리턴값이 존재하는 함수일 때 확연하게 보여진다.

```java
...orElse(getSomething()); // getSomething을 실행하게 된다.
...orElseGet(this::getSomething); // getSomething을 실행하지 않는다.
```

따라서, orElse는 null일 때 대체할 값이 미리 존재하는 경우가 아니라면 사용을 피하는 것이 좋다.

<br>



## 활용 예

```java
List<String> list = Optional.ofNullable(someInstance.getList())
    						.orElseGet(() -> new ArrayList<>());
// getList()가 null이라면 새로운 ArrayList를 만들어 넣어준다.
```

<br>

User객체가 가진 Address객체에서 postcode를 찾고자 할 때

```java
// Optional을 사용하지 않는다면
public String findPostCode(){
    User user = someInstance.getUser();
    if(user != null){
        Address addr = user.getAddress();
        if(addr != null){
            String postCode = addr.getPostCode();
            if(postCode != null)
                return postCode;
        }
    }
    
    return "우편번호 없음";
}

// Optional 사용
public String findPostCode(){
    Optional<User> user = Optional.ofNullable(someInstance.getUser());
    Optional<Address> addr = user.map(User::getAddress);
    Optional<String> postCode = addr.map(Address::getPostCode);
    
    return postCode.orElse("우편번호 없음");
}

// 축약해서 한번에 사용한다면
public String findPostCode(){
    Optionam<User> user = Optional.ofNullable(someInstance.getUser());
    
    return user.map(User::getAddress).map(Address::getPostCode).orElse("우편번호 없음");
}
```

<br>

### Optional.orElseThrow()

만약 값이 null일 때 예외처리를 하고 싶다면 orElseThrow() 메서드를 사용하면 된다.

```java
Optional<String> data = Optional.ofNullable(someInstance.getData());
String result = data.orElseThrow(CustomException::new).someMethod();
```

<br>



### 올바른 Optional 사용 가이드

* Optional 변수에 Null을 할당하지 않을 것.
* 값이 없을 땐 Optional.orElseX()로 기본 값을 반환할 것
* 단순히 값을 얻으려는 목적으로 Optional을 사용하지 않을 것.
* 생성자, Xetter(), 메서드 파라미터 등으로 Optional을 사용하지 말 것
* Collection의 경우 Optional을 사용하지 말고 빈 Collection으로 처리할 것.
* 반환 타입으로만 사용할 것.



## 정리

Optional 클래스는 null 또는 실제 값을 value 필드로 갖는 wrapper 클래스로 NullPointerException으로부터 자유로워지려고 사용하는 클래스이다.

Optional을 파라미터로 넘어가는 등이 아니라 반환 타입으로써 제한적으로 사용되도록 설계되었다.

Optional을 값을 Wrapping하고 다시 풀고, null일 경우에는 대체하는 함수를 호출하는 등의 오버헤드가 있어 잘못 사용하면 성능을 저하시킬 수 있다.

따라서, 값이 절대 null이 아니라면 Optional을 사용하지 않는 것이 좋다.

즉, Optional은 메서드의 결과가 null이 될 수 있으며, null에 의해 오류가 발생할 가능성이 높을 때 반환값으로만 사용되어야 한다.