# Java Reflection

java Reflection은 자바에서 기본적으로 제공하는 API이다.

구체적인 클레스를 알지 못해도 클래스의 정보(메서드, 타입, 변수 등)에 접근할 수 있게 해주는 자바 API



```java
Class personClass = Class.forName("Person");
```

위와 같이 클래스의 이름만으로 해당 클래스의 생성자, 필드, 메서드 등 해당 클래스에 대한 거의 모든 정보를 가져올 수 있는 API이다.



### 어떻게 가능할까?

자바에서는 JVM이 실행되면 사용자가 작성한 자바 코드가 컴파일러를 거쳐 바이트코드(.class)로 변환되어 static영역(method영역)에 저장된다.

Reflection API는 이 정보를 활용한다.



### 어디에 활용 수 있을까?

기존에는 동적으로 클래스를 사용해야 할 때

```java
Object obj = new Person();
if(obj.instanceOf(Person)){
    ~~
}
```

대충 이런식으로 작성해 형변환하여 사용하는 것을 본 적이 있을 것이다.

하지만 실제로 우리가 코드를 작성할 때 이렇게 쓰지 않는다.

구체적인 클래스를 모를 일이 거의 없기 때문이다.

그러므로 Reflection을 활용할 일도 거의 없다.



그리고, Reflection은 클래스에 접근해 값을 변경하거나 private한 변수, 메서드에 접근할 수 있게 하는 대단한 기능을 가진 만큼 치명적인 단점을 가지고 있으므로, 사용하지 않을 수 있다면 사용하지 않는 것이 좋다.



치명적인 단점 중 대표적으로 **성능 오버헤드**가 있다.

컴파일 시점이 아닌 런타임 시 동적으로 타입을 분석하고 정보를 가져오므로 JVM을 최적화 할 수 없다.

또한, 직접 접근할 수 없는 private 인스턴스 변수, 메서드에 접근하기 때문에 내부를 노출하면서 추상화가 깨진다.

이로 인해 예기치 못한 부작용이 발생할 수 있다.



##### 결론적으로 Reflection은 App개발보다는 프레임워크나 라이브러리에서 많이 사용된다.

프레임워크나 라이브러리는 사용자가 어떤 클래스를 만들지 예측할 수 없기 때문에 동적으로 해결해주기 위해 Reflection을 사용한다.



실제로 intellij의 자동완성, Hibernate등등 많은 프레임워크나 라이브러리에서 Reflection을 사용하고 있다.



Spring Framework에서도 Reflection API를 사용하는데 대표적으로 Spring Container의 BeanFactory가 있다.

Bean은 애플리케이션을 실행한 후 런타임에 객체가 호출될 때 동적으로 객체의 인스턴스를 생성하는데 이때 사용하게 된다.







