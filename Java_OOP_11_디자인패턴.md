# 디자인 패턴, 공부 시 주의할 점
싱글턴은 이미 봤음.  
디자인 패턴보다 하드웨어 도는법 알고, 내 코드가 정확이 어떻게 도는지 이해될 때까지 알 때 까지.  
카카오톡 설계 어떻게 하면 되는지 알 때까지, 패턴 보면 새롭지 않고 익숙할 때 까지.  
스스로 해답을 내보고 패턴을 보기.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/888ec0f9-a515-4dc3-bb5c-e30c6dce84e9)  


## 팩토리 메서드 패턴
무언가를 만든 공장.  
사용할 클래스를 정확히 몰라고 개체 생성을 가능하게 해주는 패턴.  
고객은 s, m, l를 선택할 뿐 실제 컵 용량을 모름.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/9d6415cc-3978-4df8-8096-94aeed25d6be)  

생성자 대신 정적 메서드를 사용하는 장점 :  
null 반환 가능.  
생성자는 생성이 불가능한 경우 반환형이 없으므로, null반환이 안됬음.  


### 다형적인 팩토리 메서트 패턴
위에 컵 사이즈 코드에서 계속됨.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/05b82d86-335f-4391-b985-2c6952f44b65)  
  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c159eb88-420c-4352-9680-d729ca7b1d22)  
createOrNull()을 다형적으로 만드는게 OO사고방식에 부합함.  
그러나 static method를 다형적으로 만들 수 없기에, 자식 클래스를 만듦.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/712591f0-d25c-4e5a-a878-a4e4a88b0547)  

여기서 한 단계 더 나아가면, 반환하는 Cup도 추상적으로 만들 수 있다.  
각 나라의 법규 따라 사용하는 컵 종류가 다름.  
어떤 나라는 1회용 종이컵, 어떤 나라는 반드시 유리컵.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/265b9c76-7bc7-4bb7-af12-12985ced0736)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/7957eb26-0f3f-4e20-8980-caca1a05393f)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/5e47d345-0d51-4959-98c8-67e4b7d660e0)  

팩토리 메서드 장점 !  
1. 클라이언트는 본인에게 익숙한 인자로 개체 생성 가능.
2. 생성자에서 오류 감지 시 null 반환 가능
3. 다형적으로 개체 생성 가능. (그래서 가상 생성자 패턴이라고도 함)

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/6ababdfd-a5b6-430d-b2b2-b3fa76acd685)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/67ac0471-dbcf-49a7-8d71-fa865a821377)  

## 빌더 패턴과 StringBuilder
개체의 생성과정을 그 개체의 클래스로부터 분리하는 방법.  
개체의 부분을 만들어 나가다가 어느정도 준비되면 그제서야 개체를 생성.  
다형성이 없는 빌더는 이미 StringBuilder에서 봄.  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/8ae0674e-ba77-4238-b758-dfe032e6ab42)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/3db9848c-8722-48c3-9bc5-8b028dae8690)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/ded2c1a1-9fe4-458d-b657-a8b3019003ab)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/6194ba80-56a1-4703-864d-789b5f8b68e2)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/36d80016-e72a-4c84-ab6e-359e64a069bb)  

## 빌더 패턴과 플루언트 인터페이스
살짝 삼천포 빠진 내용ㅎ  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/4729277e-47b8-43f8-8c04-28b474ab3a01)  

플루언트 인터페이스(fluent interface)  
요즘은 빌더 패턴 구현 시 종종 플루언트 인터페이스도 지원. 조금 더 모던화됨.    
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/9f506b56-1aff-4b5d-91e7-e313d4328856)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/899f5e6f-a822-45b2-b2c1-74358452bf24)  
자기 스스로를 반환하여 줄줄이 method 연쇄호출이 가능하도록 함.  

