# Exception
C++도 예외를 지원하지만 중요성은 떨어짐.  
남용을 방지하기 위해, 올바른 사용법 위주로 보자.  

if문으로 수많은 예외 발생상황을 처리할 수 있음.  
exception은 예외 처리 미루는, 남한테 떠넘기는거임.  
애초에 exception-safe코드를 작성하기 어려움.  
사람의 사고방식은 선형적인데 예외는 비선형적.  

C++의 예외는 다수가 언어 자체 보다는 다른 프로그래머가 만든것.  
Java, C#에 있는 예외가 C++에는 없다.  

예외처리는, 예상하지 못한 것 처리하기위한 작업임.  
이런 예측가능한 이상한 값은 예외처리 대상이 아님.  

## 범위 이탈, 0으로 나누기, NULL개체
범위 이탈  
<img width="836" height="373" alt="image" src="https://github.com/user-attachments/assets/88829b4f-8b20-4259-ab84-8101252206bd" />  
try/catch없는 경우  
<img width="771" height="371" alt="image" src="https://github.com/user-attachments/assets/19b6b7a7-2e91-415e-9c26-683e77f1e238" />  
visual studio에서 기본옵션이 핸들링 안된 예외에 중단점 걸어줌.  
궂이 try catch해야할까?  
<img width="401" height="213" alt="image" src="https://github.com/user-attachments/assets/76d9b243-e726-40f8-824c-c637e7e06af2" />  

0으로 나누기  
<img width="526" height="305" alt="image" src="https://github.com/user-attachments/assets/be7a0bc9-ccaf-4265-bd1a-e301cad122d1" />  
<img width="623" height="286" alt="image" src="https://github.com/user-attachments/assets/ef76d0ce-52d9-4412-b30c-5342e0f921ae" />  
이건 C++예외가 아니고, 운영체제에서 제공하는 예외임.  
궂이 이렇게 예외처리 하는게 아니라,  
<img width="432" height="252" alt="image" src="https://github.com/user-attachments/assets/77931608-60c0-4360-9329-90b9384ade01" />  
이게 훨씬 깔끔함.  

NULL개체 들어오는 경우  
<img width="536" height="296" alt="image" src="https://github.com/user-attachments/assets/b5444342-16a5-4364-a80f-40ec48decd2a" />  
<img width="679" height="332" alt="image" src="https://github.com/user-attachments/assets/cde359a0-226f-429b-9b78-72ca83c4cc8f" />  
이것도...  
<img width="776" height="343" alt="image" src="https://github.com/user-attachments/assets/85860e7f-fd85-4ee2-8ec5-3f0d289e924d" />  

## 생성자에서 사용하는 예외
os예외 vs c++예외  
<img width="724" height="215" alt="image" src="https://github.com/user-attachments/assets/c5513912-12a3-4cce-9f3a-bf395bf04b01" />  

아까 봤듯이, 대부분의 예외는 불필요한데, 생성자에서 발생하는 예외는 필요하더라...  
<img width="478" height="234" alt="image" src="https://github.com/user-attachments/assets/375ec09f-c7af-455b-92b9-317a3357dc78" />  

생성자는 반환값이 없으므로...  
C++ 방식 예외 만드는 법!  
<img width="737" height="263" alt="image" src="https://github.com/user-attachments/assets/897198a3-085c-4bb7-91e6-b507fe6c8bb3" />  
함수 what()을 만듦. what을 호출하면 "Slot is NULL"반환하겠다는거임.  
<img width="473" height="426" alt="image" src="https://github.com/user-attachments/assets/c8a5e8f7-2e62-40f2-84f3-88e13598e341" />  
올바른 예외처리는 아님. 못쓰게 해야할거 아님!  
생성자에서 쓰는 예외는 괜찮음.  
<img width="754" height="322" alt="image" src="https://github.com/user-attachments/assets/0108ff40-f259-455d-9843-f83b6223e6e2" />  

## C++예외와 다른 언어들 예외 비교  
<img width="715" height="221" alt="image" src="https://github.com/user-attachments/assets/f0ac42f3-8ff6-4ee6-b48e-47f0e5394268" />  

