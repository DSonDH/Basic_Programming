# Interface
인터페이스의 뜻 : 두 물체나 공간 사이의 경계  
-> 
사용자가 스위치를 보면 누르면 되겠다고 생각할 수 있음.  
사용자는 본인에게 익숙한 공간에서 지시한다.  
실제 동작은 구현 공간에서 일어난다. 사용자는 구현 디테일을 알 필요가 없다.  
나는 뭔지 모르지만 호출할 수 있고, 어떤 결과가 나오는지 아는 것. 프로그래밍에서 함수와 같음 !  
함수는 블랙박스라서 그 안에 구현은 몰라도, 반환형은 알 수 있음.  
함수 시그내처를 인터페이스라 부르기도 함.  
컴퓨터 분야에서 인터페이스는 더 다양한 의미가 있음.  
C에서 함수 선언이 함수 시그내처, 함구 구현은 어딘가 따로 있었음.  
C에서 함수 포인터 매개변수는 시그내처만 지정해서 어딘가 구현된곳에 구멍을 연결하는 방식이었음.  
Java에서는 아래와 같이 썼음.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/eda5e0d4-353a-40cd-9986-3becc0b13bfd)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e4c373c7-76c8-44c2-80c2-ed97bd728518)  
C와 Java의 차이점. 하지만 다음과 같은 방법으로 해결 가능함.  
동작만 떼어내서 구현을 강요하는 것!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/4057f225-2ec6-4a4a-8742-463e5a2f5c32)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/ccd99f67-9a32-446b-a7c3-ddcf277ea417)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/0cfc4c60-2136-4c54-9363-04ea13f555b1)  

개체지향에서 인터페이스라고 하면 순수 추상 클래스를 말하는 것.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/a5d56918-44a8-4ec7-9cbc-8f49da6172bc)  
Java와 C#은 이 특별한 클래스를 위해 interface란 키워드를 지원함.  
C++은 별도의 키워드가 없어서 추상클래스를 사용해야함.  

## 인터페이스는 순수 추상 클래스
* 어떤 상태도 없음
* 동작의 구현도 없음
* 동작의 시그내처만 있음
* 이런 특징 때문에 클래스하고는 약간 다른 규칙을 따름

추상클래스를 인터페이스로 바꾸기.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/46298c09-20c7-4ae9-8547-adef45fb9fe0)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/35b84c67-bc0a-4a14-a6ca-0cbddbb54bad)  
확장(override)의 개념이 아니라, 없는 구현을 이제서야 구현하는 거니까 implement라고 키워드 이름 지음.  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d5950de7-17f1-4231-bc47-9bf2dcde2d27)  
인터페이스는 앞에 무조건 i를 붙이자.  

## 인터페이스 미구현과 컴파일 오류
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/33f35d88-ca7b-45ca-b7a0-5d02d4533866)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e0bcf1d6-f2c5-43de-96db-656f5c5d0b73)  

미구현으로 인한 컴파일 오류는 실수를 방지함.  
오버라이딩망 쓰는 경우에, 실무에서 실수를 많이 하더라..  
1. 상속받은 메서드를 구현할 때 메서드 이름에 오타를 내서 구현이 안덮어써지는 경우.  
2. 부모 클래스의 메서드 이름만 바꾸고 자식 클래스는 손 안대는 경우.  
모두 아무 문제없이 컴파일 되므로 잘못된걸 깨닫기 힘들다 !!  

## Java 어노테이션
실수를 막기 위해 무조건 interface로 쓰면 ... 안됨!!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/cf8344af-0193-42d2-89ee-92f3816b253c)  

Java에서는 annotation으로 해결함  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/111d051a-b173-4a10-be9b-75310570c042)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/397e7f3c-efd4-4209-ae29-743e312615dc)  

@Override는 override안하면 컴파일 오류 뜸.  
프레임워크에서 저런거 쓰긴 함. 프로그래머가 원하는 방식대로 꾸밀 수 있음.  

## 인터페이스의 접근 제어자
왜 인터페이스는 public 메서드만 가능할까?  
C의 헤더파일과 비슷하다고 보면 됨. C의 헤더파일에 들어간 거는 거의 모두 전역함수니까.  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/07f7bf0a-91fe-4bac-8945-b2b2ea29b2fc)  
접근제어자 생략하면 패키지범위인데, 여전히 구현 클래스에서 인터페이스의 메서드는 모두 다 public.  
interface형 그 자체를 외부 패키지에서 사용 못하는게 전부임.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/fdefbca4-1e4b-46f9-a4ed-6b609ff17f60)  
외부에서 임포트 할려고 하면 컴파일 오류.  
Iloggable개체를 외부에서 호출하려고 하면 안되는데, 그 내부의 log메서드는 public이라서  
Iloggable을 상속받은 ConsoleLogger가 log를 호출하면 그건 가능함.  

