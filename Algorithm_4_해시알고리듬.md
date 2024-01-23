# 해시 알고리듬

## 해시 함수의 정의와 속성
해시 (hash)는 컴퓨터 공학에서 매우 근본이 되는 알고리듬 중 하나.  

* 정의: 임의의 크기를 가진 값을 고정 크기의 값에 대응시키는 함수.  

[필수요건]  
입력 -> 해시 함수 -> 출력 / 해시값 / 해시코드 / digest 라고 부르기도 함.  
수학에서의 함수의 정의도 만족해야 함 : 한 입력 값이 여러 출력을 낼 수 없다.  

용도: 해시 테이블에서 저장할 데이터를 저장할 위치를 찾기 위해.  
길이가 긴 데이터 둘을 빨리 비교하기 위해. (단, 다른 경우만 빨리 비교 가능)  
누출되면 곤란한 데이터 원본을 저장하지 않기 위해.  
용도에 따라 알고리듬 요구사항이 조금씩 달라질 수 있음.  

# 해시 알고리듬 분류와 속성
1. (비암호학적) 해시 함수.
2. 암호학적 해시 함수

해시함수 개념을 다른데 응용하는 방법이 두 개가 있음  
체크섬 (검사합, checksum), 순환 중복 검사 (cyclic reducdancy check, CRC)  

해시 알고리듬 별로 아래 속성들은 조금씩 달라짐.  
1. 효율성 (Efficiency)
2. 균일성 (Uniformity)
3. 등등

### 균일성
해시 함수의 출력값이 고르게 분포될수록 균일성이 높음.  
좋은 해시 함수는 균일성이 높아야 한다고 함.  
즉, 출력 범위 안의 모든 값들이 동일한 확률로 나와야 함 (균등 분포)  
이러면 해시 충돌이 적어 O(1) 해시 테이블을 기대할 수 있음.  

Q: 소수를 사용하는게 왜 해시값이 덜 중복되는 효과를 가지는지?  
A: 매우 큰 최소공배수가 나오기 때문입니다.  
'소수와 매미'란 검색어로 구글 검색 해보시면 재밌는 기사들을 볼 수 있을 것입니다.  

완벽한 해시 함수 : 해시 충돌이 전혀 없는 함수.  
입력값이 매우 제한적일 경우에만 가능함.  
이유 : Birthday problem에서 설명함 !  

균일성 측정법  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d056f7c1-6d3e-4fe8-9113-e665dd616068)  

균일성 높이는 방법:  
1. 해시값이 덜 중복되게 버킷 수를 정할 것 (소수를 사용)  
2. 완벽한 '눈사태'가 나도록 해시 함수를 설계할 것  

눈사태 효과(avalanche effect)  
입력값이 약간만 바뀌어도 출력값이 많이 바뀌는 것.  
보통 암호학적 알고리듬이 매우 선호하는 효과.  
알고리듬의 규칙을 쉽게 유추할 수 없기 때문!  
엄격한 눈사태 기준 (Strict Avalanche Criterion, SAC):  
입력값에서 1비트 뒤집으면 출력값의 각 비트가 뒤집힐 확률이 50%  
이 기준을 충족하는 해시 함수는 분포가 균일할 가능성이 매우 높음.  

균일성은 늘 언제나 높은게 좋을까?  
No! 비슷한 내용을 가진 데이터끼리 충돌하는게 좋을 때가 있음.  
* 지역 민감 해시 (locality-sensitive hashing)  
해시 충돌의 최소화 대신 최대화를 목표로 하는 알고리듬
엄청나게 많은 데이터에서 비슷한 것들을 찾는 용도.
스팸메일 찾기, 웹 검색 엔진에서 비슷한 문서 추천하기, 음원/사진 등 저작권 침해 검사 등등..

### 효율성
보통 빠른 해시 함수를 선호함.  
공간을 더 낭비해도 빠른 접근 속도를 선호 : 저장된 데이터를 빨리 찾는 용도  
충돌이 좀 나도 더 빠른 함수 선호  
어차피 해시 충돌은 드문 일, 몇 개 난다고 O(1)에서 크게 느려지지 않음.  
하지만 하드웨어 가속이 어려운 해시를 선호하는 경우도 있음: 암호학적 이유가 있음.  

* 암호학적 해시 알고리듬의 추가 속성
1. 역상 저항성 (Pre-image resistance)  
2. 제 2 역상 저항성 (second pre-image resistance)  
3. 충돌 저항성 (collision resistance)  


## 비암호학적 해시 함수
암호학적으로 사용하기에 안전하지 않은 해시 함수들  
보안적으로 문제없는 용도에 주로 사용.  
 - 데이터 저장 및 찾기 (해시 테이블)
 - 저장/전송 중에 생긴 데이터 오류 탐지
 - 고유한 ID생성 등등

!!! 모든 데이터에 대해 최고의 결과를 보장하는 해시 함수는 없다.  
입력값에 따라 다른 해시 함수를 사용하는 확률적 알고리듬은 존재 (Universal hashing)  
따라서 용도에 맞는 해시 함수를 사용하는 게 중요.  
심지어 bit-packing도 해시 함수로 사용 가능 (단, 균일성이 높지 않을 수 있음)  

