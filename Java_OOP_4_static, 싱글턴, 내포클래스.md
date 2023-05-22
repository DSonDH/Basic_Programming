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

## static에 대한 비판

# 디자인 패턴

## 디자인 패턴 소개

### 디자인 패턴 장단점

### 싱글턴 패턴


# 내포 클래스
## 내포 클래스를 사용 안 할 경우

## 비정적 내포 클래스를 사용할 경우
## 정적 내포 클래스를 사용할 경우