* 인터페이스의 이름
I를 앞에 붙이는 이유 : 클래스와 구분지으려고!
인터페이스 이름 뒤에 -able을 붙이기도 함. 적절해보이면 붙이자  


## 여러 인터페이스 구현하기
Java에서 다중상속은 안되지만, Interface 다중상속은 됨 !!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e7914f08-2326-4e12-a3d9-ad86e413d085)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/0cd63777-b87a-413c-a688-711cebb270d0)  

왜 인터페이스는 다중상속 허용함 ?  
다중상속은 상태와 메서드 구현이 중복되서 누구를 구현해야할지 애매해지는 경우가 문제인 거였음.  
인터페이스는 그럴 걱정 없음 !  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/b5c8e0a8-f83b-47a2-a644-3245278289fa)  
어차피 구현은 내가 하나만 해줄거니까 !!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/abc41b7a-0fe8-4183-bef5-61e14fce5428)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c2320d6a-cfc1-462e-bd64-b24acc9e2305)  

## 인터페이스와 다중 상속
어떻게 상속해도, 인터페이스의 구현은 하나뿐!  
인터페이스 구현은 클래스에서 생기고, 클래스는 다중상속이 불가능 하므로,  
한 클래스 안에서 그 인터페이스 구현은 딱 하나만 존재함.  
상속받은 메서드가 인터페이스하고 같아도 마찬가지.  
예시  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/7c8ae6ba-67f5-44af-a960-99b06281269f)  
ExtendedConsoleLogger는 ConsoleLogger를 상속받아서 overriding한거기도 하고,  
Ireportable을 구현한것이기도 함.  

그래서 인터페이스는 다중 상속의 해결법. 다중 상속을 흉내낼 수 있으므로.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/5dd69e6d-6012-478f-ad9e-cb6446f3d75c)  
vs  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/a00ec420-0018-4dd3-93a0-4f0f2fb6718b)  
여전히 구현은 여러번 해야하고, 코드 중복은 있지만,  
다형성은 사용할 수 있다는 장점이 있음.  

정리 : 인터페이스의 실무에서 핵심적인 용도 
1. 함수 포인터처럼 사용함
2. 다중 상속을 흉내 내는 방법
* 핵심은 다형성임!  

코드보기 : Widget(GUI중 하나로, 정보를 보여주거나 상호작용할 수 있는 방법을 제공하는 것.  
아이콘, 버튼 창 등등)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/f8569cbc-eeb8-4140-bbf8-b3d2056a70a5)  

* Object.clone()
Java에서 클래스형은 다 참조형.  
단순 대입으로는 복사가 안일어남.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/6875f9e5-e143-46b8-9383-a3c380eec72d)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/307e3a0a-8d7a-4e5c-a177-463754a80066)  

제대로 복사하는 방법  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e270e433-8999-435a-bd10-da8073ca01af)  
clone 호출하면 자바가 알아서 복사해준다.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/22dba472-c1f4-40a8-9cfe-9923bb0788f4)  
멤버들 중에 값형으로 반환되는건 괜찮은데, 참조형이면 서로 공유하게 되므로, 또 문제 생길 수 있음.  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/1fbdfeba-de91-4aef-8b32-43ec46276954)  

얕은 복사로 인해 문제가 생기는 경우  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/cce57a12-dd34-4113-9d5e-ef2d7df4fbf3)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/11cd1379-e9cb-4fe5-82f7-08a4c6260ae2)  

깊은복사 할려면 어떻게 해야할까 ?  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/129fc41c-ad1d-4b96-9adc-875632bee656)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/6146a727-2d8b-4bcd-8e21-6ded0692d835)  
물론, head 내에도 다른 참조형 있으면 따로 처리해줘야겠지?  

위 방법은 공식적인 복사방법. 실수하기 쉬움.  
복사 생성자라는 방법이 있음. 다른 언어(C++)에서 쓰이던 방법들임.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/382f7992-21bb-4451-89cc-8adb0ec695a2)  
this로 다른 생성자를 호출하는 방식임 !!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/33e8a6b4-619c-4b1f-8759-6215d6302066)  
진정한 깊은 복사는 Point 클래스의 복사 생성자를 사용함.  
이거 시험에 나올거같당.  


## 구체클래스 vs 인터페이스
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/1cf792a4-2c4a-4c28-8d20-157576faa527)  
이거랑 abstract class랑도 비교해서 정리하기.  
