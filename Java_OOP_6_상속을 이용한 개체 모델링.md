# 상속을 이해하는 방법

1. 일반화/특정화 관점  
종 분류 같은 tree 구조  

2. 기능의 관점  
공통 클래스를 만들고, 그로부터 상속받은 상태와 기능을 재활용  

두 방법 모두 일반화 능력이 필요함.  
일반화 능력이란 직간접적으로 경험한 다양한 개체들로부터 공통된 부분을 찾는 능력.  
공통 부분은 실존하지 않는 개념일 수도 있음.  
수학/물리학에서 허수 개념으로 양자역학이나 파동 모델링을 해결한 경우가 있음.  

... 많이 하면 늠! 익숙해지길 바래 ~~  


# 벽시계 모델링하기 : 아날로그 시계, 디지털 시계

## 아날로그 시계
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/aea3640b-68cc-4035-917f-4623899c438d)  

setter에 있는 문제 : 부적절한 범위의 값을 받을 때..  
1. IllegalArgumentException 에러 던지고 실행 중단?  
이건.. 누가 책임을 질지 모호해지므로 부적절함.  
예외처리는 나중에 더 배움.  
2. 예외 없이 시간 바꾸기  
* 최대/최솟값을 넘지 못하게 clamping하기  
* 최댓값을 넘으면 최솟값으로, 최솟값을 넘으면 최댓값으로 wrapping하기  

wrapping code  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/cbadd031-0a9f-469c-8f03-1daa91b2087a)  

60초는 1분 0초니까 .. 받아올림도 하는 시간으로 바꾸기  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/4ad6c749-7e53-459a-bb75-cad9190dc64d)  
setSeconds도 수정됨. setHours는 수정할 필요 없음. 더 올릴 시간이 업으므로.  

주의점!!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/4971c048-e689-4397-ad6e-c6cfa37f977a)  
메서드 호출 순서가 중요한데, 이를 시간적 결합(temporal coupling)이라 함.  
이는 한눈에 딱 안보여서 실수하기 쉬움. 해결 방법이 있을까 ?  

실제 시계와 좀 더 비슷하게 바꾸기.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/94598187-26e1-4f7d-a621-5587be76c772)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/a6d69b9a-d601-47e0-8db8-80907e67216f)  

-> 시, 분, 초를 각각 저장하지 않고, 초로만 저장하고 있다가, 실제 시간 반환 필요할때만 계산하기.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d79e2a20-e3c8-46d6-b1c5-721871aacec9)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/8993e6bb-f24b-4fb2-8857-dbf4c3a6915b)  
외부에서 음수 들어와도, 그거 다 확인하고 내부에는 양수값만 저장되도록 짠 것임.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/479ea80e-59af-4077-a395-45b7b71b8b87)  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/03656045-5ead-424c-8e0b-071abfb7420f)  

아날로그 시계 시침 분침 초침 각도 구현  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/a347b266-d84d-4e1f-9338-d5c1b8a13673)  


## 디지털 시계
아날로그 시계와의 공통점, 차이점을 찾아서 구현하면 됨.  
공통점 : 현재시간 기억, 벽에 검, 1초씩 셈.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/6d843b9b-8de2-452a-a31a-4d656c42245b)  

차이점: 오전/오후 구분 및 출력, 시간 맞추는 방식, 7세그먼트 디스플레이  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/a5bc3643-11c6-4a22-bf12-d5240cf266ee)  
부모 클래스 바꾸면서, 자식 클래스도 바꿈.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d69e7f7f-f976-4388-837d-76bf0d6f9c6e)  

Q: 디지털은 24시간 체계, 아날로그는 12시간 체계로 바꾸려면?  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/31febbc8-ae61-48b3-a75b-1d97037c785f)
자식마다 캐스팅 해주고 써야 함.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/a86321a3-d31f-48bf-95f2-5f531c438563)  

시, 분, 초 설정  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/0052cbab-a7bb-4d2c-b219-27c41d73cfea)  

7세그먼트 디스플레이  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/37a4c9ef-3edd-4e5a-be35-ec547cada0d9)  
1. 불리언 요소 7개 가진 배열  
2. 비트 플래그 : 자바의 enu,과 EnumSet이용
3. SevenSegmentDisplay 클래스 만들기  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/f050debf-7e65-4dca-8cfb-4fb419543ed7)  
* 이거 클래스 구현하는거 시험에 나올거 같은 느낌 ?  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/857e32ef-495a-4c89-ad81-ad2914470705)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/686fc936-6de2-454e-aa3d-a6f0ca15a69f)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/de6dbd35-32dd-4564-8d27-54f227159965)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/7fa158c2-0557-4c6c-8726-1b0edd6bdaf4)  


## 다중 상속
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/01443b47-34e7-48c8-8ce7-d595b85d32ee)  
자바에는 없는 다중 상속 개념.  
복잡해서 잘 안쓰는 개념임.  
가장 아랫줄 클래스들은 Clock클래스를 두번 상속받게 되잖아?  
C#도 지원 안함. C++만 한대.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d1b67e50-4383-41e7-81da-0ac8aa756d80)  

아무튼 자바에서는 다른 방법을 써야 함.  

## 다중 상속이 생기는 이유와 해결법
문제가 뭔데? 전혀 다른 양상의 특징을 상속받으려 함.  
유사한 특징이 추상화되면 편한데, 그러지 못하고 있음.  
여러가지 특징을 상속으로 처리하려 하면 부자연스러워짐.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/aa727532-dc84-49af-8dce-2a5f46a76dc2)  

1. wear()와 mount()를 추상화
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/4488768e-81bd-4b0c-b180-3159a4c5eac5)  


2. 인터페이스(interface)
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/6181799b-f813-418f-8e90-09c30a435d84)  
다중 상속이 아닌 점선의 뭔가가 있는데, 나중에 배운대.  


* 깊은 상속은 생각보다 어렵다!
보통 1에서 2단계만 상속함.  
당연히 단계가 늘어날 수록 추상화 능력이 더 필요함.  
근데 누가 미리 해놓은 생물 분류 같은거면 편하게 쓸 수 있음.  
지식 수준에 따라서 설계가 달라지기도 함.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/78a8a633-d0c5-4136-92e0-357173dab924)  
생각지도 못한 행동을 하는 개체가 있으면, 부자연스럽게 상속 받지 말고, 새로운 부모를 만들어 버리자 !!  

근데, 수백년간 연구한 상속 분류도 예외가 있는 정도니, ... 상속은 원래 몹시 어려운 개념인 것임 !!  
