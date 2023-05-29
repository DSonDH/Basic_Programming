개체지향에서 이루려고 했던게 재사용성.  
재사용성의 중요한 키워드가 상속, 상속을 기반으로 하는 다형성임.  

# 상속(inheritance)  
부모의 어떤 특징을 물려받는 개념.  
이미 존재하는 클래스를 기반으로 새 클래스를 만드는 방법.  
새 클래스는 기존 클래스의 동작과 상태를 그대로 물려 받음 (유전)  
그 외에 새 클래스만의 동작과 상태를 추가 가능 (진화)  
물론 이 새 클래스를 상속해서 또 다른 클래스를 만들수 있음.  

용어 정리  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/443eae5f-37ec-45f4-ac92-b8dc37a2d4c0)  

두 클래스 간의 상속 관계를 성명하는 표현.  
1. 자식 클래스가 부모 클래스를 상속받았다.  
2. 자식 클래스가 부모 클래스로부터 파생되었다.  
3. 자식 클래스가 부모 클래스의 한 종류이다 (is - a)  

두 클래스의 중복되는 내용을 하나의 부모 클래스로 만들면 코드중복 방지 가능.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e4a06c51-67a5-436e-b9a7-6cb048664c7f)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/97b75ef6-c6bb-41f1-b27e-42b53a4b0723)  

상속하는 법  
``` java
public class Student extends Person
...
```
근데, 어떤 개체든 초기화는 생성자가 책임졌음. 부모부분도 초기화가 일어나야함.  
Person클래스 부분 초기화는 어디서 해야하지?  
1. 메모리에 개체 생성. (힙 메모리)  
2. 부모 생성자 호출.  
3. 자식 생성자 호출.  
java에서는 1번은 생략하고 진행하나, c++에서는 고려하게 됨.  
한 덩어리 메모리를 만드는데, 거기에 상속순서대로 부모의 멤버 -> 자식 멤버가 위치하게 됨.  

근데   
``` java
pulic Student() {
}
```
일 때 부모 개체의 어떤 생성자를 호출할 까 ? 당연히 매개변수 안받는 생성자를 호출함.  
근데, 부모 개체에서 매개변수 없는 생성자를 안만들었으면, 컴파일 오류 생김.  
!!!!개체는 생성 시 부터 유효한 상태를 가져야 하므로,  
자식 클래스의 생성자에서 부모 생성자를 호출해야함.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d46ab115-e266-4ebd-ac0e-c192f122724c)  
자식 클래스에 firstName, lastName을 따로 저장하면 코드 중복이므로 바람직하지 못함.  

부모 클래스 생성자를 호출할 때 super(...)를 한다.  
부모 클래스의 멤버 변수/함수를 호출할 때 super.<...>를 한다.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/b24ad96c-275b-4764-aca7-2027c80ab85f)  

완성된 상속 코드  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e5ac1b55-5837-4364-aa37-f067d69a04f0)  


## 부모 클래스의 독립성, 클래스 다이어그램  
자식이 부모를 호출할 수는 있지만, 부모는 자식 호출할 수 없음.  
전자는 부모를 특정할 수 있지만, 후자는 자식을 특정할 수 없으므로.  

여전히 Person 개체도 만들 수 있음.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d44a15d3-9d5a-48f3-b555-503896ca549e)  

super()는 무조건 첫줄에 해야함. 아랫줄에 하는 순간 부모 생성자 호출 안되서 컴파일 오류 뜸.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/24960404-d1b4-47c1-9109-25b0c5192117)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e2c3b55b-ad09-42c3-a142-2210ec031b61)  

새로운 접근 제어자  !!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/4dfc8dbc-1ac8-4d0d-b682-10fac34aaa82)  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/71be1068-f619-40f0-a86d-77b867214a82)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/291e52b3-01dc-4eab-8f3d-b1ff9020d99b)  

