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
보무 클래스에서 메서드의 시그내처를 정해줘야함.  
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
## 구체 클래스 vs 추상 클래스
