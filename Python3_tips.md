# Python

sort(item, key = lambda x: f(x))


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
```  

* collection module  
```python3
from collections import Counter
>>> Counter(["hi", "hey", "hi", "hi", "hello", "hey"])
Counter({'hi': 3, 'hey': 2, 'hello': 1})
```
