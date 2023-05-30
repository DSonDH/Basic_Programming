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

## 다중 상속

## 
