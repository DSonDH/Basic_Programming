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
## KNN

## 피쳐의 가중치와 정규화

# 기타 알고리듬 기법들
