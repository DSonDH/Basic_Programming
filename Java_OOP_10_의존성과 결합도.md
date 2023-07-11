# 의존성과 결합도
의존성(dependency)  
소프트웨어 모듈 A가 제대로 작동하려면 다른 모듈 B가 필요한 경우.  
B가 없으면 A는 작동하지 못함.  
A가 없어도 B는 작동 가능.  

*의존성이 있어야 좋은 설계임.
각 클래스의 목적이 뚜렷하다는 의미.  
캡슐화가 잘 되어있다는 의미.  
클래스를 재사용할 수 있다는 의미.  

결합도랑 헷갈리면 안됨 !!  
결합도는 나쁜거, 의존성은 좋은거.  

* 결합도 (coupling)  
두 소프트웨어 모듈 간에 상호 의존성 정도를 말함.  
클래스 A가 클래스 B에 의존, 클래스 B도 클래스A에 의존  
A와 B중 하나도 독자 생존이 불가능.  
여러가지 종류의 결합도가 존재하는데, 앞에서 본 시간적 결합도 그 중 하나.  

## OOP에서 논하는 결합도
: A가 B에 의존하는 상황에서 B를 변경할 때 프로그램이 잘 작동하는가?  
A의 내부를 변경 안해도 제대로 동작하면  
A가 B에 의존하나 그 정도가 높지 않아 결합도가 낮음.  
(loose coupling)  

A의 내부를 변경해야만 제대로 동작하면  
A가 B에 의존하는 정도가 높음. 즉 결합도가 높음  
(tight coupling)  

* 높은 결합도는 나쁘다? 동의 가능함.
* 의존성이 있어서 나쁘다? NO!!!
보통 결합도 있다고 뭐라 하면 의존성이 높아서 뭐라하는 거니까 알아서 알아먹으렴.
Decouple A and B : 사실은 결합도를 줄인다는 말이지, 아예 제거하는게 아님. 알아서 알아먹으렴.

## 결합도 판정
==> A를 바꿨는데 B도 바껴야하면 B가 A에 심하게 의존하는 것.  
A에서 생성자 argument를 추가하면 B에도 추가해야한다. 즉 의존성이 심한 것.  

결합도 줄이는 방법 ?  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d018a6f1-b931-46bb-9b57-8f267b19a332)  
Robot은 Head속이 어떻게 구현되어있는지 몰라도 되니까 느슨한 커플링이 된것!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/ba5c38ac-4114-4d69-bc85-fdc657065870)  


## 의존성 주입(DI)
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/679a3aa9-98ca-4d56-8d85-3d32633ca905)  
DI가 의존성 주입 컨테이너(DI container), 의존성 역전(dependency inversion)도 있으니 헷갈리지 말것!  

setter 주입  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/f782d511-ea69-449e-b195-6982f0641875)  
setter주입을 사용하면 생성자 주입을 생략할 수도 있음.  
하지만 개체는 생성 시부터 유효한 상태를 가져야 한다는 우리 원칙에 위배됨.  

DI를 통해 얻은 것 :  
1. 결합도를 낮춤.
2. 나중에 Head의 생성자가 바껴도 Robot을 바꿀 필요가 없음.
3. Head가 바뀌면 이 클래스만 따로 컴파일 해서 배포 가능(옛날 방식)

DI를 통해 잃은 것 :  
1. 편의성 : 로봇만 생성하면머리도 딸려옴.
2. 프로그래머의 원래 의도를 잘 보여주는 클래스.
분리/합체 로봇이 아닌 하나의 개체로만 바라봐야함.

둘둥 한 방식이 옳다고 할 수 없음 !  

## 상속 관계에서의 결합도
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/fd033686-e1c3-4655-8fc7-0f628ee5ccf2)  
샾은 추상 메서드임.  
다형성을 사용해서, 두 자식 클래스의 부모타입으로 호출하면, 자식 클래스에 대한 의존성은 없앰.  
의존성이 자식에서 부모로 간거지, 없어진게 아님.  

참고 : 인터페이스도 마찬가지.  
자식 클래스를 고체해도, 그 개체를 사용하는 코드를 바꿀 일이 적음.  

## 디커플링이 적합한 곳들
단순한 구조에서는 실익이 크지 않음.  
한두 군데 고치면 끝이고, 컴파일러가 문제를 일찍 잡아주니까.  
코드 변경이 불가능한 상황이 아니라면 굳이 커플링을 줄일 실익이 미미함.  
복잡한 시스템에서 한 클래스를 5000개가 사용하면 .. 5000개 나중에 일일이 고쳐야 할 때가 문제임.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/a6a09656-db4c-460e-8226-962c0cd83384)  
함수 시그니처만 같은 모든 자식 클래스도 허용되니깐.  


## 디커플링의 단점들
단점 1. 직관적이지 못하다  
디커플링 줄이려고 Head로 들어온 head개체가 어떤 속성의 head인지 모르겠당.  

