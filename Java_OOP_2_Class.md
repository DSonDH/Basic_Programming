# Class와 Object

```java
class Human {
    String name;
    int age;
    Sex sex;
    
    void walk() {
        age += 1;
    }
    void eat() {
        age -= 1;
    }
    void speak() {
        System.out.println("Hello friend");
    }
}
```
![image](https://user-images.githubusercontent.com/15919242/236350374-f78ebc06-b6a5-4f01-860c-46f6bdb044d5.png)  
OOP에서의 클래스  
새로운 개체를 만들 때 사용하는 명세서  
개체는 반드시 클래스로 만들어야 함.  
class에는 속성, 동작 등등 을 명세한다.  


```java
public class Human {
    public String name;
    public int age;
    public Sex sex;
    
    public void walk() {
        this.age += 1;  // 위에 정의한 age를 의미함
    }
    public void eat() {
        this.age -= 1;
    }
    public void speak() {
        System.out.println("Hello friend");
    }
}
```
접근 제어자 public  
![image](https://user-images.githubusercontent.com/15919242/236350959-ad72b928-fd62-44fd-884d-03a30969764e.png)  

public을 안 붙이면?  
![image](https://user-images.githubusercontent.com/15919242/236351142-7f50d07d-fc7e-4f16-9ee0-2286098523ec.png)  

용어정리!  
상태를 칭하는 용어 
멤버 변수 (member variable) *  
필드 (field) *  
속성 (attribute) (비추천)  

동작을 칭하는 용어  
멤버 함수 (member function) *  
메서드 (method) *  
메시지 (message)  


## 개체 만들기와 메모리
Java에서는 기본 자료형만 스택에 넣을 수 있다.  
```java
Human adam = new Human();
```
Java와 C#모두 동적할당을 한다.  
Human adam 은 Stack 메모리에, adam이 저장하고 있는 new Human()을 통해서 만들어진 주소는 Heap 메모리에 저장  
![image](https://user-images.githubusercontent.com/15919242/236352189-1be2a22d-bea9-43a0-b2ce-d51d8d071499.png)  
모든 Java 클래스 형은 참조형  

용어  
인스턴스 (instance)  
개체를 부르는 또 다른 표현  
'어떤 클래스에 속하는 개체의 한 예'라는 의미  
인스턴스화(instantiation) : 클래스로부터 개체 하나를 만드는 행위  

## 개체 멤버에 접근하기, 참조형
![image](https://user-images.githubusercontent.com/15919242/236357364-36b92334-f01b-444e-a182-a9c66f76e217.png)  
Human adam;  
사실상 포인터. 메모리 주소를 저장하는 변수. adam역시 힙에 위치한 Human 개체의 주소를 담은 변수임.  
기본 자료형 (소문자) 빼고는 모두 포인터 형, 참조형임  
![image](https://user-images.githubusercontent.com/15919242/236357582-75b763b2-a71b-4330-84b4-aac7d1ca4707.png)  

![image](https://user-images.githubusercontent.com/15919242/236357785-467785db-5669-456e-a7fa-634c07252b90.png)  
![image](https://user-images.githubusercontent.com/15919242/236358036-216a5f99-af7f-4e82-b15b-a102807e9868.png)  


## 멤버 변수의 초기값, .연산자
![image](https://user-images.githubusercontent.com/15919242/236358211-82216b51-3dc9-4fe8-a7cc-3dcd43c17f3a.png)  
Java는 0에 준하는 값으로 초기화 해줌.  
int는 0, float는 0.0, 참조형은 null로  
C는 성능이 제일 중요하고, Java는 실수 방지가 중요하니까.  
![image](https://user-images.githubusercontent.com/15919242/236358308-a088111c-aef9-4452-bb23-c7d695178fbf.png)  

.연산자  
![image](https://user-images.githubusercontent.com/15919242/236358368-17d4ecb3-93a7-4616-a59d-765e5e413727.png)  
Java는 포인터 역참조용 * 연산자가 없으므로, 주소를 직접 읽을 방법 자체가 없음.  
따라서 언제나 그 주소에 저장된값을 읽어옴. 그 주소에 포인터 연산도 불가능.  


## 개체의 메서드 호출하기
![image](https://user-images.githubusercontent.com/15919242/236358708-fcd6b7b4-5546-4c23-9934-51d558cf4371.png)  

* 동적 메모리 반환 코드는 ?
자바에는 free()가 없다.  
![image](https://user-images.githubusercontent.com/15919242/236358890-59007d72-09a9-4bb9-9f5e-098e90b2fb37.png)  
![image](https://user-images.githubusercontent.com/15919242/236358999-70ec35e5-3b2b-4255-9c44-5a586b4e6bda.png)  


## 생성자
``` java
Human adam = new Human();

adam.sex = Sex.MALE;
adam.name = "Adam";
adam.age = 20;
```
위 코드의 문제점은 개채 생성시 이미 완성본이 오지 않은 점.  
뒤에 속성을 덕지덕지 붙이고 있음.  

생성 시 올바른 값으로 초기화 하기.  
![image](https://user-images.githubusercontent.com/15919242/236359330-4506b151-a2ff-470b-8b03-b40efd358c09.png)  

이를 생성자(constructor)라고 함.  
![image](https://user-images.githubusercontent.com/15919242/236359386-9e1d0eb9-d564-4a57-a00d-658ad14b5998.png)  

오버로딩(매개변수 다른 것)도 가능 !  
(오버라이딩은 다형성 - Polymorphism을 위해 상속 개념을 사용하는 방법.)  
![image](https://user-images.githubusercontent.com/15919242/236359451-888e9b01-f4ee-45b9-8619-cd43ffe33c89.png)  
같은 클래스 내부에 여러 argument 조합에 대해 각각 생성자 구현함.  
![image](https://user-images.githubusercontent.com/15919242/236359774-467fa600-a7cd-4cba-b8f2-aaff2eaf6e61.png)  
this가 다시 개체 생성을 지시함. 근데 3개짜리 매개변수를 받아서 호출하도록 하고, 1개는 dummy값으로.  
![image](https://user-images.githubusercontent.com/15919242/236359925-926aea81-c378-4238-9cd4-36e6d501eaf4.png)  

![image](https://user-images.githubusercontent.com/15919242/236360232-406416ea-53a6-48ba-a0a3-042c73e3254e.png)  
위 코드는 3개짜리 매개변수 받는 생성자만 정의 해놓고 0개 매개변수로 초기화 하려고해서 그럼.  

!!!! 기본 생성자 (default constructor)  
프로그래머가 생성자 하나도 안 정해줬을 때 '만' 컴파일 시 자동으로 생성되는 0개 매개변수짜리 생성자.  
![image](https://user-images.githubusercontent.com/15919242/236360019-2bdb94aa-8f42-4df9-b165-60f69e099870.png)  

(intellij같은걸로 .class파일 디컴파일 해서 어떤 모양으로 코드가 실행되는지 볼 수 있음.)  

* 생성자로 초기화를 해야 하는 이유
1. 개념상의 문제 : 속이 빈 콜라캔, 0살 무성별 사람 ... ??  

2. 후조건의 문제 
생성자의 후조건 : 개체의 상태는 개체 생성과 동시에 유효하다 !!  

3. 사용자를 고려 안 한 문제  
![image](https://user-images.githubusercontent.com/15919242/236360457-dd8bed60-e421-4ff4-b771-acc13f596172.png)  
개채 생성 직후에 만드는건 실수 여지가 너무 많음.  
![image](https://user-images.githubusercontent.com/15919242/236360678-76460685-b699-45e3-b057-b4f30a0f828f.png)  

![image](https://user-images.githubusercontent.com/15919242/236361331-3a569c78-677c-4cf3-ab13-4b14da32bdb5.png)  
함수 이름 괴상해서 getLengthSquared()라 안하고 getLength()라 하면 함수 이름이 잘못 된거지,  
반환 값에 루트 씌우고 그러지 말자.  
외부 클래스에서 클래스 내부 데이터를 알 필요가 없음 (데이터 추상화, 캡슐화의 일부이기도 함)  

```java
// Passenger.java
Package academy.pocu.comp2500samples.w02.vehicle;

public class Passenger {
    public String name;
    
    public Passenger(String name) {
        this.name = name;
    }
    
    public void sayName() {
        System.out.println(String.format("Hi, I'm %s!", this.name));
    }
}


// VehicleType.java
package academy.pocu.comp2500samples.w02.vehicle;

public enum VehicleType {
    MOTOCYCLE,
    SEDAN,
    MINIVAN
}


// Vehicle.java
package academy.pocu.comp2500samples.w02.vehicle;

import java.util.ArrayList;

public class Vehicle {
    public VehicleType type;
    public ArrayList<Passenger> passengers;
    public double fuelAmount;
    public int mileage;
    
    public Vehicle(VehicleType type) {
        this(type, new ArrayList<Passenger>(), 0.0);
    }
    
    public Vehicle(VehicleType type, double fuelAmount) {
        this(type, new ArrayList<Passenger>(), fuelAmount);
    }
    
    public Vehicle(VehicleType type, ArrayList<Passenger> passengers, double fuelAmount) {
        this.type = type;
        this.passengers = passengers;
        this.fuelAmount = fuelAmount;
        this.mileage = 0;
    }
    
    public void addPassenger(Passenger passenger) {
        this.passengers.add(passenger);
    }
    
    public void removePassenger(String name) {
        for (Passenger p : this.passengers) {
            if (p.name.equals(name)) {
                this.passengers.remove(p);
                break;
            }
        }
    }
    
    public void addFuel(double fuelAmount) {
        this.fuelAmount += fuelAmount;
    }
    
    public void drive(int distance) {
        System.out.println(String.format("Traveling %dkm.", distance));
        
        double gasMileadge = 100_000;
        
        switch (this.type) {
            case MOTORCYCLE:
                gasMileage = 0.05;
                break;
            case SEDAN:
                gasMileage = 0.07;
                break;
            case MINIVAN:
                gasMileage = 0.1;
                break;
            default:
                assert (false) : "Unrecognized vehicle type: " + this.type;
                break;
        }
        
        double requiredFuel = gasMileage * distance + 0.01 * this.passengers.size();
        
        if (requiredFuel > this.fuelAmount) {
            System.out.println("Not enough fuel to travel that far!");
            return;
        }
        
        this.fuelAmount -= requiredFeul;
        this.mileage += distance;
        
        System.out.println(String.format("FuelAmount %.2fL.", this.fuelAmount));
        System.out.println(String.format("Mileage %dkm.", this.mileage));
    }
}

// Program.java
package academy.pocu.comp2500sample.w20.vehicle;

import java.util.ArrayList;

public class Program {
    
    public static void main(String[] args) {
        Passenger blackWidow = new Passenger("Natasha");
        blackWidow.sayName();
        
        Vehicle motorcycle = new Vehicle(VehicleType.MOTORCYCLE);
        motorcycle.addPassenger(blackWidow);
        motorcycle.addFuel(22.0);
        
        ArrayList<Passenger> taxiPassengers = new ArrayList<Passenger>();
        taxiPassenger.add(new Passenger("Tony"));
        taxiPassenger.add(new Passenger("Thor"));
        
        Vehicle taxi = new Vehicle(VehicleType.SEDAN, taxiPassengers);
        taxi.addFuel(60.0);
        
        ArrayList<Passenger> vanPassengers = new ArrayList<Passenger>();
        vanPassengers.add(new Passenger("Steve"));
        vanPassengers.add(new Passenger("Bucky"));
        vanPassengers.add(new Passenger("Wanda"));
        vanPassengers.add(new Passenger("Bruce"));
        vanPassengers.add(new Passenger("Clint"));
        
        Vehicle van = new Vehicle(VehicleType.MINIVAN, vanPassengers, 70.5);
        
        System.out.println("Motorcycle:");
        motorcycle.drive(50);
        
        van.removePassenger("Steve");
        van.removePassenger("Bucky");
        
        System.out.println("Van:");
        van.drive(1000);
        
        System.out.println("Van:");
        van.addFuel(50.0);
        van.drive(100);
    }
}
```

## 접근 제어자 (access modifier)  
생성자로 올바르게 만들어도, 그 이후에 -1살 이런거 만들 수 있음.  
이런 분탕질을 제한하기 위한 장치가 접근 제어자.  
class수가 500개가 넘는 건 복잡한 수준이 아니래 .. ㄷㄷ 현업은 역시 빡세군.  
몇천개 이상이 되어 복잡하다면, 실수발생 가능성 많음.  
접근 제어 주체는 class 자체가 되면 좋음.  

java의 접근제어자 4가지  
![image](https://user-images.githubusercontent.com/15919242/236453217-cd2b1fcb-293a-4cfc-bc2c-8ca59896e943.png)  
OOP에서 논하는 것은 주로 public, protected, private  

1. public  
![image](https://user-images.githubusercontent.com/15919242/236453543-86e26ae8-c25c-42df-b972-f284ba0c79dc.png)  

2. private  
![image](https://user-images.githubusercontent.com/15919242/236453599-c62cf0aa-8205-4bd7-b3da-4d5f010d22bb.png)  
![image](https://user-images.githubusercontent.com/15919242/236453657-c35ed7b1-0e92-4fb7-8771-a7fec6e9b98b.png)  
외부 접근은 컴파일 오류 뜸.  

private method는 ?  
![image](https://user-images.githubusercontent.com/15919242/236453763-568912aa-49e7-45c5-85f9-47713b5d7c72.png)  

### 일반적인 접근 제어자
![image](https://user-images.githubusercontent.com/15919242/236453884-d30e3104-95fe-4324-9968-a2855dc704e8.png)  

캡슐화 : private으로 숨긴 멤버변수들 외부접근 막음.  
추상화 : 그속에 데이터를 밖에서 볼 수 는 없지만, 있는지 없는지는 추측만 가능한데,  
일단 getName호출하면 데이터는 주겠지. 가정은 할 수 있는 것.

## private 메서드 용도?
private method는 클래스 안에서만 호출할 수 있음.  고로 코드 중복을 막기위함.  
![image](https://user-images.githubusercontent.com/15919242/236455035-8928170b-356f-4693-86e8-d1e65a83ff89.png)  
![image](https://user-images.githubusercontent.com/15919242/236455219-9b8e7a55-6b0d-4c98-b9eb-6d1ebb8f86c0.png)  

private과 생성자  
![image](https://user-images.githubusercontent.com/15919242/236455303-3e56a97a-131f-4853-ae52-8a4573866d38.png)  
생성자가 private하면 새로운 개체 생성하려고 하면 컴파일 오류 뜸.  
그러나 쓰는 경우는 나중에 배움.  

[내부]의 의미 !!  
![image](https://user-images.githubusercontent.com/15919242/236455587-6784ac5f-7199-460f-b702-5023efe968f2.png)    


## 패키지 접근 제어자
사용하고자 하는 파일을 import하는거랑 접근제어자 권한이 설정되는 거랑은 상관 없음 !!  
private / public / () : package접근제어 셋 중 하나가 어떻게 설정되는지 따로 고려해야함 !!  

![image](https://user-images.githubusercontent.com/15919242/236666627-dc5ea1af-dc79-4b50-a776-f139cb658ca5.png)  
접근제어자 안붙이면 적용되는 접근 범위.  
![image](https://user-images.githubusercontent.com/15919242/236666638-e8ee6032-6152-487d-83fb-6c0d8e0ea518.png)  
![image](https://user-images.githubusercontent.com/15919242/236666647-42f2dafb-8510-4e66-99b6-7f4ccf3903ef.png)  
Application.java에서 happy.happiness를 제어하려고 하면 컴파일 에러 뜸.  
근데, 같은 패키지에 있다는 이유 만으로 내 object의 속성을 마음대로 제어할 수 있는건 캡슐화에 위배되는 내용임.  

그럼 패키지 접근 제어자는 언제 사용하면 좋을까?  
![image](https://user-images.githubusercontent.com/15919242/236666911-400f01bf-b474-48cb-bd8c-b55375c7a441.png)  

## getter, setter
getter  
남에게 보여주고픈 정보를 보여주는건 좋은데, 남이 내 정보를 수정할 수 없게 하려면, 보여줄 때 method로 보여주게 하면됨.  
![image](https://user-images.githubusercontent.com/15919242/236677832-9aa9cb6a-0432-43c5-a1dc-2d8752175372.png)  
![image](https://user-images.githubusercontent.com/15919242/236677860-0ae95dd4-7f72-43c1-907e-291b8c4a3276.png)  
setter  
남이 변경도 할 수 있게 할 때  
![image](https://user-images.githubusercontent.com/15919242/236677954-b5b2a544-47d3-4728-bcae-b1cb057c1c6c.png)  
![image](https://user-images.githubusercontent.com/15919242/236677998-7a21e7a1-4dcd-4ece-a682-4a43424b0f94.png)  
그냥 속성을 public으로 하면 되지 않냐 싶은데, 그러면 안된다고 함. 일반적으로 setter getter만듦.  
클래스를 작성한 프로그래머가 그 클래스에 대해 가장 잘 안다. 반대로 다른 사람들은 그 클래스 내부 잘 모름.  
그래서 getter, setter를 만드는 관례를 만듦. 보다 자세한 내용은 아래에:  
![image](https://user-images.githubusercontent.com/15919242/236678080-8c789558-634f-4cde-b1fc-cf78f9655644.png)  
* 트으윽수한 경우에 성능을 위해 getter/setter생략으로 함수 호출에 따른 오버헤드와 불필요한 리소스 소모를 줄이는 경우도 있다고 함.  

!!! best practice:  
![image](https://user-images.githubusercontent.com/15919242/236678471-ebfedaec-3d5e-4eab-9fcd-8be78bc1387f.png)  
![image](https://user-images.githubusercontent.com/15919242/236678490-586a90c6-059f-4485-ac50-e6fd36a0f590.png)  
![image](https://user-images.githubusercontent.com/15919242/236678509-672eaaf7-777a-437d-aee9-34335bf4f01d.png)  
![image](https://user-images.githubusercontent.com/15919242/236678546-acf3a78d-3231-4190-85a1-b7084a0e2081.png)  
위에 경우는 남에집 개를 가리키지만, 실제 내용을 바꾸려면 setter로 제어할 수 있으므로 setter의 중요성이 있긴 함.  
참고로 C++은 getter에서 읽기전용 reference를 반환할 수 있어서 이런 문제가 없음.  

![image](https://user-images.githubusercontent.com/15919242/236678658-bd6993dd-a4e9-4164-b697-3b19cb9d13d3.png)  
![image](https://user-images.githubusercontent.com/15919242/236678677-f6f1cc38-4b55-4391-856a-ee215d41cc49.png)  
![image](https://user-images.githubusercontent.com/15919242/236678746-db0f87c8-3141-4c64-98a0-e928fd6807bf.png)  
내가 쉽게 소스코드 바꿀 수 있는 상황이면 setter나중에 추가하고, 외부 판매용? 이라 내 손을 떠나는 거면 setter넣어두기.  

## 캡슐화, 추상화
OOP 4대 특성 : 캡슐화, (데이터)추상화, 상속, 다형성  
클래스 만들기와 private 멤버 변수가 캡슐화.  
private 멤버 변수와 getter/setter가 데이터 추상화.  

캡슐화  
![image](https://user-images.githubusercontent.com/15919242/236678905-ec8e991d-d8d2-4523-9dbf-ccb397ecaa62.png)  

추상화  
![image](https://user-images.githubusercontent.com/15919242/236678965-58849b9c-5941-40ff-bca2-c458d2a4ac82.png)  
추상 자료형 관점이 캡슐화에 무게를 둔 다수설, 절차적 데이터 추상화가 소수설.  
OOP에서 추상화 : 어떤 구체적인 것에 직접 손대지 않겠다는 의미. 그 이상 그 이하도 아님.  

추상화의 단점 1  
동작 없이 데이터만 있는 클래스는 쓸데없는 코드만 늘어남.  
ex: 웹 프로그래밍에서 많이 볼 수 있는 data transfer object (DTO)  
그래서 이런 경우에는 그냥 public 데이터를 쓰기도 함.  

추상화 단점 2  
어떻게 추상화를 해야 하는지 뚜렷한 객관적 기준이 없음  
사람은 뚜렷한 실체가 없는 개념을 이해하기 어려워 함.  
이해하더라도 각자 달리 이해하기 쉬움.  
나중에 다형성, 상속, 인터페이스에서 나오는 추상화에서 특히 문제가 됨.  