비트 패킹  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/f63aa968-d7c1-4e5d-8968-4557230b89ce)  
age 부분은 7비트 정도 사용(최상위 비트는 사용 안함)  
order는 아래 한 4비트 정도 사용 (각 나이별로 최대 16명 뽑을 때 기준)  

올바른 해시 함수를 고르는 법  
제한된 데이터를 사용하는 경우 정도반 해시 함수를 직접 발명함.  
그 외에는 이미 존재하는 해시 알고리듬 사용함.  
1. 실제 가지고 있는 데이터로 테스트 하면서 측정한다.  
(속도, 해시 충돌 수, 메모리(보통 크게 중요하지 않음), 균일성(실무에서는 잘 안함))    
2. 구글링 한다 (내 데이터 들이 일반적인 테이터인 경우)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/cbc6897e-bd0b-430a-bad8-8041b0334096)  

### Lose Lose 해시
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/f0fd926e-2e28-4f61-8fb9-c28e233a13cd)  

### Murmur, FNV-1해시 
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/7cbd01f6-e5b5-415e-86ee-016412e3afcd)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/ab7eb327-8865-42c0-8916-c3b65867acf8)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/6e114a5b-4ba9-473b-8830-1c6436c39a7a)  
cpu에서 xor는 매우매우매우 빠른 연산 중 하나.  

### 체크섬과 CRC
여러 데이터로 도출한 작은 크기의 데이터 하나.  
보통 데이터에 있는 모든 바이트를 어떤 방식으로든 합함.  
해시 함수랑 매우 비슷한 개념! 출력값의 크기가 고정되어 있으면 해시 함수.  
용도: 저장 혹은 전송 중 발생한 오류 찾아냄.  
 - 처음 데이터를 저장할 때 체크섬을 계산해 저장
 - 나중에 데이터를 읽을 때 다시 체크섬 계산
 - 처음 저장한 체크섬과 다르면 오류가 난 것!

ex: ISBN 유효성 검사 (책에 있는 그 코드), 신용카드 마지막 숫자  

체크섬 알고리듬은 매우 간단!  
보통 간단한 산술 연산으로 계산이 빠르고 추가 메모리가 거의 불필요.  
-> 네트워크 프로토콜에서 사용, 하드웨어로도 구현하기 쉬움.  
단, 모든 오류를 찾지는 못함.  
문자열 순서가 뒤바껴도 같다고 처리해주는 알고리즘도 있음  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/18c0f485-4549-4cb8-9159-34343d45c644)  

* 체크섬과 미러 사이트
웹사이트에서 유용한 프로그램을 배포할 경우 미러를 사용하기도 함.  
요용한 프로그램이라 매우 많은 사람들이 다운도르 한다고 하자.  
한 웹사이트에서 트래픽 감당이 안되서 다른 웹사이트에서 대신 파일을 호스팅.  
근데, 미러 사이트에서 내 프로그램에 스파이웨어를 넣으면?  
그걸 알아낼 수 있도록 내 웹사이트에 체크섬 알고리듬을 돌림  
그 둘이 일치하지 않으면 누군가 변조한 프로그램!  
주의: 미러 사이트에 공개해 놓은 체크섬 값과 비교하는 건 도움 안 됨!  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/dcf5bdec-f630-47db-9ef3-89ccbf5ba2a8)  

* 순환 중복 검사 (Cyclic Redundancy Check)
체크섬 알고리듬 중 하나.  
다항식의 나머지 연산을 이용하여 검사값을 만듦.  
검사값은 보통 고정된 길이, 따라서 CRC함수를 해시 함수로 사용하기도 함.  
이진수 하드웨어에서 구현하기 쉽고, 최신 CPU는 CRC-32C 명령어를 탑재함!  

다항식의 최고차항에 따라 CRC에 사용하는 비트 수가 달라짐.  
각 차항의 계수는 1 아님 0.  
최고차항의 계수는 언제나 1.  
x^3 + x + 1은 1011이 됨.  
하지만 최고차항의 계수는 언제나 1이니깐 무시하고 011 3개 비트만 있음 됨.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/b434bb7b-c388-4441-bcac-12d1b511837c)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/54b649d4-5c5c-4a32-bf5e-bf4444492306)  
1비트 쉬프트 해서 계산하는데, 위 숫자가 0이면 스킵함. 즉 1일때만 계산 함.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/2de3901e-787a-4c8d-a926-248836dcc3e0)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/03c1f893-66c2-4c7d-8247-3690ffbd146a)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/4d53b5b0-e185-4fce-9d70-65e1cea1e9a9)  

매애애애우 긴 문서를 String.equals()하기에는 무리가 있음.  
이 때 두 스트림을 직접비교하지 않고, 체크섬을 비교하는게 좋음.  
몇 바이트 씩 끊어와서 비교하는 방식임.  
부분적으로 String 비교하는거랑 뭐가 다른지는 모르것네  

코드보기 : CRC-32 체크섬  