실행파일 하나에 실제 사용하는 구현체가 하나라면 다형성으로 구현하는 아이가 아님.  
다형성으로 구현해야 하는 것들은, 실행파일 하나에 여러 개체들이 생성될 때 임.  
실행파일 하나를 여러 라이브러리에서 공유할려고 하는 경우는,  
컴파일 스위치를 바꿔서 실행 흐름을 제어하는게 올바른 방식임.  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d40e7cb6-c124-4d6f-a1d1-0e4ef3eddfc4)  
그렇다고 직접 실행해서 확인해보기엔, 매우오랜 시간 뒤나  
만나기 어려운 조건에서의 상황이라 디버깅하기 어려운 경우도 있음.  

단점 2. 내부를 알아야 좋은 경우도 있다.  
일반화/추상화 한다고 비효율적인 클래스를 구현해서 서버 1대로 돌릴거 서버 2~3대 쓰게 될 수도 있음.  
무늬만 바꾸는게 중요한게 아니라, 실제 어떻게 돌고, 어떤게 최적인지, 문제가 안생기는지 알 수 있어야 함.  


## 인터페이스의 잘못된 이해

인터페이스의 올바른 정의  
1. 주류 언어의 문법을 따름.  
2. 상태도, 메서드 구현도없는 순수 추상 클래스.  
pulic 메서드 시그내처만 모아 놓은 것. (C언어의 헤더 파일과 같은 존재)

OO에서 인터페이스 : 주 용도에 따른 이해  
1. 함수 포인터처럼 사용할 수 있는 것
2. 다중 상속을 흉내 낼 수 있는 방법
3. 변화에 대비해 결합도를 낮추는 것  
즉, 다형성 없는 인터페이스는 없다는 주장이 OO에서 일반적임.

* 프로그래밍 엉어마다 인터페이스라는 용어 및 키워드를 다르게 사용.
개체가 이해하는 명령(메시지)를 나열한 것이라는 개념적 정의도 있음.  
(다형성 있거나 없거나 모두 ... )  

다형성 없는데도 모든걸 Interface로 구현하는 극단적 진영이 있음.  

*인터페이스에 대해 프로그래밍 하라는 의미  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/4444492c-693e-4d90-8f53-7212cc1d2b93)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/7df1f5fd-8b58-4d37-8178-c4aff2a43375)  

*협업 시 가장 중요한 목표는 실수 예방!!
소프트웨어 개발은 협업 환경  
모두가 직관적으로 이해할 수 있는 방법은 실수를 줄임.  
- 주관성이 그나마 적음 (객관성 높이기)
- 많은 사람들이 직관적으로 이해할 수 있는 것이 OO의 캡슐화
- 추상화는 덜 하는게 실수가 적음!
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/26ca3622-41c7-4c14-9b33-b625319ad58f)  


## 이클립스(Eclipse) API와 인터페이스
디커플링 잘한 경우! 모범사례임.  
이클립스는 실무 Java에서 널리사용하는 Java IDE.  
이를 활용한 수많은 도구들이 존재함.  
API버전이 바뀔 때마다 메서드 시그내처가 바뀌면 곤란함.  
그래서 ...  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c0f87844-ef5e-479c-9f33-a2413631bfdf)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/9f50d51a-d1e1-4561-a1b0-aa970f475e66)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d58373d5-7829-4480-a7ef-eb3310c8c113)  

But 단점이 있음 !  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/fb2572bd-f121-4bfb-9930-c8cba1949a25)  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/524585c1-71dd-46aa-abe0-697b5174baa0)  

inferface와 class를 확실히 구분하는 프로젝트는 많지 않고, 시간/돈 문제도 시급해서 못하는 경우도 많음.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/beda42b3-43d9-4506-b99f-4e0b83b293b2)  


## 중요한건 클라이언트와의 약속
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/28983a33-2d15-4aa8-a7a3-6be601d4fb99)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/bb6f2c8d-a6ba-476d-92a7-7bdd70f66215)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/f88c54bb-dd4f-41e5-b998-1a5867c9689a)  
인터페이스는 바뀌는 경우가 적으니까 다른 코드 안바꿔도 될 확률이 많음.  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/92293335-45a6-40cf-8a9b-01f78a901184)  
* 요즘 사람들은 breaking 업데이트에 익숙함 !!  
즉, 버전업 속도가 빨라지고, 보안 패치 자주 받음 !!  
오작동 하는 건 클라이언트나 최종 사용자가 고침.  
요즘은 일반적으로 여러 버전을 지원함.  
*새로운 기능이나 breaking 변화는 새 버전에만 추가.

*버전 별로 지원 기간을 명시  
지원기간 동안 중요한 업데이트를 모든 버전에 적용  
지원기간이 지나면 다음 버전으로 옮겨야 함.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/a3c9785d-96bf-4cd8-b1cf-e6b3ffcdb54d)  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/59f74a47-d332-42f6-8e55-196ad28bd663)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/8891e293-be4a-454c-ba1c-735a6654917f)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d13bea15-f1ba-4522-84f9-a94e228bd39d)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/5e59cf92-b647-447b-8fcb-8334c3342914)  

