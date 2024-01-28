# 암호화

평문(plaintext)를 암호문(ciphertext)로 변환하는 것  
평문: 누구나 읽으면 곧바로 이해할 수 있는 정보  
암호문: 누구나 읽을순 있지만, 이해할수는 없는 정보. 특별한 정보를 아는 사람만 이해할 수 있음  

복호화(decryption) : 암호문을 다시 평문으로 변환하는 것.  
암호화에 사용한 방법을 알아야 빨리 복호화 가능.  

해시 알고리듬과의 차이점  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/54aab03e-ba03-4355-846d-e8b1fc7cffd0)  

암호화의 역사  
디지털화된 정보가 온라인에 있는 건 당연한 시대 흐름.  
새로운 시대에 맞는 새로운 방법이 필요함.  
글자 교환 방식은 현재 무차별 대입 공격으로 매우 쉽게 깨지는 방법임.  
현재 컴퓨터 성능으로는 사실상 깰 수 없는 암호화 기법이 필요하지만, 이것도 언젠간 깨짐.  

## 정수론
정수의 성질에 대해 연구하는 학문.  
2진수로 표현된 데이터를 암호화하려다 보니 갑자기 주목 받음. 2진수도 정수니까!  
특히 소수와 관련된 정수론적 알고리듬이 많은 주목을 받음.  
- 암호문의 패턴을 들키지 않으려면 겹치지 않는 수가 필요
- 소수는 자연에서 가장 안 겹치는 수

암호학에서 사용하는 정수 : 매우 큰 정수  
흔히 사용하는 32비트 등의 정수가 아님.  
32비트 범위 안에 있는 소수는 2억여개 정도밖에 안되서, 빠른 시간에 뚫린다.  

입력크기 N  
보통 배열 속의 요소 수를 의미함.  
암호학에서 사용하는 정수에서는 비트 수를 의미함.  

곱셈, 나눗셈, 나머지 연산의 시간 복잡도: RAM에서 보통 정수는 O(1)  
암호학에서 사용하는 정수는 비트 수에 비례  

현대에 사용하는 암호화 알고리듬 두 종류  
1. 대칭 키 암호화 (Symmetric-key encryption)
: 암호화/복호화에 동일한 키를 사용  

2. 비 대칭 키 암호화 (asymmetric-key encryption)
: 공개 키 암호화 (public-key encryption)이라고도 함  
암호화, 복호화에 사용하는 키가 다름.  

## 대칭 키 암호화
암호화, 복호화에 동일한 키를 사용  
수신자가 그 키를 가지고 있어야 복호화 가능  
다른 사람들은 몰라야 비밀 유지가 됨(대칭 키 암호화의 가장 큰 단점)  

예를들어, xor연산 두 번 하면 원문 돌아오니깐 암호화 키 두 번 적용하면 됨.  

* 스트림 암호 vs 블록 암호
방금 예는 스트림 암호 (stream cipher)의 예  
한 번에 1바이트씩 받아 암호화 진행 (같은 글자에 같은 키 쓰면 패턴 보고 해독해버리니까)  
안전하려면 각 바이트에 적용하는 키가 달라야 함  
보통 시드 (seed) 값을 정하고 난수로 생성  
블록 암호보다 설정이 복잡하나 속도가 빠름  

블록 암호 (block cipher)  
정해진 블록 크기(64비트 이상) 만큼의 바이트를 한 번에 암호화  
각 블록에 사용하는 키가 동일함  
스트림 암호보다 설정이 간단하나 속도가 느림  

wi-fi 비밀번호도 일종의 대칭 키  
공유기에 설정하는 비번과 스마트폰에 입력하는 키가 같음.  
따라서 그 키를 아는 사람만 메시지를 해독할 수 있음.  

WPA2=Personal은 이런 식으로 작동  
폰이 처음 공유기에 접속 시 교환하는 어떤 값과 비번을 합쳐 키 생성.  
그 키로 메시지 암호화  
따라서 모든 접속자마다 다른 키 사용  
하지만 둘 사이의 모든 트래픽을 캡처한다면 읽기 가능.  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/b0d74fdd-81bb-4ad1-848b-50564cc5e35f)  

### AES (Advanced Encryption Standard) 알고리듬
NSA에서 일급비밀 용으로 승인한 유일한 공개 암호화 알고리듬  
블록 암호임.  
현재 가장 널리 사용되는 대팅 키 알고리듬.  
앞에 든 WPA2프로토콜 일부로 사용되기도 함.  
블록 크기: 128비트  
키 길이: 128, 192 또는 256 비트  
키 길이에 따라 평문을 암호문으로 변환하는 라운드 수가 다름. 라운드 마다 동일한 연산.  
128비트: 10라운드  
192비트: 12라운드  
256비트: 14라운드  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/f5c8b5b5-25f4-449c-8c01-9679cbb87fa7)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/38ebdfc9-8bf0-4106-a16a-4f0733d17131)  