protected 접근제어자는 #으로 표현함.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/920345a2-b9b1-4908-97ef-7f3e37f7d044)  
* 문법상, 학생이 person의 email에 접근할 수 있게 됨... 다만 설계를 안했을 뿐.  


![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/379904e3-a85d-4e80-a19d-257e6dcbdd2b)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/338faa04-fa07-49b9-8941-2b25bf8939bf)  

quiz  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/95ebddf5-375f-4a3f-a124-151fbc481d74)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/626eb67b-53b3-4758-905e-cbb64d0b7d42)  


## 상속의 상속 
선생을 전임 강사와 시간 강사로 나누자.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/7e64881b-2e47-48b4-98f3-4fb4adb38c84)  


## is-a, has-a 관계  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/39987819-69d9-44fc-8ee1-7d7e32de7e24)  
has-a 관계 : composition 관계. 부품 관계. waterspray가 head, body가지는 것.  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/28d56e3c-3e42-4ed5-be5b-90aff8ac6c7c)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/20593f0f-19eb-4e6d-81fc-865e9124b643)  


## is-a 관계와 부모형 변수
``` java
Student student = new Student("Leon", "Kim");
Person person = student;
// 컴파일 됨
```
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/df81fa22-3218-48a7-9297-aabdfec8378a)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/81d8690f-cbed-49b0-967a-7a074f960883)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/06714625-cc7c-4ecc-a51b-f22e50c9aecd)  
이건 컴파일 안됨.  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e3a35a6e-db21-492c-894f-495e98c8798f)  
person이 학생인지 선생인지 알 수 없다. 따라서 허용 안함. 컴파일러가 막음.  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/6bf8d120-4a65-4047-b90e-5264ce7baeba)  

* 자식을 부모에 대입한 뒤, 부모에서 자식의 메서드 호출은 될까?  
``` java
Student student = new Student("Leon", "Kim");
student.setMajor(Major.INFORMATION_TECHNOLOGY);
Person person = student;  // 형 변환, casting임
person.getMajorOrNull();  // 자식의 메서드 호출
// 앞과의 같은이유로 컴파일 안됨 !!
```

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c0e5fc7b-8308-4519-bee3-2bd526fc2252)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/25b73df8-6cfb-47f2-947e-c6a4376a2b87)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/9284f15d-de56-4cff-8b5d-36b2ce6e0d79)  
부모를 자식으로 캐스팅 후 호출. 컴파일 잘됨.  
근데 ... ?  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/8691416f-1f83-4438-9fa5-85ca8ecc0a34)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/b03c3910-f88a-47b3-89cd-13b3fc88b18e)  

수직으로는 되지만, 수평으로는 안됨.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/0dbef040-f7e3-4374-be55-6db43241250e)  
컴파일러가 잡아주는 경우가 있으나, 예외가 있어서 런타임 오류 생길 때도 있음.  
부모로 둔갑해서 형제 개체로 형변환 하려는 경우.  

## instanceof 연산자
예외를 피할 수 있으면 그러는 게 좋은 습관임.  
예외 처리 없이 해결하는 법 배우는데, 다형성을 배우고 나면 이렇게 할 경우 별로 없다고 함...  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/36f7f341-71d3-4d37-b7a1-6010c6510bce)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/058446dc-2fcf-4166-b84d-0aa7121763f7)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/58719a57-d3ee-4651-a1c1-df5a9fe4f167)  

그런데, instanceof연산자는 반드시 특정 클래스의 인스턴스인지 확인하는게 아님. !!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/f4e8feca-4bae-4516-9372-7b0c4a422a04)  
수직 관계 전부다 맞다고 판단해버림.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/74d0b32c-9a35-442f-b1f6-40bc600f4480)  


## 클래스 정보와 Object 클래스
getClass() 메서드  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/9e672dd3-4a5c-4869-838c-d23d942e9458)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/89b11692-889a-4cf6-8c69-219a5b405af4)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/42fc4341-2c18-430d-a657-aff38ec0df7d)  

