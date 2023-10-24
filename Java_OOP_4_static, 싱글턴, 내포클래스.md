# static
전역 변수나 전역 함수가 없어서 좀 불편한듯 ?
System.out.println() 은 개체 안만들었는데 그냥 사용하네? static 클래스라 그럼 !!  
단순한 계산도 개체를 만들어서 하는건 좀 억지 같음.  
개체 단위가 아니라 클래스 단위에서 (공장에서 찍어낸 물건의 총 갯수 기억 등)  
뭔가를 하고싶을 때 정적(static)이 해결해줌 !!  

## 정적 메서드
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/5dccd33c-1949-4f86-936e-22126cc0e0d7)  
멤버 함수 시그내처에 static만 붙여주면 됨.  
이 멤버함수의 소유주는 인스턴스가 아니라 클래스!!!  
new를 이용해서 Math개체를 안만들어도 됨.  
근데 궂이 만들어서 호출은 할 수 있음.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/b007268b-045d-40c4-922a-d79b75caef4e)  


## 정적 클래스와 생성자
궂이 만들어서 헷갈리는데 못만들게 할수 있나?  
있음! 개체를 못만들게 할 수 있음. 생성자를 private으로 궂이 만들어두면 됨.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/a47f1633-2a9d-4b6b-b90b-1a3fac4753b9)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/133fedc8-c066-4c8e-831b-8f379eccc9b4)  

(참고: C#에서는 static클래스가 있어서 private생성자 꼼수 안부려도 됨. 근데 Java나 C++은  
static class개념이 없어서 궂이 private 생성자 만들어줘야 함.)

## 정적 멤버 변수
개체보다 상위개념인 클래스에 있어야 하는 변수.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/97d67a99-5144-4b7f-b5c1-47f3f8736f70)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/2c244ebc-52bc-4bb9-b981-824028d9a626)  
범위 지정자 개념이 적용되서, {} 범위 밖에 필요한 정보가 있는지 확인함.  

## 정적 메서드에서 멤버 변수 접근하기
정적 멤버변수에 접근하는 정적 메서드  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e4a33f8d-7638-4cb7-affe-c81712883fcc)  

정적 메서드에서 비정적 메서드 접근하기  
오류 뜸  
클래스에 속한 메서드가 개체에 속한 멤버함수, 멤버변수에 접근 불가.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/f84cf821-b081-418c-a608-b6e68700a13c)  
클래스 마다 생성할 수 있는 개체는 거의 무한할 수 있음. 클래스가 그 중에 어떤거에 접근해야 하는지 알 턱이 없음.  

* !!! 정적 메서드는 정적 멤버 변수/함수만 접근 가능하다 !!!

정리
1. static 멤버 변수 및 멤버 함수는 클래스에 속함 (딱 하나만 존재)  
2. static이 아닌 것은 개체에 속함 (개체 수 만큼 존재)  
3. 비정적 -> 정적 : 접근 가능  
4. 정적 -> 비정적 : 접근 불가능  

static이 C의 전역 변수/함수와 비슷한 점도 있고, 더 좋은 점도 있음  
비슷 : 수명 - 프로그램 실행 시 부터 종료 시 까지 존재함.  
장점 : 클래스 내부에서만 접근 가능하도록 접근 범위를 제어할 수 있다. 공개적으로 보일 일 없음.  
각기 다른 클래스끼리 써도 이름 충돌이 적다.  
ColaCan.printStats();  
BeerCan.printStats();  

``` java
package academy.pocu;

// Student.java
public class Student {
    // 코드 생략
}

// StudentManager.java
package academy.pocu;
import java.util.ArrayList;

public class StudentManager {
    private static int numTotalEnrolled;
    private ArrayList<Student> students = new ArrayList<>();
    
    public void enroll(Student student) {
        this.students.add(student);             // (1)
        ++this.numTotalEnrolled;                // (2)
    }
    
    public int getStudentCount() {
        return this.students.size();            // (3)
    }
    
    public static int getTotalEnrolled() {
        return StudentManager.numTotalEnrolled; // (4)
    }
    
    public static void reset() {
        StudentManager.numTotalEnrolled = 0;    // (5)
        this.students.clear();                  // (6)
    }
}
// 위 코드에서 오류가 나는 곳은 ? 6번 !
// 오류 종류는 ? 컴파일 오류!
```

