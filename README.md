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

## 메서드 정의

메서드는 여섯 부분으로 구성된다.  
Access modifier, Return type, Method identifier, Parameter list, Exception list, Body

```java
public String getName(String firstName, String lastName) throws RuntimeException {
    return firstName + " " + lastName;
}

/**
 * Access modifier: public  
 * Return type: String  
 * Method identifier: getName  
 * Parameter list: String firstName, String lastName  
 * Exception list: throws RuntimeException  
 * Body: return firstName + " " + lastName; 
 */
```

##### 여기서 새롭게 알게 된 사실  
1. Method identifier 은 최대 65536자 까지 정할 수 있다는 것이다.
2. Parameter list 는 쉼표로 구분하며 0 개에서 최대 255 개를 가질 수 있다.  

### Method Signature

Method Signature 는 두 가지 요소로만 구성된다.  
Method identifier 와 Parameter list

### Method Overloading

Method identifier 는 같지만 Parameter list 가 서로 다른 두 개 이상의 메서드를 정의할 수 있다.  
즉, Method Signature 가 다른 메서드이다.  

## 생성자

#### A No-Argument Constructor

```java
import java.math.BigDecimal;
import java.time.LocalDateTime;

class BankAccount {
    private String name;
    private BigDecimal balance;
    private LocalDateTime opened;

    public BankAccount() {
        this.name = "";
        this.balance = 0;
        this.opened = LocalDateTime.now();
    }
}
```

위에 작성한 생성자에 대해서 몇 가지 짚고 넘어가야 하는게 있다.  
첫째, 위의 생성자는 메서드이지만 return type 이 없다. 생성자는 생성한 객체를 묵시적으로 반환하기 때문이다.  
둘째, arguments 를 받지 않는다.  
우리는 이것을 arguments 가 없는 생성자라고 한다.  

생성자를 명시적으로 작성하지 않으면 컴파일러가 arguments 가 없는 기본 생성자를 추가한다.  
이것이 명시적으로 생성자를 작성하지 않았음에도 객체를 생성할 수 있었던 이유이다.  

#### A Parameterized Constructor

```java
import java.math.BigDecimal;
import java.time.LocalDateTime;

class BankAccount {
    private String name;
    private BigDecimal balance;
    private LocalDateTime opened;

    public BankAccount(String name, BigDecimal balance, LocalDateTime opened) {
        this.name = name;
        this.balance = balance;
        this.opened = opened;
    }
}
```

위 코드는 arguments 를 받는 생성자를 명시적으로 작성한 것이다.  

```java
BankAccount account = new BankAccount("Hyukjae", BigDecimal.valueOf(10000), LocalDateTime.now());
```

이렇게 명시적으로 생성자를 하나라도 작성했다면, 컴파일러는 arguments 가 없는 기본 생성자를 추가하지 않는다.  

#### A Copy Constructor

```java
import java.math.BigDecimal;
import java.time.LocalDateTime;

class BankAccount {
    private String name;
    private BigDecimal balance;
    private LocalDateTime opened;

    public BankAccount(String name, BigDecimal balance, LocalDateTime opened) {
        this.name = name;
        this.balance = balance;
        this.opened = opened;
    }
    
    public BankAccount(BankAccount other) {
        this.name = other.name;
        this.balance = other.balance;
        this.opened = other.opened;
    }
}
```

위 코드는 arguments 로 동일한 클래스를 받는 생성자를 추가한 것이다.

```java
BankAccount other = new BankAccount("Hyukjae", BigDecimal.valueOf(10000), LocalDateTime.now());
BankAccount account = new BankAccount(other);
```

#### A Chained Constructor

```java
import java.math.BigDecimal;
import java.time.LocalDateTime;

class BankAccount {
    private String name;
    private BigDecimal balance;
    private LocalDateTime opened;

    public BankAccount(String name, BigDecimal balance, LocalDateTime opened) {
        this.name = name;
        this.balance = balance;
        this.opened = opened;
    }
    
    public BankAccount(String name) {
        this(name, BigDecimal.valueOf(10000), LocalDateTime.now());
    }
}
```

위 코드는 arguments 로 일부 값만 받아 나머지는 추론하거나 기본값을 제공할 수 있는 생성자를 추가한 것이다.
만약 부모 클래스 생성자를 연결하려면 this 키워드 대신 super 키워드를 사용해야 한다.  
또한, this 또는 super 키워드는 항상 첫번째로 호출되어야 한다.  


<hr>

#### References

> 웹 문서
> - [Baeldung | Java Classes and Objects](https://www.baeldung.com/java-classes-objects)
> - [Baeldung | Access Modifiers in Java](https://www.baeldung.com/java-access-modifiers)
> - [Baeldung | A Guide to Creating Objects in Java](https://www.baeldung.com/java-initialization)
> - [Baeldung | Guide to the this Java Keyword](https://www.baeldung.com/java-this)
> - [Baeldung | Methods in Java](https://www.baeldung.com/java-methods)
> - [Baeldung | A Guide to Constructors in Java](https://www.baeldung.com/java-constructors)
