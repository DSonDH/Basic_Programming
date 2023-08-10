# 다형성, polymorphism이란
* poly(많은) + morph(형태가 변하다) : 어떤 개체가 다양한 형태로 변하는 능력  
* 같은 지시를 내렸는데, 다른 종류의 개체가 동작을 달리하는 것.  
* 어떤 함수 구현이 실행될지는 실행 중에 결점됨(late binding).  
* 부모 개체에서 함수 시그내처 선언, 자식 개체에서 그 함수를 다르게 구현  
* 실용적인 용도 : 다른 종류의 개체를 편하게 저장 및 처리 가능.  

예시 :  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c0c17304-2ad3-4190-9d65-b5bbc04f5f63)  
실제 개체 자료형에 있는 shout()를 호출함 !  
부모 개체를 만들어도 자식 클래스에 같은 시그니처의 메소드가 있으면 그게 호출되버림.  
즉, 같은 시그니처의 메서드는 무조건 가장 낮은 자식께 실행됨.  

다형성이 어떻게 구현이 되는지는 c++에서 어셈블리 까면서 설명함.  

1. 겉보기에는 같은 형.  
상속관계를 의미함.
부모형으로 자식 개체를 참조할 때 한정임!  
주류언어에서 상속은 다형성에 필요한 선수 조건.  

2. 개체들에 내리는 동일한 명령.  
부모 클래스에서 메서드의 시그내처를 정해줘야함.  
그렇지 않으면 부모 클래스형 변수에서 호출 불가  
자식 클래스에서 그 메서드의 구현을 덮어씀  
이를 overriding이라 함.  
* 오버라이딩은 선택사항이므로, 부모의 동작 중에 필요한 것만 고쳐사용할 수 있게 하자.  
즉, 자식에서 메서드 구현 안하면 부모꺼 씀. 당연하지?  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c0f28e17-f18c-40e2-abfb-0467bbee18e8)  
생성자는 super()가 맨 위에 있었어야 하는데, 메서드 오버라이딩에선 그럴필욘 없음.

## 다형성의 장점
개체 스스로를 책임진다는 개념에 가까운게 다형성임.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/2b306b8e-0275-48bb-87b9-29d6c61b3b24)  
1. 각 자료형의 코드가 클래스 안에 들어가니 캡슐화 증가.  
2. 유지보수성도 높아짐.  
3. 새로운 클래스를 추가할 때 클래스 코드만 추가하면 됨.  
다형성을 사용하면 새로운 클래스안에 메서드 추가하기만 하면 됨.  
근데 다형성 안쓰면, 코드 어딘가 찾아서 if문 추가해야 함.  
4. 클라이언트가 작성할 코드가 줄어듦.  

* late binding vs early binding  
실행될 메서드 정해지는건 언제 결정되는 걸까?
실제 실행중에 부모 메서드에 구현이 있는지, 자식에 같은 구현체가 없는지 확인이 들어감.
늦은 바인딩(late binding)  
실제로 호출되는 메서드 구현이 프로그램 실행중에 결정된다는 의미.  
dynamic binding이라고도 함.  

이른 바인딩(early binding)  
정적 바인딩(static binding)이라고도 함.  
C에서 배웠던 함수의 호출 방식.  
어떤 함수 구현을 호출해야 할 지가 빌드중에 결정남.  
어떤 함수를 호출할 지 jmp명령어로  
그 함수의 어셈블리어 코드가 시작되는 메모리 주소를 가리키게 함.  
C에서는 다형성을 지원 안하니까 가능한것임.  

C에서는 함수포인터가 late binding이었음.  
C에 없는 기능은 하드웨어에 없다.  
Java에만 있는 기능은 C의 기능들을 조합해서 만든 것.  
즉 컴파일러와 JVM이 함수 포인터 같은걸 대신 전달해주는 게 전부.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/841ba9a8-423e-4f5f-87d3-4bf4d60b48b2)  
c++에서 가상메서드라는 용어도 많이 쓴다네  

