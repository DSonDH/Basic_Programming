# 유한 상태 기계 (Finite State Machine, FSM)
상태에 따라 다른 동작을 하는 추상적인 기계.  
여러 상태가 있음 (ex: 문이 열려 있음, 문이 닫혀 있음 ...)  
기계는 동시에 두 상태일 수 없음  
특정 조건 만족 시 다른 상태로 변이할 수  있음 (transition, 전이)  
외부 입력, 내부 상태 변화  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/36a2c140-63a6-412e-9ae6-69052f59f300)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/5d8802b4-b63d-4771-98c4-89860e0d9675)  

유한 상태 기계의 용도: 엘리베이터, 교통신호등, 세탁기, 열차 ...  
직원이 ID를 입력할 때 올바른 포맷인지 검사할 때.  
웹브라우저 안에서! DB까지 긁기엔 너무 무거우니 간단한 유효성 검사하기!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d520a11b-2099-475e-b91e-8f18396e737e)  
이런걸 간단히 정규식으로 판단할 수 있음 !!  

# 정규식 (regular expression, regex)
문자열 검색 규칙을 정의하는 문자열  
 - /abc/: "abc" 를 찾음
 - /a{3}/: "aaa"를 찾음
 - /abc|def/: "abc"나 "def"를 찾음

사용자 입력을 검증하거나 문서에서 정보를 추출할 때 주로 사용.  
정규식 문법 그 자체가 방대하고 복잡한 언어!  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/47e92f35-f727-4148-b16c-89f4c522a5cc)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/268e74b5-baf2-42c4-8c99-5edd9aee4bbe)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/5dbd8906-237e-4587-9c92-4c04ab5d91c9)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/50191e4b-836a-4acd-9870-ce218e09aafd)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/b4ec704b-cd10-4ef0-9d23-7c1efcbc5482)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/0b04c346-716f-40d2-a455-36beadc01dfb)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/3f1bed11-e93c-4b8d-973e-63af459accb3)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/2c1005be-222b-4410-a9a2-298280740cd0)  
d: digit  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c36cf184-f64e-4ae0-aa87-a6bd7b05e194)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/cb9aa641-f8f4-45cc-baa1-815720d0ca30)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/a37d5062-67e7-4d4d-a9f1-50faf27540ca)  

정규식은 상태 기계!  
정규식 처리기의 기본 동작: 첫 번째 매치만 찾아서 반환! 대소문자 구분 등  
플래그를 통해 기본 동작을 바꿀 수 있음. 
모든 매치를 찾아서 반환, 대소문자 구분 안함, 여러 줄(multiline) 모드 등  
궁금하면 regex flags 검색해보기!  

정규식 사용법: 간단하게 정규식으로 표현가능하면 쓰고, 아니면 직접 for, if 써가며 코딩하기!  

# 패턴 인식
## KNN (K-Nearest Neighbor)
귀납적 학습!  
누군가의 지도에 따라 사물의 분류법을 배움  
충분히 학습이 된 모델은 새로운 사물을 스스로 분류할 수 있음  
이는, 사물의 어떤 특징이 그 분류를 결정짓는지 알게되며 생기는 현상임.  

이런 supervised learning 알고리듬 중 하나.  
훈련 데이터에 정답이 있고, 새로운 데이터에 정답을 달고자 함.  
주로 classification에 사용하지만 regression에도 사용할 수 있음.  

1. 훈련 데이터 로딩
2. k 값 선택
3. 입력값과 가장 비슷한 (거리가 가장 가까운) 훈련 데이터 k개 찾음
4. 결정을 내림
classification: 가장 많이 등장하는 그룹의 레이블 반환
regression: k개 데이터의 평균 반환

데이터끼리 비슷한걸 어떻게 구하나? 거리개념을 고안하면 됨!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/8f3f2bec-267a-4702-bdc9-257ed19275ae)  

피쳐의 가중치와 정규화  
거리를 계산할 때, 각 피쳐 고유의 스케일이 다르면, 단위가 큰 피쳐가 무조건 거리가 크게 나옴.  
따라서 피쳐별로 정규화를 통해 동일한 범위에 맞춰서 거리를 판단함.  

KNN 사용례: 이미지 인식 및 분석, 연봉 예측, 문서 분류, 주가 예측 등...  

# 기타 알고리듬 기법들
선형 계획법 (linear programming, LP)  
선형으로 표현해야 하는 수학 모델에서 최고 결과를 성취하는 기법  
선형 최적화라고도 함  

병렬 알고리듬  
여러 코어/컴퓨터를 사용하여 동시에 여러 연산을 수행하는 방법  
CPU에 기본으로 탑재된 코어 수가 둘 이상이 되면서 흔해짐  
모든 문제를 병렬로 풀 수는 없음  
데이터 분할이 용이해야하고, 서로 의존관계가 없는 하위 문제로 분할 가능해야 함  