* code sample : static logger 파일 읽고 빠르게 눈에 들어와야 함 !!  

## static에 대한 비판
개체지향이 지양하고자 했던 바 이므로.  
OO의 개념이 멀다.  
근데 개념과 멀다고 잘못된 방법은 아님.  
OO개념을 언제, 어디서 써야 하는지 아는게 훌륭한 프로그래머의 자세임 !!  
static과 같이 작동하지만, class로 구현한게 singleton패턴임.  
얘도 똑같은 이유로 욕먹는대 ...  


# 디자인 패턴
기본적으로 사람은,  
1. 새로운 문제를 맞이한다.
2. 장기기억에서 과거에 겪은 비슷한 문제를 찾는다.
3. 그 문제 솔루션을 새 문제에 적용한다.  

## 디자인 패턴 소개
소프트웨어 설계에서 흔히 겪는 문제에 대한 해결책.  
범용적, 반복적인데 완성된 설계가 아님.  
가이드일 뿐.  

### 디자인 패턴 장단점
장점  
1. 이미 테스트를 마친 검증된 개발방법을 사용해 개발 속도 향상  
새 코드 작성할 때 곧바로 알 수 없는 문제점들이 있음.  
아직 드러나지도 않았고, 예측 못한 문제들.  
증명된 패턴은 이런 문제에도 대비되어 있음.  
(이게 장점이라구 ..? 생각하면 정상이래.)  

2. 공통 용어 정립을 통한 개발자들 간의 빠른 의사소통 촉진  
무슨패턴을 사용하면 된다는 한마디로 의사소통 가능.  
(근데 모든 개발자들이 그 패턴과 용어을 알아야 함.)  

단점 
1. 고치려는 대상이 잘못 됨  
2. 곧바로 적용할 수 없는 참고 가이드를 패턴이라 부를 수 없음  
3. 잘못 적용하는 경우가 빈번함  
4. 비효율적인 해법이 될 수 있음
5. 다른 추상화 기법과 크게 다르지 않음

디자인 패턴 저자들이 책에 쓴 내용  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c55c6344-10a5-4a55-bf2b-d1dff36bdc2d)  

디자인 패턴 공부법  
대부분 다형성에 기반한 추상화에 기초함.  
내가 겪은 다양한 문제를 예쁘게 정리하는 방법임 !!  
내 코드가 정확히 어떻게 도는지 이해될 때까지 디자인 패턴은 금지.  
ex: 카카오톡 같은걸 만들려면 어떻게 설계해야 하는지 알 때 까지.  
남은 이렇게 작성했구나 ~ 이건 내거보다 낫네? 나도 이렇게 했는데? 이런 편안한 반응이 나올 수준까지 ...  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/4b2807da-8b92-46c1-97ea-f1de9349e322)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/0c8f548c-7e76-4356-b9a8-758062208276)  


### 싱글턴(singleton) 패턴
어떤 클래스에서 만들 수 있는 인스턴스 수를 하나로 제한하는 패턴.  
1. 프로그램 실행 중 최대 하나만 있어야 함.  
프로그램 설정, 파일 시스템 등.  
2. 이 개체에 전역적으로 접근이 가능해야 함.  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/2cde3e56-46ca-43e6-bf53-e3dcdb25b23d)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d69320ad-75ff-4a9a-b071-66b170016484)  
private 생성자 이므로 new 로 생성 안됨.  
getInstance호출 했을때 비로소 생성해주고, 이미 있으면 있는거 반환함.  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/cfe3b5ab-6272-469e-9f97-b816c282fe9d)  
다른 method들은 일반 메서드.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/8a0c23b3-4c3e-41af-b0e7-6f1c55798895)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e4641470-e637-4d66-aa15-ba86b9e13985)  

static vs singleton 다른점이 있음 !!  
static으로 못하는 일  

1. 다형성을 사용할 수 없다.
2. 시그내처를 그대로 둔 채 멀티턴 패턴(갯수제한 둔 것. 1개만 둔 게 싱클턴.)으로 바꿀 수 없다.  
3. 개체의 생성 시점을 제어할 수 없다.  
Java의 static은 프로그램 실행 시에 초기화 됨.  
단, 싱클턴을 사용해도 제어에 어려움이 있음.  

