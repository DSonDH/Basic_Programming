# Java 기본 문법
* 구조적(structured) 프로그래밍 요소  
object-oriented 요소가 아님.  
구조적 프로그래밍은 기계가 이해하는 방식으로, 모든 프로그래밍 언어가 구조적 프로그래밍 요소를 포함함.  

## 정수 자료형
![image](https://user-images.githubusercontent.com/15919242/235924410-79b74107-58d5-4e68-b04f-af1a82845692.png)  2의 보수법 사용.  
자료형 크기가 고정. 따라서 C의 sizeof()같은 키워드 가 없음.
!! 부호있는 자료형만 존재함.  
음수 나이, 음수 배열색인 같은 걸 예방하도록  
코드를 방어적으로 (함수 초반에 예외 처리 많이 필요) 해야함.  
![image](https://user-images.githubusercontent.com/15919242/235925448-f177e5a6-1a07-4b3a-84ee-7f48145da589.png)  
## char, boolean, String
16bit인 char.  
Java의 유일한 부호없는 자료형.  
표준은 정수형이라고 말함.  
그런데 유니코드의 최댓값은 U+10FFFF. 즉 char로는 모든 유니코드를 표현할 수 없음.  
Java 탄생 시 유니코드 최댓값이 U+10FFFF여서 역사적 한계를 가진 것.  

* boolean 형  
![image](https://user-images.githubusercontent.com/15919242/235926256-f7b38978-c4c8-4aa0-b39f-8c916ba6db79.png)  

* 기본 자료형은 모두 '값형'임 !!  
모든 값형은 복사 가능. 참조형은 그렇지 않음.  

* String 형 (클래스 형)  
![image](https://user-images.githubusercontent.com/15919242/235926556-44816d08-6c5a-449b-8523-dbabf081f134.png)  
![image](https://user-images.githubusercontent.com/15919242/235926690-5c800a03-882c-4b26-942d-019c6dc5b54b.png)  
![image](https://user-images.githubusercontent.com/15919242/235926755-ade9076d-cd03-4f01-9cba-3dde9b55ba3b.png)  

* ArrayList  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/54d0f76e-7fdd-498c-9dcd-912dcf4a4c14)  


## 리터럴
정수 리터럴  
![image](https://user-images.githubusercontent.com/15919242/235927410-10d0eac0-8c82-41a7-bb95-a8ac70507728.png)  
![image](https://user-images.githubusercontent.com/15919242/235927693-dbb992a1-f0f4-4659-95fc-3dca5654d5a6.png)  
01234는 1234(10)이 아니라 1234(8)이다. 리얼 뻐킹 페이크  

부동소수점 리터럴  
![image](https://user-images.githubusercontent.com/15919242/235928256-e8818377-8379-4750-9fe3-2955920cd71a.png)  

문자, 문자열 리터럴  
![image](https://user-images.githubusercontent.com/15919242/235928368-998dbb84-b387-48e3-9a5c-d9cef8385e46.png)  

기타 리터럴  
![image](https://user-images.githubusercontent.com/15919242/235928470-f7e5c5a6-1ef5-42ad-8082-87268aa17b1f.png)  
_ 위치는 내맘대로 아무데나 넣어도 됨. 

## final 키워드
Java의 상수형 변수: final 키워드로 만듦. 변수값 변경을 금지시킴  
1. 지역변수
2. 클래스 멤버 변수
3. 메서드 매개변수
4. 클래스와 메서드
이 네가지에 final 붙일 수 있음.  
![image](https://user-images.githubusercontent.com/15919242/235929222-50e5b287-dfa8-4e62-8954-1690f2854f53.png)  
![image](https://user-images.githubusercontent.com/15919242/235929250-2bb6646c-3a96-4ad6-b609-8408fd639f55.png)  

![image](https://user-images.githubusercontent.com/15919242/235929419-4ee35cef-01b6-4b43-a84b-9d56cb989360.png)  
![image](https://user-images.githubusercontent.com/15919242/235929491-ff7070a5-f826-403f-bdba-06d5ea6ae4f2.png)  
![image](https://user-images.githubusercontent.com/15919242/235929660-971adb52-de02-4b00-96db-19eabb11336f.png)  
final 변수의 초기화 2 예  
![image](https://user-images.githubusercontent.com/15919242/235929820-e2890c77-381a-4659-96e3-4687ed56f2d1.png)  

## 주석, 연산자 우선순위, 산술 연산자
한 줄 주석 : //  
여러 줄 주석 /* */  

Javadoc 주석 : 문서 관리할 때  
![image](https://user-images.githubusercontent.com/15919242/235930059-b50c2eef-86ba-4adf-a9fa-a223e87a9ae1.png)  
![image](https://user-images.githubusercontent.com/15919242/235930106-a1a476f8-c4bc-4ec1-b64f-937ce544a864.png)  
![image](https://user-images.githubusercontent.com/15919242/235930367-c091cc9b-4acf-403f-a645-5d0a6bc30d10.png)  
![image](https://user-images.githubusercontent.com/15919242/235930434-b5b75448-4ada-4a8d-9a19-749e390f37e7.png)  

연산자 우선순위  
![image](https://user-images.githubusercontent.com/15919242/235930595-2195cfbf-e726-46b8-afa9-4b50e9e505c1.png)  
![image](https://user-images.githubusercontent.com/15919242/235930709-e2a4a985-2eb3-46e7-87ac-0a321fd8817b.png)  
-> 연산자는 C의 의미랑 다름!  

산술 연산자  
![image](https://user-images.githubusercontent.com/15919242/235930822-8bff3806-311c-405e-9369-ee1eab927f40.png)  

## 대입 연산자, 논리 연산자, 캐스팅
대입 연산자  
![image](https://user-images.githubusercontent.com/15919242/235931027-89f673c2-04a3-4b90-896f-a150b070bf79.png)  
![image](https://user-images.githubusercontent.com/15919242/235931337-72f796b9-3186-4890-874c-9290f2c533cc.png)  

String과 대입 연산자  
![image](https://user-images.githubusercontent.com/15919242/235931526-12c3eb2c-9f7a-4e56-87b8-2e80d8f7d21f.png)  
같이 Mumu가리키다가 아예 Nana로 다른 메모리 가리키게 됨.  
![image](https://user-images.githubusercontent.com/15919242/235931793-15acca43-ecda-46bd-849c-c65e73deefd7.png)  

자료형 변환  
![image](https://user-images.githubusercontent.com/15919242/235931929-1e6c8464-b550-4175-b936-7a7fc97521a4.png)  

논리 연산자  
![image](https://user-images.githubusercontent.com/15919242/235932053-2c212165-0e78-4404-a76c-6d97c3c02da1.png)  
short circuit도 있음.  

== 연산자와 문자열  
```java
String name1 = "Nana";
String name2 = "Nana";
String name3 = new String(name1);
String name4 = new String("Nana");

boolean isSame1 = (name1 == name2);
boolean isSame2 = (name1 == name3);
boolean isSame3 = (name1 == name4);
boolean isSame4 = (name1 == "Nana");

/* The answer is ...
true
false
false
true
*/
```
문자열은 참조형 !  
![image](https://user-images.githubusercontent.com/15919242/235934003-b8017449-b955-4db9-b6a7-309edbcda823.png)  
근데 주소를 공유하는 경우가 있음.  
![image](https://user-images.githubusercontent.com/15919242/235934038-0d78fe23-69f4-4d23-9d71-16a3a8b87270.png)  
new로 생성안한 문자열은 공유하도록 최적화 함.  

## 문자열 비교
문자열의 주소가 아닌, 문자 내용 자체를 비교하고픔.  
equals() 메서드 써야함.  
![image](https://user-images.githubusercontent.com/15919242/235934454-b1b6c14f-5862-47a2-bcd3-7542a1801748.png)  

연산자 오버로딩?  
함수 오버로딩와 유사한 개념.  
피연산자의 자료형에 따라 연산자의 동작을 바꾸는 것.  
ex: 같은 + 연산자지만 숫자 + 숫자 / 문자열 + 문자열 등등 동작이 다르다!  
자바에서는 지원 안한대 ...  
예외 딱 하나 : String용 + 와 += 연산자.  
프로그래머가 자체 제작한 클래스에서는 사용 불가.  
다행히도 메서드 오버로딩은 지원함.  
![image](https://user-images.githubusercontent.com/15919242/235935442-0bd97b17-032c-428b-9ad0-613776a17769.png)  

Jave의 문자열 비교 베스트 프랙티스  
문자열이 참조형이란 사실을 잊지말것!  
==를 쓰지 말 것!  
그 대신 equals() 메서드를 사용할 것!  

bit shift 연산자  
![image](https://user-images.githubusercontent.com/15919242/235935828-ea601aa7-dae2-441c-bb7a-4844e0e41b2d.png)  
![image](https://user-images.githubusercontent.com/15919242/235935936-7af57f26-4980-4ecb-b28d-3092090e1400.png)  


## 조건문
if문: 알던대로!  
![image](https://user-images.githubusercontent.com/15919242/236215309-f49bb0c9-4d10-45a9-91c5-3745f15ca3ad.png)  

switch case문  
![image](https://user-images.githubusercontent.com/15919242/236215470-4cec1604-e00c-4e99-aef0-08b3fa818787.png)  
C랑은 다르고, C# 이랑은 같은 부분: case에 사용 가능한 자료형!  
![image](https://user-images.githubusercontent.com/15919242/236215555-75da6c32-b6aa-4430-8260-625bdaab131d.png)  
intentional fallthrough도 되서 C랑 비슷, C#이랑은 다름. C#은 컴파일 오류.  
case문 마다 미리 break;를 넣는 습관 들이기 !!

## 반복문

for loop, while loop  
![image](https://user-images.githubusercontent.com/15919242/236216660-b25c2566-b0c6-44c6-a31f-cfca89ccd527.png)  
![image](https://user-images.githubusercontent.com/15919242/236216836-40f5b0e8-760c-43e9-ba3f-6f1cd06d0190.png)  

goto문 비슷한게 Java에 있음  
break <라벨이름>;  
![image](https://user-images.githubusercontent.com/15919242/236217050-43e9c8c6-1bbc-4d17-b789-60a24a305886.png)  
![image](https://user-images.githubusercontent.com/15919242/236217190-1b328f88-c45c-4256-bd8d-fef7f9399e15.png)  
![image](https://user-images.githubusercontent.com/15919242/236217333-a11ed108-1c8d-4070-a137-7225db01a761.png)  

continue 역시 라벨 사용 가능.  
![image](https://user-images.githubusercontent.com/15919242/236217706-4de7c4b0-2e08-4e7b-a580-a2665990a115.png)  

foreach 스타일 for문  
![image](https://user-images.githubusercontent.com/15919242/236217842-37bed3bd-a0ee-49f6-bc6e-d7e2b31e28f6.png)  


## 참조형 인자, 열거형

함수  
![image](https://user-images.githubusercontent.com/15919242/236218126-a3e9ea42-b4f6-41c1-8283-fc244076ec24.png)  
Java에서는 모든게 포인터!  
![image](https://user-images.githubusercontent.com/15919242/236218847-d1c27ce0-0287-406d-b5a7-40cbda76e9c1.png)  

final 참조형 매개변수  
![image](https://user-images.githubusercontent.com/15919242/236219232-6e400ef9-592a-4333-95d7-a8bb255bb2c5.png)  
![image](https://user-images.githubusercontent.com/15919242/236219330-76bbc7c0-95b4-4d63-b456-97bfc4adcbf4.png)  

1차원 배열 예  
![image](https://user-images.githubusercontent.com/15919242/236219438-74e1e958-dec5-484b-a9f6-d558931320e3.png)  
![image](https://user-images.githubusercontent.com/15919242/236219469-b3bdb044-9f5d-45db-89d9-5dc2f23b8fac.png)  
new String[10] 하면 참조형이므로, string 개체를 담을 수 있는 공간을 10개 만들어 줌. 실제로 string 10개를 넣어주지 않음.  실제로 들어가는건 Null 10개. 실제 값 넣으려면 for loop 돌면서 인덱스 별로 넣어줘야 함.  

다차원 배열 예  
![image](https://user-images.githubusercontent.com/15919242/236220250-cab1f827-6a34-4776-8d0d-2994b98702e6.png)  
![image](https://user-images.githubusercontent.com/15919242/236220338-9df5c1fc-7449-4621-8779-d0853f0727db.png)  
Java는 다차원의 배열, 배열의 배열 문법적으로 구분은 안하고 있음.  

열거형  
![image](https://user-images.githubusercontent.com/15919242/236220644-4517576a-bfff-4a57-be88-64bffca07fce.png)  

Java 열거형에서 못하는 것.  
![image](https://user-images.githubusercontent.com/15919242/236220856-c261497b-f8c3-41a5-ad27-5a53ceb8f94f.png)  
![image](https://user-images.githubusercontent.com/15919242/236221402-fdd8a766-8b73-451b-ab4b-ac41c81fb373.png)  
정수형이 아니므로. 클래스이므로... 마지막에 ;도 찍어줘야 함.  
![image](https://user-images.githubusercontent.com/15919242/236221638-9c1507a3-4a28-4d02-9983-7a15a6fe9e2d.png)  

![image](https://user-images.githubusercontent.com/15919242/236221780-d30f5f58-000d-4b58-83b9-08dc6f9f220f.png)  
![image](https://user-images.githubusercontent.com/15919242/236221846-647afbab-15a8-421a-8590-0f1b1e4c5a08.png)  
![image](https://user-images.githubusercontent.com/15919242/236222068-f9d4ae44-641a-44db-b717-da5b5f1ad464.png)  

열거형의 메모리 위치  
자바에서 열거형은 일종의 클래스이고, 상수 하나 당 인스턴스를 하니씩 만들어 public static final 필드로 공개한다.  
또한 열거타입의 인스턴스는 클라이언트가 직접 생성할 수 없고, 인스턴스는 런타임에 단 한번만 생성된다.  
이런 특징으로 Singleton을 보장할 때 사용되기도 한다.  

JVM의 메모리 영역은 크게 메소드 영역, 힙 영역, 스택 영역으로 나뉜다.  
메소드 영역 : class, class variable(Static Variable).  
따라서 열거형 클래스도 메소드 영역에 올라감.  
힙 영역에는 개체 인스턴스가 올라감.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/f071e23a-afa0-4b75-af35-48409aaa5f69)  
그런데 
```Java 
Week holiday = Week.MONDAY
```
처럼 열거형 변수가 열거 개체를 참조하면 ?  
스택 영역은 메소드가 호출될 때 그 메소드와 관련된 로컬변수와 매개변수가 저장되는 곳.  
메소드 영역에서 주소값만 복사해서 결국 같은 열거형 개체를 가리킴.  
```Java 
System.out.println(holiday == Week.MONDAY) // true
```

var  
![image](https://user-images.githubusercontent.com/15919242/236222159-3741514c-e8f6-4e0b-8fa7-165941e08be0.png)  

var 사용 시 주의점!  
![image](https://user-images.githubusercontent.com/15919242/236222327-841e677e-796e-4d96-ad18-a64ac9eb14eb.png)  


## 람다  
![image](https://user-images.githubusercontent.com/15919242/236223252-a02b2e79-ac93-4626-b366-0c4d6dabe53c.png)  
이름없는 함수를 한번 쓰고 버린다는 개념.  
가독성 해치긴 함.  


## 모듈  
기본 방식 : 패키지  
패키지 방식의 제약점(런타임 크기가 너무 커지는)을 보완하는. 효율적인 관리 및 배포에 좋다네  
![image](https://user-images.githubusercontent.com/15919242/236223992-7ef14a4b-e97f-4823-b50e-9b27134a3db4.png)  
기존 패키지 시스템의 한계 1.  
![image](https://user-images.githubusercontent.com/15919242/236224696-de4b9c57-5f49-4864-bc0f-cf75fb6915d1.png)  

한계 2.  
![image](https://user-images.githubusercontent.com/15919242/236225149-e9df4352-549c-4d80-8893-cfe8b10a9d7e.png)  

새로운 방식 : 모듈  
![image](https://user-images.githubusercontent.com/15919242/236225212-bba9e820-879e-4815-84fa-2b691c8f9529.png)  
패키지 위에 새로운 그룹(초록색)을 만듦.  

![image](https://user-images.githubusercontent.com/15919242/236225374-d290b5d9-1da3-42aa-a4b5-176ccfdc741f.png)  
module-info.java 안에 어떤걸 필요로 하는지 등등 정보를 넣어둠.  
모듈의 이름은 패키지와 마찬가지로 중복을 피해야 함.  
여러 단어로 이룽어진 경우, 점(.)을 찍음. 단어 별로 폴더를 만들지 않음!  

module-info.java  
![image](https://user-images.githubusercontent.com/15919242/236227414-713f851c-1eb3-4f18-82b9-872803fa89be.png)  
![image](https://user-images.githubusercontent.com/15919242/236227666-a86f8041-06ef-4d50-82a8-9791e994bf79.png)  


