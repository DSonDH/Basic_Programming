# 예외 (exception)
사실 예외는 개체지향의 일부는 아니지만, 시기적으로 비슷한 시기에 나왔고,  
일부 소수파에서 같이 취급한 거래 ...  

## try / catch / finally
예외처리를 중구남방으로 하는거 올바르게 잡아보자 ...  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/b1498f11-0edd-427c-a8e5-1abaf63fad1b)  
try 다음에 catch는 꼭 있어야 되는데, finally는 옵션임.  
finally는 catch 실행되어도 나중에 실행되는 블록임.  
심지어 catch 블록에서 return을 하더라고 finally 블록 실행 됨 !  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/8ee86027-0f11-48d3-8c70-2654894c3c7e)  
Exception class는 모든 예외의 부모.  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/685f35c4-c690-4d45-9da8-3df366efe03a)  
왼쪽 블록에서는 FileNotFoundException 절대 실행 안됨.  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/279c02db-f160-4d00-a8c5-9b77bee93dc6)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/de8b3c9d-494b-4d25-92b0-5db6aa4e9cff)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/dee65c7a-d488-4a09-9da1-f7fcf277d4b6)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/69aedbb9-84d8-4494-a2cd-9723904bf7fa)  
파일을 찾을 수 없는 경우 IOException의 자식인 NoSuchFileException 발생함.  
따라서 첫 번째 catch문에서 해당 예외를 잡음(catch !)  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/3556e50b-cc88-4887-8166-71f1a930d4ec)  

finally 사용법  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/5688c6cc-f13a-4ad5-b086-cb5a60e6d1a6)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d762fed4-08ae-492b-8af3-78c37a4c7965)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/3b564d4c-1ec6-420b-a5a1-6f102aee0722)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/a0edae4a-71d0-4b23-8858-402f36984823)  

try, catch 바디 돌고나서 정리해야할 것을 정리할 때 유용함.  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/42c36276-7a00-4735-b1ac-45ef7adf481b)  
위 코드가 나쁜 이유는, garbage collector(GC)가 파일을 대신 닫아주기 때문임.  
GC가 참조되지 않는 FileOutputStream 개체를 해제. 그 때 GC가 호출하는 finalize()가 close() 메서드를 호출.  
그러나 그 시점이 언제인지 알 수 없음.  
또한 GC가 실행되기 전에 OS리소스의 한계에 다다를 수도 있음.  
이럴 때도 예외 발생함.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/542aec2c-0040-4d1d-bab1-6f325cc49786)  

close()를 호출하는 방법?  
직접 호출! 이 과목에서 사용하는 방법.  
try-with-resources : Java7 부터 사용 가능. 이 과목에서 다루지 않음. 궁금하면 직접 자바문서 확인하기!  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e6f2e158-0fd2-4c77-b902-54650e6eec12)  

정리  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/49947b80-6209-4d5e-bd0a-aba2e7f0eba8)  

참고  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/a01d68d9-5271-4c0f-b9a2-651a95b1acbf)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/fdb734d7-cbb5-4e1d-9954-94a3df05304b)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/daeee812-d5c8-4de4-8e11-35a10998d5be)  

## 나만의 예외 만들기

### 오류를 방치하면 일어나는 일


### 예외 처리를 제대로 하지 못하는 이유

## Java의 checked 예외

### checked 예외의 존재 의의

## 예외로부터 안전한 프로그래밍

## 근래의 예외 처리 트렌드

## 제어 흐름용으로 예외를 사용하지 말 것

## 예외적인 상황에만 예외를 사용해야 하는 경우

## 오류 상황, 예외 상황

## 4가지 오류 상황 처리법

### '무시'와 '종료' 방법

### '수정'과 '예외' 방법

## 예외는 OO의 일부가 아니다.

## 잘못된 예외처리보다 크래시가 낫다

## 프로그램 종료도 올바른 방법이다

## 4가지 처리법의 순위

### 예측 가능한 상황의 처리법

### 예측 불가한 상황의 처리법