C와 에러코드  
<img width="812" height="364" alt="image" src="https://github.com/user-attachments/assets/29b1d3b5-22d4-494d-81c1-4da12c5ab9ba" />  
<img width="661" height="229" alt="image" src="https://github.com/user-attachments/assets/f0c605b8-e273-4ebe-a096-679c8ceb0c54" />  

Java와 에러코드  
어느 약팔이가 그러길 ... 1  
<img width="860" height="371" alt="image" src="https://github.com/user-attachments/assets/fc1cbbd3-677a-4b99-82b4-e08b310d6553" />  
그러나 이건 코딩스타일로 깔끔해질 수 있는 부분이지, 에러코드 vs 예외 비교가 아니었음.  

어느 약팔이가 그러길 ... 2  
예외를 쓰면 소프트웨어가 더 탄탄해지나? 근거가 없음.  
20년 넘게 시간이 지나서 보니, 대부분 예외를 제대로 처리 안했음.  
예외안정성: 예외가 나면 예외가 나기 전의 상태로 돌아가는 것. (이런 상태를 일일히 제어해야함)  
이런거 제대로 처리 안하고, 그냥 돌기만 하는 프로그램을 좀비라 함.  
<img width="632" height="300" alt="image" src="https://github.com/user-attachments/assets/e7b1c199-04ba-4729-a167-ebae6ddcda3e" />  
<img width="641" height="303" alt="image" src="https://github.com/user-attachments/assets/764a0b27-c50e-425b-8e16-fe57a23cfaab" />  
100% 예외 안정성을 가지게 프로그램 짜는게 쉽지 않음.  
사람 머리로는 못따라감.  

수많은 언어에서 어떤 함수가 무슨 예외를 던지는지 알기 힘듦.  
예외로, Java는 무슨 오류 던지는지 표기하는 언어임.  
C++는 함수 헤더에 어떤 오류 던지는지 표기 안해서 보기 힘듦.  
<img width="830" height="371" alt="image" src="https://github.com/user-attachments/assets/6c843a08-b518-4b29-baad-3085576f1ef8" />  

웹 에러코드  
웹 요청은 상태코드(status code)와 바디(body, 데이터)를 반환.  
상태코드 20x: 바디가 있음(정상), 4xx(내 문제)나 5xx(서버문제)는 바디가 비어있을 수 있음  

웹 애플리케이션에서의 에러처리: Struct, Class로 c++에도 적용 가능  
예: 웹 요청 방식  
<img width="863" height="365" alt="image" src="https://github.com/user-attachments/assets/3cd71469-f54c-4297-82af-ea0e62d4ca51" />  

## 적절한 예외 처리  
적절한 예외 처리 전략  
1. 유효성 검사,예외는 오직 경계에서만  
밖에서 오는 데이터를 제어할 수 없으므로.  
예: 외부에서 들어오는 웹 요청, 파일 읽기/쓰기, 외부 라이브러리  

2. 일단 시스템에 들어온 데이터는 다 올바르다 간주하기  
assert를 사용해서 개발 중 문제를 잡아내고 고칠 것  

3. 예외 상황이 발생할 때는 NULL을 능동적으로 사용  
하지만 기본적으로 함수가 NULL을 반환하거나 받는 일은 없어야 함  
코딩표준: 만양 NULL반환하거나 받으면 함수 이름을 잘 지어야함(OrNull)  
  
<img width="396" height="351" alt="image" src="https://github.com/user-attachments/assets/b2949874-1b58-405b-8180-d926046b006b" />  

파일 읽으려는 순간 누가 지우는 경우.  

예외는 만병통지약이 아니다.  
<img width="721" height="175" alt="image" src="https://github.com/user-attachments/assets/17aefa44-da9c-4363-b651-41f2fdbdf764" />  
내가 아닌 다른 테스트 전문가가 필요함.  

개발 중 버그 잡기  
<img width="629" height="299" alt="image" src="https://github.com/user-attachments/assets/555642f4-6b41-4710-a1d0-86e0284d310b" />  
<img width="868" height="272" alt="image" src="https://github.com/user-attachments/assets/ba813de4-55d7-405f-85c2-95328e1b47c0" />  
