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


## 접근 제어자
### 일반적인 접근 제어자

## private 메서드 용도


## 패키지 접근 제어자


## getter, setter


## 캡슐화, 추상화






