# Java Class

클래스란, 객체의 정의 또는 유형을 나타낸다.  
자바에서 클래스는 필드, 생성자 및 메서드를 포함할 수 있다.

## 클래스 정의

```java
class Car {
    
    // Fields
    private String type;
    private String model;
    private String color;
    private int speed;
    
    // Constructor
    Car (String type, String model, String color) {
        this.type = type;
        this.model = model;
        this.color = color;
    }
    
    // Methods
    int increaseSpeed(int increment) {
        this.speed = this.speed + increment;
        return this.speed;
    }
    
    // ...
}
```

위의 클래스를 이용하여 여러 유형의 자동차를 만들 수 있다.  

### 접근 제어자

접근 제어자란 클래스, 변수, 메서드 및 생성자에 대한 접근 수준을 설정하는데 필요한 키워드이다.  
최상위 클래스는 public 또는 default 접근 제어자만 사용할 수 있으며 나머지는 네 가지를 모두 사용할 수 있다.  

|Modifier |Class|Package|Subclass|World|
|:-------:|:---:|:-----:|:------:|:---:|
|public   |O    |O      |O       |O    |
|protected|O    |O      |O       |     |
|(default)|O    |O      |        |     |
|private  |O    |       |        |     |

## new 키워드

new 키워드는 생성자를 통해 새 객체에 대한 메모리를 할당한다.  

생성자는 일반적으로 생성된 객체의 주요 속성을 나타내는 인스턴스 변수를 초기화하는데 사용된다.  
생성자를 명시적으로 정의하지 않으면 컴파일러는 인자가 없는 기본 생성자를 만들고 객체에 메모리를 할당한다.  




<hr>

#### References

> 웹 문서
> - [Baeldung | Java Classes and Objects](https://www.baeldung.com/java-classes-objects)
> - [Baeldung | Access Modifiers in Java](https://www.baeldung.com/java-access-modifiers)
> - [Baeldung | A Guide to Creating Objects in Java](https://www.baeldung.com/java-initialization)
> - [Baeldung | Guide to the this Java Keyword](https://www.baeldung.com/java-this)