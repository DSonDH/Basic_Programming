# 재귀함수
큰 문제를 반복 적용 가능한 작은 문제로 나눠 푸는 방법.  
어떤 함수가 매개변수만 바꿔 자기 스스로를 호출하는 방식으로 구현.  

장점  
가독성이 좋음  
코드가 짧음  
각 단계의 변수 상태가 자동 저장됨 (함수 스택 프레임 덕분)  
코드 검증도 쉬움.  

단점
재귀적 문제분석/설계아 안 직관적  
맹목적인 믿음이 필요 (수학적 귀납법)  
재귀 함수 호출이 너무 깊으면 스택오버플로 발생가능  
함수 호출에 따른 과부하  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/1b81bd1a-867b-4d78-9d42-362b325a255d)  
기본적으로 재귀함수 쓰느게 가독성 좋고 유지보수가 쉬움.  
스택오버플로우/성능문제 생길 가능성 크면 반복문으로 변환하기!  
모든 재귀함수는 반복문으로 작성가능. 복잡한 경우 데이터구조를 써야 함.  

## 꼬리재귀 (tail recursion)
꼬리 호출 (tail call)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/03b84d19-e91a-41c2-9582-5deed506512c)  
그런데, 꼬리 호출의 경우에 스택프레임을 유지할 실익이 있나?  
스택프레임은 중간에 저장하는 변수가 있을 때 필요한 건데,  
꼬리 호출은 타 함수로 반환 후 더이상 연산이 없으니 스택프레임에 저장 안해도 됨.  
-> tail call elimination / tail call optimization해줄 수도 있음 (언어 / 컴파일 따라 다름)  

tail recursion
꼬리 호출의 특수한 경우.  
마지막에 호출하는 함수 (꼬리 호출)이 자기 자신(재귀).  
꼬리 호출과 똑같은 최적화가 적용됨.  
``` java
int factorialRecursive(int n) {
  if (n <= 1) {
    return 1;
  }
  return n * factorialRecursive(n - 1);
}
```
얘는 반환 후 곱셈 연산 진행하니 아님! 스택프레임에 n이 저장되있어야 함.  
``` java
int factorial(int n) {
  return factorialRecursive(n, 1);
}

int factorialRecursive(int n, int fac) {
  if (n <= 1) {
    return fac;
  }
  return factorialRecursive(n - 1, n * fac);
  // 이 함수 호출이 마지막 명령어!
}
```
꼬리재귀함수 작성하기  
보통 꼬리 재귀 함수가 덜 직관적이지만 이런식으로 작성하는 경우가 종종 있다. 최적화 때문에.  
언어에서 최적화 지원 안해도, 꼬리 재귀는 반복문으로 쉽게 변경가능하므로 쓰는 실익이 있긴 함.  

* 코드보기 : 재귀함수로 총합 구하기

# Brute Force Algoritm
모든 가능한 경우의 수를 시도하는 알고리듬. 모로가도 서울만 가면 된다!  
좋은 알고리듬 조건 중 효율성을 고려하지 않은 알고리듬.  
문제에 따라 브루트포스보다 더 효율적인 알고리듬이 없는 경우도 있음.  
보통 가장 직관적인 문제 해결법이지.  
O(N)보다 시간 복잡도가 높은 알고리듬들이 많다.  
보안 분야가 이에 많이 의존해서 무조건 나쁜건 아님!  
ex: traveling salesman problem (TSP, 외판원 문제)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/01abb715-6d80-41d8-a670-a38689197842)  
알고리듬:  
1. 시작할 도시를 고른다
2. 모든 방문 순서 목록들을 만든다 (모든 경우의 수, O(N!))
3. 각 목록의 총 이동거리를 계산한다
4. 그 결과 중 총 이동거리가 가장 짧은 목록을 선택한다

기하급수적 증가 알고리듬의 문제점 : N이 커질수록 문제푸는 속도가 매우 느려짐  
실무에 사용하기 어려운 경우가 많음.  

## P vs NP
P분류 (P class) : 결정론적 튜링 기계에서 다항식 시간 안에 풀 수 있는 문제를 포함  
판정 문제들을 분류하는 방법 중 하나.  
판정문제: 입력 값에 대해 예/아니오 답을 내릴 수 있는 문제  

결정론적 튜링 기계: 어떤 명령어 실행 뒤, 다음 실행할 명령어가 확정됨.  
코어 하나에서 명령어를 순서대로 실행한다 생각할 것.  
즉, 코어 하나에서 실행되는 다항식 시간 알고리듬이 있는 문제는 P  
튜링 기계: 무언가 계산하는 기계를 대표하는 가상의 장치. 일반적인 컴퓨터 알고리듬을 수행할 수 있음.  

NP분류 (NP class) : 
NP: Nondeterministic Polynomial Time. Not P가 아님!  
'비'결정론적 튜링 기계에서 다항식 시간 안에 풀 수 있는 문제를 포함  
비결정론적 튜링 기계: 어떤 명령어 실행 뒤, 다음 실행할 명령어가 확정되지 않음.  
여러개의 다음 명령어를 병렬적으로 실행하는 기계라고 생각하면 좋대  

결정론적 튜링 기계에서의 NP문제  
: 일단 답이 있으면, 그 답이 맞는지 다항식 시간 안에 검증할 수 있음  
푸는데는(답을 찾는데는) 지수 시간이 걸릴 수도 있음.  
그래도 다항식 시간 안에 검증 가능  

deterministic 튜링머신을 사용한다는 가정하에,  
NP는 다항식 시간안에 답이 맞는지 검증할 수 있다는거고 P는 다항식 시간안에 답을 풀 수 있다는 말  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/0f546f65-e0fb-46da-bec0-75383e7f5a22)  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/8ae2ade7-9391-4c49-8256-9219bb285807)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/7f90d2d0-bcd0-43e5-bf31-19d687bb0d84)  

모든 P문제는 NP. NP안에 P 있다.  

### NP-complete (NPC, NP-완전)
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e7acb2c6-e953-4d1a-9fda-f41b464a12b7)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/0a2317ea-70d7-4c00-b9bd-c81e83af97c7)  
NP-완전 문제의 예 : 외판원 문제(판정버전), knapsack문제  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/b8c46562-65f1-498a-aa0f-e8f084855fc0)  

### P vs NP 문제
P와 NP가 같은지 아닌지를 논하는 문제.  
NP-완전 문제는 NP문제 중 가장 어려운 문제.  
NP-완전 문제 중 하나라도 다항식 시간 안에 풀 수 있다면 이 문제는 P가 됨.  
모든 NP문제를 NP-완전 문제로 다항식 시간 안에 환원할 수 있음.  
따라서 모든 NP문제가 P문제가 됨.  
-> 느려서 못풀던 그 많은  문제들을 효율적으로 풀 수 있게됨!!  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/7a7f5613-f21a-4742-a4c8-94e8553c1d9c)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/4a5be64f-59d6-4033-8a93-3fb59db39b75)  

# Search Algorithm

## binary search