여러 클래스에 싱글턴 패턴이 있는 경우 초기화 순서가 중요할 때가 있음.  
초기화 순서를 보장하기 위해서 실무에서 이런 일을 하기도 함.  
프로그램 시작 시 여러 싱글턴의 getInstance()를 순서대로 호출하는 것.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/9bf240e3-a7ea-453e-bffe-2f4dda9783a9)  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d17212c1-b216-4180-bbfb-fb102c1d3c0d)  
기존 싱글턴으로 구현이 어려운 점이 발생하기도 함.  
따라서 다른 변형을 사용하기도 함.  
아래의 예는 getInstance호출할때 매번 다른 클래스 인자 두개를 세트로 넣어서 호출하는게 불편해서 이를 우회하는 방법으로 해결하는 방법을 소개하는 것임.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/306e0ef2-784e-40e0-a6cd-a03c2ecaf36d)  
create, get이 분리됨.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/fba8a3f4-ca27-43e1-9afc-cf180398a964)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/5d3ebc51-7d16-4e9e-adf3-63e09a24a95b)  
상태머신 : 상태가 바뀌면 그 바뀐상태에서 필요한 뭔가가 있다면 초기화를 새로 해주는 것.  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d79676c0-6f4f-469d-b63d-96761856ff2b)  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/53974b51-40ce-406d-a0e1-1bbcfaf90784)  
싱글턴은 안티패턴이라 하는 진영은 모든 것은 개체여야 한다는 진영임. 신경 안써도 됨.  


# 내포 클래스
클래스 안에 다른 클래스가 들어가 있는 모습.  
안에 들어 있는 클래스를 내포(nested) 클래스라 함.  
```java
public class Outer {
    public class Inner {
        ...
    }
    ...
}
```
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c21d9052-3db1-4c9b-b39a-1e9b7815f02d)  

용도  
서로 연관된 클래스를 그룹 지을 수 있음  
패키지로 그룹 짓는 것도 가능  
하지만 클래스 속에 넣는 것이 더 긴밀한 그룹  
내포 클래스는 바깥 클래스의 private 멤버에 접근 가능  
(바깥 클래스는 내포 클래스의 private 멤버에 접근 가능)  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/a7e868e2-436e-46a1-a318-313d34fe041e)  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/4aba1885-c888-4db7-92a1-63a009f4c468)  
 ![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/73acb793-8efd-448b-a464-106923a9897c)  

  
 정적 내포 클래스를 활용한 버전.  
 ![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/b6d61fd6-b6d5-4310-b3a1-0ca1271e9133)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/9b85bb36-2ec3-4cee-8766-64d7f51cef75)  
새로운 개체 생성할 때 코드가 좀 더 깔끔해짐. Record.new reader() 가 아니고 new Record.Reader()  

  
자바에는 static class가 없음.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e9603fcf-b2d6-41b3-859d-897954bb3123)  
다른 언어도 이렇게 씀.  
outer class의 레퍼런스가 없다는 의미는, 자동적으로 outer class의 멤버변수를 자동으로 불러올 수 없다는 뜻  

Q: this를 반드시 써라는 말인가?  
A: this.record를 해줘야 한다는 말은 this를 반드시 써야한다는 의미가 아니었습니다.  
Record 안에 있는 멤버에 접근하려면 반드시 Reader 개체 안에 저장된  
record 멤버 변수를 통해 접근해야 한다는 의미입니다.  
그와 반대로 비정적 클래스에서는 이걸 생략해도 접근이 가능하거든요.  

Q: 내포클래스를 사용하지 않고 쓰는거나, static nested class를 쓰는거나 같은거 아니냐?  
A: 어느 계층적 구조에서나 마찬가지로 무엇의 주종관계를 나타내는 정도의 용도가 있습니다. (그 외에는 별 차이가 없죠)  
  
  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/a2990c61-146e-432e-a7db-02abd4da782c)  
static은 자바에서 class하나당 하나만 생성할 수 있고, static아닌 변수는 클래스가 개체를 특정할 수 없으므로  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c2990441-f7fd-44c2-b31f-bb83ef835e4f)  

요즘에는 내포 클래스를 잘 안씀.  
클래스마다 파일을 만듦!!  

상속과의 차이점 ??  
