# Java
1991년 첫 등장. 썬 마이크로시스템즈의 제임스 고슬링과 동료들이 개발.  
원래 목적 : 임베디드 시스템에서 사용하기 위해 한 번만 빌드하면 어떤 플랫폼에서든 작동하는 언어를 만들게 됨.  
그러다가 갑자기 고속 성장하던 언터넷에 맞춰 그쪽으로 방향을 바꾸며 대중화됨.  
가장 많이 쓰이는 매니지드 언어 -> 메모리 관리를 덜 신경 써도 됨.  
따라서 기계와 아주 가깝지 않은 개념을 코드로 옮기기에 적합.  

# Java 기본 문법

## 메인 함수
```java
// HelloPocu.java
package academy.pocu;

public class HelloPocu {
    public static void main(String[] args) {
        System.out.println("Hello POCU");
    }
}
```  
![image](https://user-images.githubusercontent.com/15919242/235670852-493a6633-c83e-4ffd-8cbc-5758a83f7875.png)  
C에는 없는 개념. java에서는 언제나 클래스가 필요함.  
모든 멤버변수, 함수는 class 안에 있어야 함. class 밖에 선언하는 것은 유효하지 않음.  

* 최고 레벨의 public 클래스는 하나만 있어야 함.  
![image](https://user-images.githubusercontent.com/15919242/235671165-a4880273-0ad2-4227-85a0-a1ac5d3bc3e4.png)  

* 내포 클래스  
![image](https://user-images.githubusercontent.com/15919242/235671293-4812e90b-0736-4a38-87fa-779505fb0a81.png)  
클래스 안에 다른 클래스를 넣을 수 있음. 안에 있는 클래스는 내포(nested) 클래스라 부름.  
중첩 클래스, 내부 클래스라고도 부름. 이때 내포 클래스는 public이어도 됨.  

* main함수  
프로그램의 시작점(entry point)  
반드시 signature대로 main함수를 만들어야 함. 안그러면 실행 시 main 못찾는다고 오류 발생.  
```java
    public static void main(String[] args) {
    // 커맨드 라인으로부터 받은 인자가 문자열 배열로 args로 들어옴.
        ...
    }
```

## 출력문과 가변 인자
```java
System.out.println("Hello POCU");
System.out.println(12345);
System.out.println(3.14);
System.out.println("Your score is" + 100);
// System은 class
// out은 System 클래스의 static 멤버 변수
// println은 정적멤버변수인 out의 메서드 중 하나
// 다양한 타입을 출력할 수 있음. 함수 오버로딩으로 가능함! 
// 입력변수 타입따라 호출되는 함수가 다른것임. 함수들의 이름은 같지만 매개변수 타입이 다르게 미리 정의된 것.
```
standard output으로 한 줄을 출력하는 함수.  
문자열 뿐만 아니라 숫자도 출력 가능  
print()라는 함수도 있는데, 이는 C#의 Write()함수와 유사함. 새줄로 안바뀜.  
![image](https://user-images.githubusercontent.com/15919242/235675369-14a0e47d-b64a-442b-85b1-2abd45326995.png)  

java에도 printf()가 있음!  
![image](https://user-images.githubusercontent.com/15919242/235675911-45201100-a670-4f1e-9a71-744a0fe635d0.png)  
원래는 println()만 있다가 나중에 추가된 메서드. C의 printf()처럼 포맷팅 가능.  
printf() 대신 format() 메서드를 사용해도 동일하게 동작.  
서식 문자는 C언어 메모를 참고할 것.  

올바른 새 줄 문자 추가 방법  
그냥 \n하면 안될 수 있음.  
![image](https://user-images.githubusercontent.com/15919242/235676480-7ae3173e-317a-4d0d-8816-bc22c36d23c7.png)  

가변인자
```java
public PrintsStream printf(String format, Object... args);
```
```java
String name = "Mumu";
int score = 65;
System.out.printf("%s's score: %d", name, score);
//C의 가변인자 함수와 비슷
```
![image](https://user-images.githubusercontent.com/15919242/235677155-e23cc583-5a39-461f-97ec-1464520c19d4.png)  

## 패키지
```java
package <패키지 경로>;
package academy.pocu;
```
연관된 클래스들끼리 묶는 기법.  
마치 디스크 상의 폴더와 같은 역할.  
'사진' 폴더는 사진 파일을 저장, '동영상'폴더는 동영상 파일을 저장.  

패키지 종류
1. 자바 기본 (build-in) 패키지  
  이름이 java로 시작하는 패키지들  
  java.lang, java.util, ...  
2. 프로그래머가 직접 만든(user-defined) 패키지  

패키지의 목적: 이름 충돌 문제를 피할 수 있게 해준다 !!!  
![image](https://user-images.githubusercontent.com/15919242/235678681-49da83e3-ae6f-4605-a3f7-b90c84095fd0.png)  

패키지 이름 짓기  
![image](https://user-images.githubusercontent.com/15919242/235678820-c135fff3-66e6-4d0a-9aee-84fde9bbee87.png)  

주의: 패키지 이름만 적으면 안됨!  
![image](https://user-images.githubusercontent.com/15919242/235679132-cb641833-494a-432f-90cc-8d77edbc993a.png)  
public class HelloPocu 클래스가 src안에 academy안에 pocu안에 있다는걸 말해주는 것임.  
패키지명과 똑같은 폴더 트리에 .java파일을 넣어야 함.  
IDE사용하면 알아서 해준대...  

폴더구조 정리  
![image](https://user-images.githubusercontent.com/15919242/235680004-b0bf2625-de6c-40c1-9419-74d7ca733e64.png)  

java vs C# vs C  
![image](https://user-images.githubusercontent.com/15919242/235680286-96c9a4bc-f444-4fb7-949e-469dbecd9328.png)  

## 빌드 및 실행
기본은 커맨드 라인 명령으로 빌드 함.  
![image](https://user-images.githubusercontent.com/15919242/235680799-3dfc0801-4337-40be-a259-c908cfaf7ffb.png)  
class폴더에는 compile된 결과물이 들어간대.  

``` hellopucu>javac -d class\ src\academy\pocu\*.java```  
이 명령어 치면 컴파일한 java클래스의 패키지 이름과 동일한 폴더들이 class 폴더 밑에 생성됨!  
![image](https://user-images.githubusercontent.com/15919242/235681822-88697209-2e14-4c7a-8b50-0bc2504d6ef4.png)  
그리고 그 안에 HelloPocu.class라는 파일이 생김.  

javac 명령어  
java compile  
![image](https://user-images.githubusercontent.com/15919242/235681992-b476bedc-bc5c-4fcb-94c2-75762d9bc16f.png)  
.java파일과 .class 파일이 동일한 폴더 구조를 따름.  

프로그램 실행하기  
```java -classpath D:\hellopocu\class\ academy.pocu.HelloPocu```  
java 명령어  
![image](https://user-images.githubusercontent.com/15919242/235684049-93fdfd64-57be-4872-9d81-bd6e2f99546a.png)  
main이 없으면 main 못찾는다고 컴파일에러 뜸.  

java 명령어의 -classpath 옵션  
![image](https://user-images.githubusercontent.com/15919242/235684250-a6657b2b-8f69-4e0a-949e-30f4056860d2.png)  

흔히 하는 실수 : 클래스명 앞에 패키지 누락  
![image](https://user-images.githubusercontent.com/15919242/235684426-1889364e-323e-4194-ad37-832c40253b59.png)  

배포하기  
내가 만든 라이브러리나 프로그램을 배포하는 방법  
C#의 경우 라이브러리 : .dll파일을 만듦, 프로그램: .exe파일을 만듦.  
java의 경우 : 두 경우 모두 .jar파일을 만듦.  
![image](https://user-images.githubusercontent.com/15919242/235686009-431c0a28-c8e1-4515-870a-f29b7ae5220c.png)  

jar 명령어  
![image](https://user-images.githubusercontent.com/15919242/235685138-22365bdd-d8cd-4dc4-8718-4098ce4f157b.png)  
정상적으로 명령어가 실행되면, .jar파일이 생성됨.  

jar 파일은 .zip파일임. .jar파일 내부를 보면 META-INF\MANIFEST.MF라는 파일이 있음.  
.jar를 만들 때 자동으로 같이 생성되는 파일임.  

Manifest파일?  
자바 애플리케이션의 정보를 담고 있는 메타데이터 파일.  
.jar파일을 만들 때 이 파일을 같이 넣어줄 수 있음.  
.jar파일의 시작점 (main함수)에 대한 정보를 넣어야 함.  
그 외에 여러 정보를 담을 수 있는데, 직접 찾아볼 것.  

![image](https://user-images.githubusercontent.com/15919242/235687046-b8d73165-4262-49e7-ba57-029d54601263.png)  
![image](https://user-images.githubusercontent.com/15919242/235687111-1ba6628f-0ffe-4201-924b-e4518878e6d6.png)  
![image](https://user-images.githubusercontent.com/15919242/235687194-070fa98e-08e9-4963-8da0-1d60bd6485de.png)  



## 패키지 사용하기

## 정수 자료형

## char, boolean, String

## 리터럴

## final 키워드

## 주석, 연산자 우선순위, 산술 연산자

## 대입 연산자, 논리 연산자, 캐스팅

## 문자열 비교

## 조건문

## 반복문

## 참조형 인자, 열거형

## 람다

## 모듈