### 잘못 사용하는 빌더 패턴
String은 빌터 패턴의 괜찮은 예 이지만, String 붙이기를 대신 해주는게 전부.  
빌더 패턴을 제대로 이해하기에는 좀 모자름!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/ef9a216d-bc26-4fb8-a087-a467f4816e4f)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/6c34c11c-6a86-4187-b625-ac38719fb221)  
컴파일러가 잡아줄 수 있는 문제는 자료형이 안맞는 정도.  
형이 같은 매개변수 여럿 있으면 이런 문제가 생김!  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/aa9c9ee0-2a2d-44fc-9377-0bc90b712196)  
아까보다는 함수 명으로 잘못된 값을 전달할 확률이 적어지지만, 여전히 근본적인 해결은 아님.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/2ea0e4a6-5cc8-42ba-af19-1ef1b5d249d5)  

  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/37014641-5941-47f6-9053-beaeb2cd48ca)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/f87fccca-19c9-43dc-b4cc-e862cb2d0e97)  
멤버변수 추가를 클래스 내부에선 했는데, 호출할때 추가하는거 까먹는 경우 등 실수여지 남아있음.  
그러나, 앞에 빌더패턴보다는 천배 나은 방법이래.  

### 빌더 패턴 없는 올바른 문제 해결법
C#에서 완벽하게 처리하는 방법  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/01d261a1-f55b-490f-b563-584f36b8d9e6)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e5bcf668-135a-4842-aac3-6ec81ba775f2)  
언어에서 자체 지원 안해줘서 발생하는 문제인 것이다 ...  

### 다형적인 빌더 패턴
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/ffee8992-39f7-4327-b391-d53ab627456c)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/8b76d83f-95df-47ed-b3b5-c65094fa216c)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/eae31b18-adc0-43e5-b409-6bdf163e3b16)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/9f696e55-7491-4fc3-b85f-2eacbcc59279)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/9a315a48-1c6b-4376-b282-451f591ced97)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/1f3dd8df-c637-48cf-acff-81696c201dca)  

## 시퀀스 다이어그램
코드를 직접 보여주기 어려운 경우, 이에 잘 쓰이는 UML다이어그램이 시퀀스 다이어그램임.  
개체들이 서로 통신하는 모습을 보여주는 UML다이어그램.  
동작을 시간 흐름에 따라서 보여줌.  
전에 본 클래스 다이어그램은 구조를 보여주는 다이어그램이었음.  
맨 위에 박스들이 참여자임.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/fe3ad41e-e19f-4d75-a93d-2c5b0313797b)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c198d6df-57e2-4a7c-8ab8-601549d0f01e)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/1e46bba3-166b-4272-bee1-0ea6c5794360)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/776d28cc-0275-4fc5-9485-5f55b3420280)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/fdca6172-3b0e-4514-a2dc-56fc918e6d95)  

## 래퍼(wrapper) 패턴
주로 업계에서는 wrapper패턴이라 함, adapter패턴이란 이름을 사용함.  
어떤 클래스의 메서드 시그내처가 맘에 안 들 때 다른 걸로 바꾸는 방법.  
단 그 클래스 메서드 시그내처를 직접 변경하지 않음.  
소스코드가 없거나, 그 클래스에 의존하는 다른 코드가 있을 수 있으므로.  
대신, 새로운 클래스를 만들어 기존 클래스를 감쌈.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/896dc71c-b8b6-4b8b-b0d8-ada1670e9e9a)  

매서드 시그내처를 바꾸려는 이유는 다양함.  
1. 추후 외부 라이브러리를 바꿀 때 클라이언트 코드를 변경하지 않기 위해
2. 그냥 사용중인 메서드가 코딩 표준에 맞지 않아서
3. 기존 클래스에 없는 기능을 추가할려고
4. 확장된 용도: 내부 개체를 클라이언트에게 노출시키지 않기 위해
data transfer object(DTO)만들기  

### 래퍼 패턴과 그래픽 API
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/1fb549df-8605-478d-88f5-67a5c6001ba0)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/f41dda96-5141-4c01-84cf-62757066068f)  
하는 동작은 같아도 시그내처가 다르네 ?  
일일이 모든 코드 부분을 바꾸기 불가능할 수 있음.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/19c68dfc-26cb-4f21-8343-0369f5220ef9)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/66902a0c-3bce-4a1f-9083-7a76b18dde59)  

