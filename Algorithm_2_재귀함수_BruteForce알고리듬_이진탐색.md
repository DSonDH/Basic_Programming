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

## P vs NP

# Search Algorithm

## binary search