### 바인딩과 성능, 오버라이딩 막기
1. CPU최적화가 더 잘 되는것은 이른 바인딩.  
컴파일러가 실제로 어떤 함수를 호출해야 하는지 앎.  
따라서 컴파일 중에 충분한 시간을 들여 최적화를 할 수 있음.  
실행중에는 이렇게 충분한 시간을 사용할 수 없음.  

자바에서도 early binding 이 가능하다고 함.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/be33b6a8-69fa-44c6-b492-2b95787a6903)  
더이상 오버라이딩 안되게 막는 방법.  
메서드 앞에 final 키워드를 붙이면 자식에서 오버라이딩 불가  
C의 함수 호출되 동일하게 동작. 이른 바인딩 가능.  

final 키워드 사용처 3가지 정리  
아래 3가지를 어기는 코드는 컴파일 오류 냄.  
1. 변수앞에 붙는 final  
더 이상 변수 갑을 변경하지 못함.  

2. 메서드 앞에 붙는 final  
자식 클래스에서 더 이상 메서드 오버라이딩 못함  

3. class 앞에 붙는 final  
더 이상 상속하지 못함. 자식 클래스 존재 불가.  
따라서 오버라이딩도 못함.  

Best Practice : final은 기본적으로 붙인다 !!  
나중에 상속 및 변경해야하는 상황이 오면 그때 final 빼도 됨.  
예외1 : 상속 및 변경을 할 개연성이 높은 클래스 및 메서드  
예외2 : 소스코드 없이 외부에 제공하는 라이브러리  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/9150edf1-1633-4901-93ed-e56867d4bb8a)  

## 다형성 적용 예
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/4aadfedb-d4fd-4bd1-84e1-004c0ae2df97)  
이제 예외적인 개체에 대해 처리하기 쉬워짐!  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/5de85bc8-a148-4e7b-8c08-bd8dc1056523)  
오버라이딩은 클래스 다이어그램에서 확인 불가능함. 코드 직접 봐야함 ...  
근데 이 예시는 나중에 배울 인터페이스가 좀 더 좋은 해법이래  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/0ac7d937-6958-4d22-b5a2-078eea3624e4)  

*코드 샘플 : 마법사 구현  

## Object 클래스와 toString()
일반화의 끝판왕 Object에 있는 메서드.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/66d9b3ad-dcab-4b6a-b55d-946615e4e4b2)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/ffbb87e5-928c-4ad6-9a96-013ee80819ef)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/3a125a20-b6f0-4665-a00b-95a97bd7a6c1)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/a1e5d453-4f80-4b5d-a1bf-722fbacb9214)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/186d3d73-b1dc-498e-8f7c-e85163293a0b)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/a3217f0b-c612-4905-88cf-2336dabc79e6)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/5ac2b4db-fc30-4970-89a4-946dcf11ea78)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/9b6591c1-f8a5-401b-984b-02a542b270a0)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/cc926532-a327-4942-9847-743c523f3b7d)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/7f953a2c-7c97-4185-adff-1ea54284dc44)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c5e1f4ba-1433-43a1-9f2f-dba7c7fcb1f9)  
두개가 틀림을 바르게 볼 수 있지, 같아도 ... 우연히 해쉬맵이 같은 경우일 수 있음.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/95fbb7a9-6d21-4360-be5d-4079361cb0bd)  

코드보기 : 개체비교  
코드보기 : 해시값 계산  

# 추상메서드/클래스

## 다형성, 상속, 추상화의 관계
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/1a2b3c64-2639-4890-870f-dd202e6a91ae)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/84165472-4a7d-461d-a511-5507f3deab7a)  

뭔갈 잘 알려면 장점만이 아니라, 단점도 확실히 알고 설명할 줄 알아야 함.  
장점만 설명하는건 약팔이!  

## 추상 메서드 / 클래스 등장 배경
다형성으로 추상화를 수행하면서 새로운 문제가 발생함.  
어떤 문제인지 직접 모델링 해보면서 보자고 함. 