### 래퍼 패턴과 DTO(data transfer object)
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/0dbe8cec-385e-4ba5-ae97-b9d61d6f1b7c)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/f6d12094-4902-45a3-9bbe-f10ae978dfed)  
필요한 정보만 반환하고 싶음!!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/ce6b4db7-7766-49b9-87aa-9f3235eb2cfb)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/1021f375-1894-41b7-a9ce-c0cba52e8a37)  
새로운 obj만들어서 반환하기만 하면 됨.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/21e150d7-4d88-404a-bd99-0c77e936a081)  

## 프록시 패턴
proxy란?  
프록시 서버란 실제 웹사이트와 사용자 사이에 위치하는 중간 서버.  
인터넷 상의 캐시메모리 처럼 작동함.  
- 사용자는 프록시 서버를 통해 원하는 문서를 읽으려 함.
- 프록시 서버에 이미 그 문서가 저장되어 있다면 그걸 반환.
- 없다면 실제 웹 서버에서 문서를 읽어와 프록시 서버에 저장.

프록시 패턴이 이루려는 목적도 비슷.  
클래스 안에서 어떤 상태를 유지하는게 여의치 않은 경우가 있음.  
데이터가 너무 커서 메무리 부족하거나 시간이 꽤 걸리거나,  
개체는 만들어도 그 속의 데이터를 사용하지 않는 경우.  
(나중에 필요하면 부르도록 대기하기)  

-> 이럴 경우 개체 생성시에는 데이터 로딩에 필요한 정보만(파일 위치) 기억해 둠.  
클라이언트가 실제로 데이터를 요청할 때 메모리에 로딩함.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e3fa4239-b4dd-48db-a2ab-1ba7ad304c62)  

### 즉시로딩 vs 지연로딩
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e1050047-9941-4e59-9ba1-775d9bc6dbad)  
요즘 컴퓨터는 메모리 충분히 가지고 있으므로, 지연로딩 궂이 안해도 될 경우가 많음.  
클라이언트는 언제 뭐 때메 이 클래스가 느려지는지 알 수 없다.  
위에 표 3가지 방법 중 어떤걸로 구현되있는지 모르니까!  

이에 대한 여러가지 주장들 ...  
클라이언트가 그걸 알 필요가 없다. (극단적인 OO진영의 주장)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/6313e714-762b-429a-9456-a1d20dc46a8d)  
요즘은
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/330629e1-3b29-4cb3-ba13-eb3d766c1bb9)  
이런 방법을 더 씀. 즉 내부 구현 을 알긴 해야함.  
요즘 세상에는 클라이언트에게 조작 권한을 주는게 좋을 수 있음. 아래에 나옴!  

### 프록시 패턴의 현대화 예
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c9380794-9f3d-42d6-a5dd-3499e053416d)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/6a63a75f-e3f6-437a-a78e-5486e06e141e)  
상태 별로 업데이트 목록을 바꾸는걸 state machine이라 함.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/19323116-0d11-4efb-af6b-4f64714a396c)  

지연 로딩이 무조건 나쁘다는게 아님.  
필요한 곳에 잘 선택해 쓸것.  
사용자 경험(UX)도 고려해야 함.  
내부 동작이 명백하게 보이게(다만 캡슐화는 깨지게) 클래스를 작성하면 좋은 경우  
- 단순히 결과를 말하는 게 아님.
- 거기에 걸리는 시간 등의 부수적인 요소도 중요하다면 더더욱!

## 책임 연쇄 패턴과 로거
wiki에서 잘못 설명하고 있는 내용...  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c923c2f1-36dc-4e40-8c11-360a2cff990d)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/3d3a7d3f-9d37-4019-95fe-2bbb9328d998)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/91c51304-fda0-4bfa-aba9-2865e914ee41)  
enum안에서 values()라는 메서드를 호출하면 모든 enum내용들 반환함. (꿀팁)  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/b42457cf-f19d-4c27-b030-339e2ceb2904)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/7b29ca40-d8cb-4992-a6ac-6c6420882dae)  
근데 이 방법은 비효율적임 !!  

