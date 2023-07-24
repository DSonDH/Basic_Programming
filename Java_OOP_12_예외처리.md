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
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/92c99cb9-c7c9-4dc4-a82d-af2b52bc053e)  
super()를 통해 RuntimeException의 생성자를 호출.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/fa09bb59-3cba-471b-9da3-cd4f4493cdb3)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e5867296-018c-4266-add6-618866ad5dc5)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e85f1478-8584-480e-a1e9-05ee455421b4)  
사실 Java에서도 Exception을 상속받아 커스텀 예외를 만들 수 있음. 옛날 방식인듯 ?  
요즘은 RuntimeException을 쓰는 일이 많대.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/87cf7ff6-fcad-47fe-b5c0-7133f2ec84a6)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/bf017a4d-ef5d-4c59-9cdd-0314a9b4cdde)  

### 오류를 방치하면 일어나는 일
Java의 예외는 크게 두 분류로 나뉨.  
다른 언어의 예외와 다른점이고, 역사적인 이유도, 정신적인 이유도 있음.  
우선 JVM환경에서 도는 프로그램에서 발생한 예외를 전처 처리(catch)안하면 어떻게 될까 ?  
예 : 분모가 0일 때 발생하는 예외.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/1c30bd71-1fc7-462f-8873-b02e979a6705)  
JVM에서 책임지고 프로그램을 종료시켜주기에 OS나 기계에는 아무 영향 없음.  

옛날  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/f321c0b7-c8fe-460d-a365-004f6532ee1b)  
근데, 웹서버 처럼 지속적인 조작 없이 알아서 실행돼야 하는 프로그램이면?  
자다가 깨서 회사 가서 재부팅 해야하는 .. 공포가 생길 수 있었던 시절임.  

요즘  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/7470c4c6-5e71-4c6b-817f-f976f1d2195b)  
요즘은 재부팅도 자동으로 되게 세팅할 수 있다.  
JVM이 보장해주던 안전성을 이제는 OS가 책임져주는 꼴!  

### 예외 처리를 제대로 하지 못하는 이유
과거에는 컴퓨터 재부팅에 대한 귀찮음이 컷어서 예외처리가 최우선시 됬었던거 같음.  
그래서,  
"함수에서 오류코드를 반환해서 오류 상황을 알려주는건 절대 금지!
함수에서 반환하는 것은 무조건 올바른 값  
문제가 있으면 무조건 예외 던지기!, 호출자는 그 예외를 제대로 처리해야 함!"  
같은 주장을 하는 사람이 있음...  

근대 문제는 수십년이 지나도록 이걸 제대로 한 사람이 드뭄.  
물론 시도는 했지만, 사람이 이해하기 힘들어서 실패 ...  
왜냐하면 ...  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/051b3b8c-a47c-4d5d-88f7-8ed5ca2cdac4)  
어떤 함수가 예외를 던지는지 알아야 하는데, 거의 불가능함!  
그래서 함수 위 주석으로 표기하기도 하는데, 사람들이 주석을 잘 안읽음 ... ㅋㅋㅋ  
인간에 대한 이해 없이 만든 방법론은 실패하기 마련...  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/74e4abf9-2cd8-4bcb-b37d-edc00c49bcda)  

## Java의 checked 예외
Java는 이에 좀 더 대비되어 있었음!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/bac242ba-6521-4441-9968-75a9fe76382d)  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/80f72d5b-52fe-4be9-9ea1-fdb2c9d38e3a)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/af2a411b-d9a7-423a-ae31-a169ef3afb6d)  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e918ae13-a0a6-44d4-948a-7ca033bd12fc)  
unckecked 예외는 throws UserNotFoundException 안붙여도 됨.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/6c30c026-c54f-41bb-9c73-4920b45d8604)  

만약 findUser()를 호출하는 메서드에서도 UserNotFoundException을 처리하고 싶지 않다면?  
즉 예외를 상위 호출자로 던져버리고 싶으면?  
try catch 빼고,  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c13d89e1-0404-4c75-87b1-6d2b00e88fa1)  

구분 방법  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/27bd2497-a902-4828-b1c6-33c2ec07344e)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/9c9740e8-a47b-44ee-9469-1c2b7e521393)  

### checked 예외의 존재 의의
언제 어떨걸 쓸까? 과거에는 checked 예외를 선호했고, 의도는 좋았지만 다소 실패함.  
API제작자가 이건 클라이언트가 반드시 처리해야 할 예외라고 알려주는 용도였거든.  
근데, 처리하라는 의미가 다양함.  
1. 프로그램을 그냥 종료?
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/a82f5699-c05f-44ed-b449-50bc15c9a524)  
단계가 올라갈수록 수십 수백개 던져야함. 사람에 대한 이해가 부족한 것.
오히려 unchecked 예외를 사용하면 메서드 시그내처가 간결해지므로 이 가정은 아님.  

2. 예외를 무시(swallow)하고 진행?
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/82f20c9e-1945-4daa-bfdc-4b3583f6fec0)  
이럴거면 예외를 던질 이유가 없음.  

3. 어떻게든 프로그램을 장상상태로 회복하라!  
과거 Java진영에서 굉장히 선호하던 방식.  
최상위 클래스인 Exception이 checked 예외인 것도 이 때문일지도?  
unchecked 예외(RuntimeException)이 기본이 아니다!  
덕분에 Java를 접할 떄 unchecked예외가 있는지 모르는 사람도 있음.  
나만의 예외를 만들 떄 언제나 Exception을 상속.  
그 결과 무조건 throws절을 넣어야 한다고 생각할수 도 있음  
프로그래밍 언어의 기본 동작이 중요한 이유!  

## 예외로부터 안전한 프로그래밍
그런데, 회복이 쉽지 않다.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/92653082-3210-4c23-8ad0-e67cd6a28f63)  
정말 번거로움! 이걸 모든 코드에 적용하기 쉽지 않음.  
그렇지만, 정~~말 필요한 곳에는 넣어야 함.  
그렇지 않은 많은 코드 부부은 그냥 재부팅하도록 ...  

## 근래의 예외 처리 트렌드
1. 그냥 unchecked 예외를 쓰자고 함.  
다시 다른 언어와 똑같아짐.  
그 결과 아까 호출 트리에서 봤던 문제는 못고침.  
즉 누가 어떤 예외를 던지는지 한눈에 안보임.  

2. 예외로부터 안전한 최선의 방법은 재부팅
예외로부터 회복하지 않는다.  
단, 디버깅에 필요한 정보를 최대한 남기고 프로그램 종료.  
이런 변화에 따라 예외를 얼마나 세분화해서 처리해야 하는가? (exception granularity)  
이 질문에 대한 의견도 바뀌기 시작함.

예전 :  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/256646d3-4e4f-4342-a9f1-15fa9684cd4c)  

요즘 : 
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/f05bf6fa-bfb4-4539-b9e3-c7c9b5619400)  


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