AES 내부 연산  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/94961f8f-566e-44de-bf36-eba6720332a1)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/2d29ff67-367c-499d-b93e-815b08293cd6)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/74baa316-5f79-4339-8420-39c4111b6365)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/4fc39a53-279f-4e4f-8c75-2832b029771d)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/3e84c43e-ee1f-47be-9b8a-aa202b8fdd9e)  
선형적인 변환이 아니라서 단순 사칙 또는 비트 연산으로 찾을 수 없음!  
이를 혼돈(confusion) 효과를 성취한다고 함.  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/3542ca49-1e8d-4442-8fc5-73c924d9ebde)  
확안 (diffusion) 효과를 성취 한다고 함.  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c7e204b6-ac59-4423-823f-0792982ee521)  
곱셈도 그냥 곱이 아니라 특별한 곱셈 규칙을 따름.  
(이건 중요한 내용은 아님)  
1로 곱할 때 : 일반적인 곱셈과 동일. 원래 값 그대로 유지.  
2로 곱할 때 : 원래 값에 2를 곱함 (=왼쪽으로 1만큼 비트 시프트)  
원래 값 최고 비트가 1이면 0x1B로 xor  
3으로 곱할 때 : 2로 곱한 결과에 원래 값을 xor함  

-> 행 이동과 마찬가지로 확산(diffuse) 효과 성취  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/11e687f9-128d-4be5-a372-498d89351093)  

최종 라운드  
바이트 대체, 행 이동, 라운드 키 더하기(열 섞기만 안 함)  
그 결과가 최종 암호문!  

복호화는 지금껏 한 연산 반대로 하면 됨.  

코드보기: AES  

대칭 키 암호화 용도  
하드에 파일 암호화하여 저장  
DB에 고객 정보 저장  
사내 서버 간 통신 암호화  
동일한 키를 사용하므로, 메시지 교환용으로 사용할 때 안전하게 키를 배포하기 힘듦.  
wi-fi접속 사례 처럼.  
이 보안 문제 해결할 수 있는데 비대칭 키 암호화 방법임.  

## 비대칭 키 암호화
복호화에 사용할 키를 완전히 공개하지만, 수학적 방법으로 보안 유지함!  
암호화와 복호화에 사용하는 키가 다름.  
두 키 사이에는 특수한 수학적 관계가 있음.  
둘 중 한 키로 암호화한 메시지를 다른 키로 복호화할 수 있음.  
따라서 키 하나는 완전히 공개해도 상과없음. 이를 공개 키(public key)라 함.  
다른 키 하나는 한 개인이 비밀로 가지고 있음. 이를 비밀 키 또는 개인 키(private key)라 함.  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/1026db6f-2684-4bf9-85b3-5105fcb848be)  

비대칭 키 암호화의 두 가지 주요 용도  
1. 전송하는 메시지 암호화
다른 사람이 원문을 못 보게 숨김  
공개키로 암호화, 비밀키로 복호화.  
  
3. 전자서명(digital signature)
비밀키로 암호화, 공개키로 복호화.  
메시지는 누구든 볼 수 있음  
메시지 송신자가 올바름을 증명  
암호화폐에서 돈을 옮길 때도 이 방법을 사용 (로그인 시스템이 없으므로)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/966d7343-ceec-4e2d-9030-2ccf29883376)  


## RSA와 큰 소수
비대칭 키 암호화를 사용하는 곳
* HTTPS  
비대칭 키 암호화와 더물어 대칭 키 암호화도 사용  
* 메신저 앱의 비밀 채팅 모드  
서버도 내 비밀 키를 모르는 모드  
* 비트코인 등 암호화폐 프로토콜  
* Git 커밋의 전자서명  
Github에서 지원하는 GPG키  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/4898b32d-8b5a-4023-a146-abbb6278c264)  

* RSA  
현재 데이터 전송용으로 매우 널리 쓰이는 암호화 기법  
정수론에 기초해 놀라운 일들을 성취  

공개 키/비밀 키 쌍을 만드는 게 매우 쉬움 (매우 큰 두 소수를 이용)  

이 두 키는 특수한 수학적 관계를 가짐  
공개키를 알아도 그로부터 비밀 키를 찾기 매운 힘듬  
거듭제곱과 나머지 연산만으로 암호화 가능  
암호문을 다시 거듭제곱한 뒤, 나머지 연산을 하면 원문이 돌아옴  

* 소수의 특징
소수는 더 이상 인수분해가 안 되는 숫자  
서로 다른 두 소수 p, q를 곱하면 합성수 n이 나옴  
n의 인구는 p와 q뿐  

RSA가 이용하는 소수의 성질  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/6208c280-bcf3-4bc7-9ea0-ef5e19ff54ae)  
200자리 숫자에서 두 소수 찾으려면, 10^98초가 소요됨 ㄷㄷ  

공개 키/ 비밀 키의 특수한 관계  
RSA키 길이와 연산 속도  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/017c2556-bd6c-421a-9c11-701328cc6ef3)  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/4efcc4f2-af7b-420e-a93d-8b3449164638)

두 번째 특수한 관계 덕에 암호화 복호화가 간단하게 됨.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/5b7086e9-d0f4-4916-8405-09ede6e097dc)  

증명 설명은 메모 안할거임 > <  

RSA 키 생성  
1. 매우 큰 두 소수 p와 q를 찾는다.
2. p와 q를 곱해 n을 만든다.
3. p, q와 특수한 수학적 관계인 e를 찾는다.
4. e와 특수한 수학적 관계인 d를 찾는다.

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/96c5eac3-aff3-4e8f-a1c4-d0f2c28dfc8a)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/1c388829-d20c-4668-853b-1bfe6b20d0b0)  

대칭 키 vs 비대칭 키 암호화 속도 비교  
비대칭 키 암호화가 보통 더 느림  
키 길이가 훨씬 길고, 알고리듬 자체가 더 복잡함.  
그래서 비대칭/ 대칭 키 암호화를 같이 사용하기도 함.  
예: 세션 동안 사용할 대칭 키를 비대칭 키 암호화를 이용해서 전송  

코드보기 : RSA  