언제 쓰나?  
getClass(): 클래스 이름 찾을 때, 클래스 안의 메서드나 멤버 변수 등도 찾을 수 있음.  
getClass().getName()은 정말 많이 씀 (ex: log메시지를 출력할 때)  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/89a11684-54e2-46b5-a145-1e59ffecf6d3)  


근데, 이런 내가 작성 안한 코드는 어디서 가져온거지 ? !!  
어딘가에서 상속한 것임 !!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/48f86e7b-1ba2-4d8c-8b85-b3551d34a9ba)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/901afbd3-3a00-4613-b749-71fd3c602a0a)  

```java
// BaseEntity.java
package academy.pocu.comp2500samples.w05.baseentity;

import java.time.OffsetDateTime;
import java.util.UUID;

public class BaseEntity {
    private UUID id;
    private OffsetDateTime createdDateTime;
    private OffsetDateTime modifiedDateTime;

    public BaseEntity(UUID id, OffsetDateTime createdDateTime, OffsetDateTime modifiedDateTime) {
        this.id = id;
        this.createdDateTime = createdDateTime;
        this.modifiedDateTime = modifiedDateTime;
    }

    public UUID getID() {
        return this.id;
    }

    public OffsetDateTime getCreatedDateTime() {
        return this.createdDateTime;
    }

    public OffsetDateTime getModifiedDateTime() {
        return this.modifiedDateTime;
    }

    public void setModifiedDateTime(OffsetDateTime modifiedDateTime) {
        this.modifiedDateTime = modifiedDateTime;
    }
}


// Course.java
package academy.pocu.comp2500samples.w05.baseentity;

import java.time.OffsetDateTime;
import java.time.ZoneOffset;
import java.util.ArrayList;
import java.util.UUID;

public class Course extends BaseEntity {
    private String courseCode;
    private String title;
    private ArrayList<CourseTerm> courseTerms;

    public Course(UUID id,
                  OffsetDateTime createdDateTime,
                  OffsetDateTime modifiedDateTime,
                  String courseCode,
                  String title) {
        super(id, createdDateTime, modifiedDateTime);
        this.courseCode = courseCode;
        this.title = title;
        this.courseTerms = new ArrayList<>();
    }

    public String getCourseCode() {
        return this.courseCode;
    }

    public String getTitle() {
        return this.title;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    public ArrayList<CourseTerm> getCourseTerms() {
        return this.courseTerms;
    }

    public void setCourseTerms(ArrayList<CourseTerm> courseTerms) {
        this.courseTerms = courseTerms;
    }

    // helper methods
    public void addCourseTerm(int term) {
        CourseTerm courseTerm = new CourseTerm(UUID.randomUUID(),
                OffsetDateTime.now(ZoneOffset.UTC),
                OffsetDateTime.now(ZoneOffset.UTC),
                this,
                term);

        this.courseTerms.add(courseTerm);
    }
}


// CourseTerm.java
package academy.pocu.comp2500samples.w05.baseentity;

import java.time.OffsetDateTime;
import java.util.ArrayList;
import java.util.UUID;

public class CourseTerm extends BaseEntity {
    private int term;
    private Course course;
    private ArrayList<Student> students;

    public CourseTerm(UUID id, OffsetDateTime createdDateTime, OffsetDateTime modifiedDateTime, Course course, int term) {
        super(id, createdDateTime, modifiedDateTime);
        this.course = course;
        this.term = term;
        this.students = new ArrayList<>();
    }

    public int getTerm() {
        return this.term;
    }

    public Course getCourse() {
        return this.course;
    }

    public ArrayList<Student> getStudents() {
        return this.students;
    }

    public void setStudents(ArrayList<Student> students) {
        this.students = students;
    }

    // helper methods
    public void addStudent(Student student) {
        this.students.add(student);
    }

    public int getStudentCount() {
        return this.students.size();
    }
}


//Student.java
package academy.pocu.comp2500samples.w05.baseentity;

import java.time.OffsetDateTime;
import java.util.UUID;

public class Student extends BaseEntity {
    private String name;
    private String email;
    private String nickname;

    public Student(UUID id,
                   OffsetDateTime createdDateTime,
                   OffsetDateTime modifiedDateTime,
                   String name,
                   String email,
                   String nickname) {
        super(id, createdDateTime, modifiedDateTime);
        this.name = name;
        this.email = email;
        this.nickname = nickname;
    }

    public String getName() {
        return this.name;
    }

    public String getEmail() {
        return this.email;
    }

    public String getNickname() {
        return this.nickname;
    }

    public void setNickname(String nickname) {
        this.nickname = nickname;
    }
}


// Program.java
package academy.pocu.comp2500samples.w05.baseentity;

import java.time.OffsetDateTime;
import java.time.ZoneOffset;
import java.util.UUID;

public class Program {
    public static void main(String[] args) {
        UUID id = UUID.randomUUID();
        OffsetDateTime now = OffsetDateTime.now(ZoneOffset.UTC);

        Student student1 = new Student(id,
                now,
                now,
                "Tom",
                "Smith",
                "tommy hammer");

        printStudentInformation(student1);

        id = UUID.randomUUID();
        now = OffsetDateTime.now(ZoneOffset.UTC);

        BaseEntity student2 = new Student(id,
                now,
                now,
                "Kevin",
                "Park",
                "KtotheP");

        // Compile Error!
        // printStudentInformation(student2);

        printStudentInformation((Student) student2);

        ((Student) student2).setNickname("KevinInThePark");

        now = OffsetDateTime.now(ZoneOffset.UTC);
        student2.setModifiedDateTime(now);

        printStudentInformation((Student) student2);

        id = UUID.randomUUID();
        now = OffsetDateTime.now(ZoneOffset.UTC);

        Course comp2500 = new Course(id,
                now,
                now,
                "COMP2500",
                "Java");

        id = UUID.randomUUID();
        now = OffsetDateTime.now(ZoneOffset.UTC);

        CourseTerm term202005 = new CourseTerm(id,
                now,
                now,
                comp2500,
                202005);

        comp2500.getCourseTerms().add(term202005);

        printCourseInformation(comp2500);

        comp2500.addCourseTerm(202009);

        printCourseInformation(comp2500);

        term202005.addStudent(student1);
        term202005.addStudent((Student) student2);

        comp2500.setTitle("Object Oriented Programming and Design (Java)");

        printCourseInformation(comp2500);
    }

    private static void printStudentInformation(Student student) {
        System.out.println("student:");

        printBaseEntityInformation(student);

        System.out.printf ("    name: %s%s",
                student.getName(),
                System.lineSeparator());

        System.out.printf("    email: %s%s",
                student.getEmail(),
                System.lineSeparator());

        System.out.printf("    nickname: %s%s",
                student.getNickname(),
                System.lineSeparator());
    }

    private static void printCourseInformation(Course course) {
        System.out.println("course:");

        printBaseEntityInformation(course);

        System.out.printf("    course code: %s%s",
                course.getCourseCode(),
                System.lineSeparator());

        System.out.printf("    title: %s%s",
                course.getTitle(),
                System.lineSeparator());

        System.out.println("    course terms:");

        for (CourseTerm courseTerm : course.getCourseTerms()) {
            System.out.printf("        term: %s%s",
                    courseTerm.getTerm(),
                    System.lineSeparator());
            System.out.printf("        # students: %s%s",
                    courseTerm.getStudentCount(),
                    System.lineSeparator());
        }
    }

    private static void printBaseEntityInformation(BaseEntity entity) {
        System.out.printf("    id: %s%s",
                entity.getID(),
                System.lineSeparator());

        System.out.printf("    created: %s%s",
                entity.getCreatedDateTime(),
                System.lineSeparator());

        System.out.printf("    modified: %s%s",
                entity.getModifiedDateTime(),
                System.lineSeparator());
    }
}
```