오늘 할 모델링 : 맨날 싸우는 몬스터  
* 몬스터를 만들어서 서로 공격하게 만들고 싶음.
* 몬스터 종류는 오우거, 유령, 트롤
* 공격하는 몬스터 종류에 따라 피해치 계산법이 다름.  
  본인과 상대방의 상태를 피해치 계산에 사용.  
  그 상태들을 합치는 방법이 몬스터에 따라 다름.  
* 나중에 몬스터 종류를 더 추가할 수도 있음.  

유일한 동작인 공격: 어떻게 구현할까?  
때리는 몬스터A, 맞는 몬스터 B가 있다.  
1. A에게 B를 공격하라 명령 : monsterA.attack(monsterB);
2. A는 B의 공격력(attack)과 방어력(defense)을 읽어옴
3. B로부터 읽어온 상태와 자신의 상태를 이용하여 피해량을 계산
4. B에 피해량을 적용: monsterB.inflictDamage(damage);  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/7c0004b9-bf47-49b6-88da-550735108bf9)  
일단 몬스터 마다 공격 방법이 달라서 메서드 비워둠.
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/60554743-49f8-4a9d-8c17-3f103dcfd53e)  
inflictDamage() 메서드는 protected여야지 아무나 접근해서 몬스터 체력 깎지 않도록 함.  
근데 ... !!! attack만 하고 inflictDamage() 호출을 안하는 문제가 생길 수 있음.
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/7e71b3a6-aff9-446d-8f76-cc94e65a4c96)  
-> 3번만 다형성으로 구현하는게 적절한 범위였음.
  ![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/6b31ee16-f112-475c-a213-8dcc66781838)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/fd792e44-24a2-453e-9f4b-1c8370f4a853)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/783b5f6b-bf99-49fb-8563-dfcae0e9eec2)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/b127e6bc-6cc1-4ee6-9471-7d8ddd0df93c)  

이렇게 설계 바꿔도, 메서드 구현을 안하면 말짱도루묵임.
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/89e0534f-7cfb-4575-8179-318bede821dd)  

현재 Monster클래스의 문제점  
1. calculateDamage() 메서드는 다형성을 위해서만 존재함.  
  자식이 구현을 안하면 원하는 기능이 안나옴.  
2. 구현이 없는 메서드란?  
시그내처는 있고, 함수 속 코드는 없는 메서드.  
동작이 일부라도 구현되지 않은 클래스는 실체가 완성되지 않은 클래스. abstact하다고 표현함.  

* 추상 메서드/클래스로 문제 고치기
두가지 실수  
1. 자식 클래스가 메서드 구현을 안하는것.
2. Monster라는 추상적인 실존하지 않는 인스턴스를 만들 수 있는 것.  
C에서는 함수 구현을 빼는 방법은 함수 시그니처 선언을 앞에 빼놓는 거였음.  

추상 메서드는 구현이 안된 시그니처만 있는 아이므로, 추상 클래스 개체를 만들 수 없게 해놔야함.  
class에도, method에도 abstract 키워드를 붙이면 됨.  
추상 클래스가 되면 그 클래스 개체를 생성할 수 없게됨.  
그리고 추상 클래스 내부 추상 메서드는 자식개체에서 반드시 구현이 되야 컴파일오류 안남.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/0cc4fa64-e4e6-4d8b-ad54-9978279e21c1)  
abstract 클래스면 클래스 박스 꼭대기에 ```<<abstract>>```로 쓰는 비표준 방법도 있다고 함.  

## 구체 클래스 vs 추상 클래스
* 추상 클래스여도 내부에 추상 메서드가 없을 순 있다.  
즉 모든 메서드가 구현이 없어야 추상클래스인건 아님!  
다만 추상 메서드가 있으면 그 클래스는 반드시 추상 클래스임.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/af9c04f0-c003-489c-986e-876b40cece1a)  
상속을 사용하지 않더라도 추상클래스를 만드는 의의가 있음.  
독자생존은 현 시스템에서 부적절하다고 판단되나, 나중에 재사용될 가능성 있다고 판단되어 만드는 경우.  

코드리뷰 : BaseEntity  

