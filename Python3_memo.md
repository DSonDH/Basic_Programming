# Python
primitive는 이용 가능한 가장 단순한 요소들이다.  
프로그래머에게 이용가능한 가장 작은 processing단위이거나 언어에서 표현의 원자 요소가 될 수 있다.  
덧셈, 뺄셈 같은 가장 단순하고 원초적인 연산을 primitive operation이라고 함..  
python은 primitive type이 존재하지 않는다. 모든 데이터는 object나 object산의 관계로 표현된다.  


## module import 관리
[상대경로, 절대경로, __init__.py와의 관계](https://daco2020.tistory.com/62)


## 변수 명 규칙
[under bar 관련 변수명 규칙](https://eine.tistory.com/entry/%ED%8C%8C%EC%9D%B4%EC%8D%AC%EC%97%90%EC%84%9C-%EC%96%B8%EB%8D%94%EB%B0%94%EC%96%B8%EB%8D%94%EC%8A%A4%EC%BD%94%EC%96%B4-%EC%9D%98-%EC%9D%98%EB%AF%B8%EC%99%80-%EC%97%AD%ED%95%A0)

sort(item, key = lambda x: f(x))

## scope 내 변수들 확인 (local, global, ...)
globals(), locals(), vars(), and dir()  

## python modules
.

### subprocess
현재 소스코드 안에서 다른 프로세스를 실행하게 해줌. 그 과정에서 데이터 입출력을 제어함  
![image](https://github.com/user-attachments/assets/85b07d00-ffcc-47ff-9a7e-92ee5c1682a2)  

subprocess.run() : subprocess의 기본이되는 메서드, python 3.5부터 사용가능  
arguments:  
args: 이곳에 써있는 명령어를 실행  
stdin, stdout, stderr: 표준입력, 출력, 오류를 설정 (데이터를 중간에 가로채서 다른 곳으로 보낼 수 있음)  
input: 입력데이터를 설정  
shell: 쉘 화면에 출력을 할 것인지 (윈도우 쉘 명령어를 쓰려면 반드시 True여야 함)  
cwd: 현재 실행중인 디렉토리 반환  
check: True면 CalledProcessError 예외 발생함. run()으로 해당 프로세스가 정상종료되면 CompletedProcess가 선언되서  
결과가 0으로 리턴되야하는데, 이를 0 아닌 값으로 만들겠다는 뜻. 선언된 예외처리에 run()의 입력값과 데이터가 보관됨.  
text: True면 결과값을 string형태로 출력  
등등 ...  


### select module
소켓 프로그래밍에서 I/O multiplexing을 가능하게 하는 모듈.  
I/O multiplexing: 하나의 전송로로 여저 종류의 데이터를 송수신하는 방식.  
둘 이상의 클라이언트가 동시에 접속해도 잘 동작하도록 함, 클라이언트와의 접속이 끝나도 서버 종료되지 않도록 함.  


## logging 
우리 프로그램이 어떤 상태를 가지고 있는지, 외부 출력으로 개발장 등이 눈으로 직접 확인하는 것.  
DEBUG < INFO < WARNING < ERROR < CRITICAL 다섯가지 등급이 사용됨.  
Handler : 내가 로깅한 정부가 출력되는 위치를 설정하는 것.  


## 데몬(Daemon) 
멀티태스킹 운영 체제에서 데몬은 사용자가 직접적으로 제어하지 않고, 백그라운드에서 돌면서 어려 작업을 하는 프로그램을 말한다.  
프로세스 형식으로 실행되고, 데몬이라는 표시를 위해 뒤에 d가 붙는다고 함 (syslogd 등).  
유닉스 계열에서는 시스템의 기능을 제공하거나 백그라운드에서 항시 실행되는 프로그램을 뜻하고,  
다른 운영체제에서는 시스템 프로세스라 부름.  
대부분 시스템의 시작과 끝을 함께하므로 대개 관리자 권한으로 실행되어 네트워크 요청, 하드웨어  
동작 등 여러 기능 담당.  
이런 데몬은 크게 Standalong 혹은 Super daemon(xinetd) 두가지 방법으로 동작 함.  



## 알고리듬  
n 크기 이하 모든 소수 찾기 : 에라토스테네스 체  
n 의 약수 찾기 : ???  



## 타입별 내장함수
* string type
``` s.lower().count('p') ```  
!! string은 immutable 이므로 index별 재 allocation 불가능. 리스트로 바꾸면 가능.

```python3
'ooyyy'.count('y')
>>> 3

chr(string)
: Return the string representing a character whose Unicode code point 
is the integer i. For example, chr(97) returns the string 'a'

ord(number)
: 하나의 유니코드 문자를 나타내는 문자열이 주어지면 해당 문자의 유니코드 코드
포인트를 나타내는 정수를 돌려줍니다. 예를 들어, ord('a') 는 정수 97 을 반환
```  



* list  
```python3
>>> [1, 1] + [1, 2, 3]
[1, 1, 1, 2, 3]

test = [1, 2, 3, 4]
test[-2:]
>>> [4]

test[-200:]
>>> [1, 2, 3, 4]  # 리스트 크기 초과해도 됨.

test[:200]
>>> [1, 2, 3, 4]  # 리스트 크기 초과해도 됨

test[4]
>>> IndexError: list index out of range

test[-4]
>>> 1

test[-5]
>>> IndexError: list index out of range
```

pop : 해당 index 자리 제거  
remove : 해당 값 제일 왼쪽값 제거  
```python3
>>> a = [1, 1, 1, 2, 3]
>>> a.count(1)
3

>>> ['ox', 'o', 'x', 'oxoxox'].count('ox')
1
```


* set  
create empty set  
```python3 
set()
{}  # empty dictionary not set

>>> s1 = set([1, 2, 3])
>>> s1.add(4)
>>> s1
{1, 2, 3, 4}

>>> s1 = set([1, 2, 3])
>>> s1.update([4, 5, 6])
>>> s1
{1, 2, 3, 4, 5, 6}
``` 

* dictionary
<br>
<br>
## 주의사항
* python for loop iterable data type change cause unexpected behavior  
for loop 돌도록 하는 변수를 loop 내에서 바꾸면 다음 루프에서 바뀐 아이로 실행되서 코딩이 어려워질 수 있음
![image](https://user-images.githubusercontent.com/15919242/206884883-dd7947f0-8383-40b5-81a9-4b594d46533b.png)  
for loop 변수값을 바꾸던지/pop 등으로 길이 변경되게 하던지, 

## 기타  
* python combination module  
![image](https://user-images.githubusercontent.com/15919242/206885055-05410248-b6ee-4fa2-813f-c244a668a120.png)

* for -else 문은, for loop를 break하지 않으면 else가 실행되는 것임. for iterable data가 없을때 else가 실행되는게 아님.

* 제곱 관련 loop돌면서 판별할 때 역으로 sqrt로 판별해버리면 loop 안돌아도 되는 경우가 있음  
  
* int(str, base) : str을 base 진법 수로 바꿔줌. base 기본값 10.
  
* map, lambda
```python3
list(map(lambda x:x*x, range(1,6)))

>>> from functools import reduce   # 파이썬 3에서는 써주셔야 해요  
>>> reduce(lambda x, y: x + y, [0, 1, 2, 3, 4])
10
>>> reduce(lambda x, y: y + x, 'abcde')
'edcba'

>>> list(map(lambda x: x ** 2, range(5)))     # 파이썬 2 및 파이썬 3
[0, 1, 4, 9, 16]

>>> list(filter(lambda x: x < 5, range(10))) # 파이썬 2 및 파이썬 3
[0, 1, 2, 3, 4]


# int함수를 unpacking에 일괄 적용하는 경우
# for loop 쭉 풀어쓰는 것 보다는 list comprehension으로 처리가능한 간단한 경우
# 함수명이 date_cnvrt보다 to_days로 직관적인 경우.
def to_days(date):
    year, month, day = map(int, date.split("."))
    return year * 28 * 12 + month * 28 + day

def solution(today, terms, privacies):
    months = {v[0]: int(v[2:]) * 28 for v in terms}
    today = to_days(today)
    expire = [
        i + 1 for i, privacy in enumerate(privacies)
        if to_days(privacy[:-2]) + months[privacy[-1]] <= today
    ]
    return expire

```  



* collection module  
```python3
from collections import Counter
>>> Counter(["hi", "hey", "hi", "hi", "hello", "hey"])
Counter({'hi': 3, 'hey': 2, 'hello': 1})
```

hehe