## 암호학적 해시 함수
해시값에서 원본 값을 찾는 게 사실상(너무 오래걸려서) 실행 불가능한 알고리듬.  
one-way function  
수학적 지식이 많이 요구됨. 따라서 이미 있는 해시 함수를 주로 사용함.  
원본 값 찾으려면 모든 조합을 모두 시도해봐야 함.  
보안 분야에서 다양한 용도로 사용함.

용도 예:  
메시지나 파일의 무결성 검사 (미러 사이트에서 파일 다운로드 하기)  
디지털 서명 생성 및 검증  
비밀번호 검증  
작업증명(proof-of-work, PoW): 블록체인 등에서 서비스 거부 공격(DoS)를 어렵게 하기 위해.  
일반 해시 알고리듬 대신으로 사용 가능 (대신 느림)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/23176679-beea-4c59-b025-8bda6013fe7b)  
어떻게 작동하고, 뭘 보장하려고 하는지 알면 됨.  

* 암호학적 해시 알고리듬의 추가 속성
1. 역상 저항성 (pre-image resistance)
2. 제 2 역상 저항성 (second pre-image resistance)
3. 충돌 저항성 (collision resistance)

* 역상 저항성
해시값으로 부터 원본 데이터를 찾기가 어려워야 함.  
즉, 원본 데이터를 같이 저장하지 않는 용도에 적합. (예: 비밀번호 저장)  
내가 저장한 거는 해시값이고, 그걸로 원본 복원하기 어려워야 함.  
비보안학적 해시 함수에서 본 비트 패킹은 역상 저항성이 거의 없음.  
낮은 역상 저항성을 이용하는 게 역상 공격(pre-image attack)  
무차별 대입 공격을 통해서만 해시값을 찾을 수 있는 것이 이상적!  
즉, 해시값으로 부터 패턴을 보기 어려워야 함.  
좋은 알고리듬이 필요한 이유(예: 산사태 효과), 해시값의 길이가 길수록 좋다.

* 제 2 역상 저항성
똑같은 해시값이 나오는 다른 입력값을 찾기 어려워야 함.  
(입력값, 해시값) 쌍을 이미 가지고 있을 때  
이 저항성이 낮으면 제 2 역상 공격에 취약  
즉, 내 계정의 해시값을 알 때, 유사한 비번도 알기 쉬우면 안됨.  

역상 저항성 보다 한 가지 정보가 더 있는 경우  
역상저항성은 해시값만 있는데, 제 2 역상 저항성은 입력값도 알고 있음.  

* 충돌 저항성
내가 가진 데이터 없어서 아무 문구나 해시 함수 돌려서,  
해시값이 똑같은 두 입력값을 찾기가 어려워야 함.  
해시값도 입력값도 주어지지 않은 경우  
이 저항성이 낮으면 충돌 공격에 취약.  

충돌 공격은 역상 공격들 보다 쉬움.  
이미 MD5와 SHA-1에 대해 실행 가능한 충돌 공격이 발견됨.  
MD5는 일반 컴퓨터로 몇 초면 될지도...   
모든 암호학적 해시 함수는 생일 공격(birthday attack)이 가능하기 때문.  
생일 공격은 무차별 대입 공격보다 빠름 (이유: 생일 문제)  

* 생일 문제 (birthday problem)
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/cd783d42-f91b-490b-a789-d0674087b86a)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/8980a8cf-7cc6-478a-9112-a23d242544ad)  

보안 이야기  
비번을 해시로 저장해야 하는 이유  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/5c9643f1-bbe1-4d5d-8d45-dba8c4afa1a0)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d5e79ddf-7ca4-48d2-8fb3-b9f31c8abee7)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/4290bbcd-9394-4f3c-9ba7-25b84113f410)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/cc54c1ee-b264-49ac-b5d0-ec8827dcd454)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/6dcf8c9e-6d75-4382-aab2-ae41929aa07c)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/3e687804-dce5-4a39-a1f5-efca96204cc9)  

비밀번호 덜 털리는 법  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d761e8b8-86d6-4f50-92ed-897e15a0c0d0)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/60084753-8dff-4540-98cc-106abbd44dea)  
다른 사람은 다른 랜덤한 스트링을 추가로 부여받음  
더 이상 레인보우 테이블에서 찾을 수 없음.  
각 비번마다 무차별 대입 공격 및 사정 공격을 해야 함.  
몇천만번 돌려서 N명중 한 명 알 수 있는거에서 1명당 몇천만번 돌려야 알 수 있게 제한됨.  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/de923aae-8671-4609-b87b-8cd7987d3e78)  
웹서버에서 메모리에만 들어가 있는 값임! 디비 털려도 안나옴!  
해커가 안가지고 있어서 거의 모든 공격을 무력화.  
단, 디비 털릴 때 웹 서버 메모리 까지 털리면 도루묵..  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/3eca46dc-1338-482d-a86d-fba08ef205ab)  

마지막 조언!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/ca886001-6082-49f5-8aec-d28a2ca5e98b)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/1fc04fd9-927e-4196-9e17-df67df8adf6f)  

코드보기: 비밀번호 해시 만들기  