-- 더 나은 방법 --  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/49938636-a2e7-4019-8819-fe3c84066bcd)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/ada4a3cd-73b7-439d-bcb0-0709ab464c09)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/47c27f71-6f7f-4a9d-b0ee-1e868cce5de5)  
이 전보다 더 단순해짐 !!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/2d3e25b4-d098-4407-a30a-aacd016af43f)  

wiki 예시가 잘못됬던거임.  
책임, 연쇄에 대한 이해가 필요함.  

### 올바른 책임 연쇄 패턴 예
* 어떤 메시지를 처리할 수 있는 여러 개체가 있음.
* 이 개체들은 차례대로 메시지를 처리할 수 있는 기회를 받음
* 만약 그중 한 개체가 메시지를 처리하면 그거에 대한 책음을 짐
* 즉, 다음 개체는 메시지를 처리할 기회를 받지 못함
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/6e1a9574-1ed1-4607-93b7-d062db475936)  
내가 처리했으면 끝, 그게 아니면 다음 애가 처리해줘~ 하는게 책임연쇄의 구현임.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/9cf38e18-961a-4598-93d2-0c7854a67b9f)  

## 옵저버 패턴과 Pub-sub 패턴
observer.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d15f0782-a702-4262-b625-b747bcde2d03)  
A가 바뀌면 나도 바뀌고 싶다. 혹은 난 뭘 하겠다는 결정을 내림.  
근데 더 많이 쓰는 이름이 Publisher-Subscriber패턴이라고 많이 부르고 있음.  
옵저버와 비슷하지만 엄밀히 다른 패턴.  
그러나 이루려는 목적은 비슷하기에 흔히 같은 패턴이라 봄.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d2ed4c59-0048-45f6-a692-13d522a86346)  
여기서 LogManager를 빼면 그게 옵저버 패턴.  

### 옵저버 패턴 예
후원 받을 때마다 두 개체를 업데이트 하고 싶음.  
1. 장부 업데이트 (상태는 금액만 필요)
2. 모바일 폰에서 노티를 받음 (상태는 이름과 금액이 필요)
(cf: event-driven 아키텍처라고도 함)  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c56e0b01-d470-4c8e-a319-71c4a2032f33)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/87e5eac6-1ee9-4097-b0ef-6bf3d070b7e7)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/a7d6a0db-0077-431a-b134-2b81b0fbd590)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/b9e989c2-edcd-4aca-85b2-177e60c16392)  

* pub-sub 패턴과의 차이는 발행자가 하나!  
* pub-sub 패턴은 many-to-many니 그걸 조율해주는 중간 클래스가 있을 뿐.  
C언어 함수 포인터를 통한 콜백 함수와 동일함.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/397b4002-1985-49f3-b869-c07e57980bc1)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/0adaf2af-95f7-4c91-90cd-3762d203ce25)  

### 옵저버 패턴과 메모리 누수문제
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/50bd90ad-69b7-4a68-bb3d-a977e48e3cd6)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/8606cad9-f5d9-4f56-8bc9-ad5ba7efa796)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/0e738123-e8b3-480e-8d1a-6c77799e3ba0)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/f779fab5-c464-49f6-bfce-58d875739dc4)  
* unsubscribe() 호출하는거 안 까먹기 힘듬. 여러 메소드 unsubscribe() 일일이 해줘야하면 더더욱.
* 그래서 실제로 이런 메모리 누수 많이 생기고, 문제 찾기도 힘듬.
* Java에서는 book이 지워질 때 자동으로 unsubscribe() 호출하게 만들기도 좀 어려워짐.
* C++에서는 소멸자(destructor)를 통해 자동화 가능.
C++은 개체가 지워질 때 반드시 호출되는 함수가 있음. 개체를 스택에 만들수도 있어서 그 범위를 벗어나면
개체 지우도록 하는게 가능함. 그래서 Java, C#의 메모리 누수는 C++의 메모리 누수랑 약간 다름!
