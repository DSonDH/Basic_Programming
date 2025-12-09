# 벡터(Vector)
Standard Template Library (STL)컨테이너 중 하나.  
모든 컨테이너에 적용되는 표준 인터페이스  
메모리 자동 관리, 템플릿 기반  

벡터란: 어떤 자료형도 넣을 수 있는 동적 배열 (자동으로 늘려줌)  
기본(primitive)데이터, 클래스, 포인터 넣을 수 있음  
그 안에 저장된 모든 요소들이 연속된 메모리 공간에 위치.  
요소수가 증가하면서 자동으로 메모리 관리해줌.  
어떤 요소에도 임의로 접근(random access) 가능  
<img width="683" height="332" alt="image" src="https://github.com/user-attachments/assets/1b7d2062-5b64-4739-9ddd-ea7e44da44a5" />  
vector<int>라는게 템플릿 이라고 함  
<img width="551" height="264" alt="image" src="https://github.com/user-attachments/assets/d498173e-dd8f-4443-aa98-3d1052e57d68" />  
<img width="653" height="274" alt="image" src="https://github.com/user-attachments/assets/0f5bb23b-3211-499e-95c8-7e09ccfb4dd7" />  

복사생성자와 같음  

## 요소 삽입/삭제, 용량, 크기, 요소 접근, 반복자
제일 마지막에 요소 추가  
<img width="513" height="231" alt="image" src="https://github.com/user-attachments/assets/89faadfd-da0b-48a0-b0e0-416e8451d81c" />  

pop_back(); // 맨 뒤에 요소 제거  
중간에 요소 제거는 조금 복잡함.  

capacity vs size  
capacity: 벡터에 할당된 요소 공간 수  
size: 실제로 들어있는 요소 수  

벡터 용량늘리기: reserve(\<size\>);  
용량이 증가해야하면 새로운 저장 공간을 재할당하고 기존 요소들을 모두 새 공간으로 복사  
불필요한 재할당을 막기위해, 벡터를 생성한 직후에 이 함수를 호출하자!!!! (미리 넉넉히)  

요소 하나에 접근하기  
<img width="526" height="237" alt="image" src="https://github.com/user-attachments/assets/0a83ddb2-cdb8-4336-8279-cdec5f95fbb8" />  

이 방식은 벡터에만 쓸 수 있음.  
map에서는 인덱스로 operator[]를 쓸 수 없음.  
STL컨테이너를 순회할때는 iterator를 쓰는게 표준 방식임.  
``` cpp
#include <iostream>
#include <vector>

int main()
{
	std::vector<int> scores;
	scores.reserve(2);

	scores.push_back(30);
	scores.push_back(50);

	for (std::vector<int>::iterator iter = scores.begin(); iter != scores.end(); ++iter)
	{
		// do something
	}
}
```

반복자(iterator)  
<img width="626" height="158" alt="image" src="https://github.com/user-attachments/assets/56417ec0-d5ee-4fcc-8ede-b46dc3d6da07" />  
begin(), end()  
<img width="851" height="352" alt="image" src="https://github.com/user-attachments/assets/1d73ade0-89ce-49f8-bdb4-9f509f4ab9c3" />  

c string맨 뒤는 \0인것처럼 마지막 요소 다음을 가리킬 필요가 있음.  

코드보기: 내 점수 추가, 출력  
``` c++
#pragma once

#include <vector>

namespace samples
{
	void PrintScores(const std::vector<int>& scores);

	void VectorAddingElementsExample();
}
=====
#include <iostream>
#include <vector>
#include "VectorAddingElementsExample.h"

using namespace std;

namespace samples
{
	void VectorAddingElementsExample()
	{
		vector<int> scores;
		scores.reserve(5);

		scores.push_back(30);
		scores.push_back(50);
		scores.push_back(80);
		scores.push_back(65);
		scores.push_back(73);

		PrintScores(scores);

		scores.pop_back();
		scores.pop_back();

		PrintScores(scores);

		scores.resize(10);  // 크기도 용량도 10으로 됨. 빈공간은 0으로 채움

		PrintScores(scores);
	}

	void PrintScores(const vector<int>& scores)
	{
		cout << "Current elements : ";
		for (vector<int>::const_iterator iter = scores.begin(); iter != scores.end(); ++iter)
		{ // 입력인자 scores가 const라서 const_iterator써야만 함
			cout << *iter << " ";
		}
		cout << endl;

		cout << "Current capacity : " << scores.capacity() << endl;
		cout << "Current size : " << scores.size() << endl << endl;
	}
}
```

## 역방향 반복자, 특정 위치에 요소 삽입/삭제
begin(), end(), rbegin(), rend()  
<img width="496" height="280" alt="image" src="https://github.com/user-attachments/assets/0cdb8398-8cde-454f-8293-a8e5b18f3089" />  
<img width="773" height="262" alt="image" src="https://github.com/user-attachments/assets/c20b9aaa-225d-45e4-b6a1-5181282cdc53" />  

특정 위치에 요소 삽입하기  
<img width="769" height="250" alt="image" src="https://github.com/user-attachments/assets/8279a991-2411-43b8-8c28-579037b8b65d" />  
``` cpp
std::vector<int> scores;

scores.reserve(4);
scores.push_back(10);
scores.push_back(50);  // 10, 50
scores.push_back(38);
scores.push_back(100); // 10, 50, 38, 100

std::vector<int>::iterator it = scores.begin();

it = scores.insert(it, 80); // 80, 10, 50, 38, 100
```
it++;하고 insert했다면, 10 80 50 38 100이 되었을것.  

복사 문제  
<img width="821" height="309" alt="image" src="https://github.com/user-attachments/assets/048ce873-a3db-4c9e-bc9e-7329eead0a5f" />  
3은 size, 4는 capacity  
<img width="815" height="298" alt="image" src="https://github.com/user-attachments/assets/fb1d01d8-5318-4e17-b345-8ae47997b4a8" />  
즉, 기존 배열을 통째로 복사하고 있다가, 순서에 맞게 하나씩 재할당 해주는것.  

재할당, 복사문제  
<img width="813" height="292" alt="image" src="https://github.com/user-attachments/assets/ef7025a5-e5c8-40c2-9a9d-7d74bcdaf23e" />  
역시 통째로 복사하고 메모리 찾아서 재할당  
**이 연산이 비싸므로 미리 크게 할당하는게 좋음**  

특정위치에 있는 요소 삭제  
``` cpp
std::vector<int> scores;

scores.reserve(4);
scores.push_back(10);
scores.push_back(50);  // 10, 50
scores.push_back(38);
scores.push_back(100); // 10, 50, 38, 100

std::vector<int>::iterator it = scores.begin();

it = scores.erase(it); // 50, 38, 100

// 참고
while (it != scores.end())
// while 쓴 이유는 erase하면서 end()기준이 움직여서 그럼.
// for loop 쓰면 위험: erase 후의 it는 end인지 아닌지와 무관하게 무효화된 iterator에 ++를 적용하는 순간 undefined behavior
{
	if (*it == 38)
	// *it 는 원본 참조한것
	// Score score = *it 처럼 primitive형 아니라 클래스 개체였다면
	// 원본 참조한거를 가지고 새로운 score를 복사해서 생성한 것이다.
	// 그래서 score를 암만 바꿔도 scores내용물은 바뀌지 않는다. (아래 Object vector참고)
	{
		it = scores.erase(it);
		// 여기는 ++it를 추가하면 안됨
		// 지워진 자리에 다음 요소가 자리를 채워주므로, 추가로 it를 옮기면
		// 지금 채워진 요소를 검사 안하는것임
	}
	else
	{
		++it;
	}
}
```
요소 앞으로 한칸씩 당기므로 복사  
<img width="809" height="241" alt="image" src="https://github.com/user-attachments/assets/de66eff3-26f0-4919-aca5-6ba4a320e436" />  
(재할당은 메모리 공간 새로 잡는걸 말함)  
(순서 상관없는 배열이면, 마지막 요소를 맨앞으로 땡겨오면 O(n)대신 O(1)으로 처리 가능)  

벡터 교환하기  
``` cpp
std::vector<int> scores;
scores.reserve(2);

scores.push_back(85);
scores.push_back(73); // 85, 73

std::vector<int> anotherScores;
anotherScores.assign(7, 100); // 100, 100, 100, 100, 100, 100, 100
scores.swap(anotherScores);  // scores: 100, 100, 100, 100, 100, 100, 100
                             // anotherScores: 85, 73
```  
요소 대입: n개의 \<data\>값을 벡터에 넣는다. assign(size_t n, \<data\>);  
두 벡터 교환: 두 배열 내용을 바꿈. swap(vector& other);  
구현은, 메모리 주소랑, size, capacity정보만 바꾸면 됨.  

크기 변경, 모든 요소 제거하기  
``` cpp
std::vector<int> scores;
scores.reserve(3);

scores.push_back(30);
scores.push_back(100);
scores.push_back(70); // 30, 100, 70

scores.resize(2);

for (int i = 0; i < scores.size(); ++i)
{
	std:cout << scores[i] << " "; // "30 100"
}
```
size작아져서 초과분(마지막꺼) 날라감. 기존 용량보다 크면 재할당.  
reserve는 줄이는거 없음. 그냥 유지됨. resize는 줄이기 가능.  

모든 요소 제거: clear();  
size는 0이 되고 용량은 변하지 않음.  

Object 벡터  
<img width="861" height="362" alt="image" src="https://github.com/user-attachments/assets/d1352185-5ce1-4bbe-b4a5-a18712651a34" />  
실제 scores안에 Score개체가 들어감. 힙에 할당한 주소를 가리켜서 4바이트만 있는게 아님!! score에 mScore 4바이트,  
string(capacity 4바이트, size 4바이트, c_str 주소 4바이트)  
여기서 string은 컨테이너에서 나온 개념.  
16바이트가 4개 : 64바이트  

**코드보기: 개체 벡터 (생각할거 좀 있어서 중요한듯. 동영상 다시 봐보기)**  

포인터 벡터  
<img width="811" height="291" alt="image" src="https://github.com/user-attachments/assets/5cfa05c5-a66e-4cc5-b685-9d4ea63ad545" />  
개체를 직접 보관하는 벡터의 문제점은 복사에 어마어마한 리소스가 쓰일 수 있다.  
그러면 포인터로 저장하면 해결될듯?  
<img width="438" height="290" alt="image" src="https://github.com/user-attachments/assets/eb05bc96-608c-4bd3-bb75-9d9918737c4b" />  
포인터 저장의 문제점?  
<img width="814" height="302" alt="image" src="https://github.com/user-attachments/assets/7c9000b8-6304-4d4e-a621-6db62e5f589a" />  
재할당이 필요하면,  
<img width="799" height="263" alt="image" src="https://github.com/user-attachments/assets/2029dcb0-de72-4b0e-aeec-c494fd183e1c" />  
기존 10이랑 "C++"을 다시 할당한게 아니라서 빨라짐.  
그러나, 모든 요소에 대해 delete꼭 호출할 일이 늘어남.  
<img width="781" height="341" alt="image" src="https://github.com/user-attachments/assets/28a15eea-19bd-42ae-b28c-3fcfeb0190fd" />  

코드보기: 포인터 벡터 동영상강의 다시 봐보기  

벡터의 장단점  
: 순서 상관없이 요소에 임의적으로 접근 가능  
제일 마지막 위치에 요소를 빠르게 삽입 및 삭제  
중간에 요소 삽입 및 삭제는 느림  
재할당 및 요소 복사에 드는 비용이 있음  

# 맵(Map)
key, value 쌍으로 요소를 만듦. (해쉬맵이 아님!!!!!)  
키는 중복될 수 없음.  
C++ 맵은 자동정렬되는 컨테이너... (이진탐색트리 기반 오름차순)  
<img width="642" height="305" alt="image" src="https://github.com/user-attachments/assets/ee92e80f-a456-4980-82e1-88479ce8f442" />  
<img width="678" height="292" alt="image" src="https://github.com/user-attachments/assets/6c436463-a2a2-47ed-97ed-dffc70b71514" />  
복사생성자 호출함.  

## std::pair, 요소 삽입
<img width="676" height="172" alt="image" src="https://github.com/user-attachments/assets/583ee528-e29c-4a84-9dd9-dd2cabcf2433" />  

pair의 타입을 지정해줌.  
iter->first하면 첫번째 요소 (키), iter->second하면 두번째 요소 (value) 얻어짐.  

insert  
<img width="740" height="353" alt="image" src="https://github.com/user-attachments/assets/2d4b4390-220c-4573-a626-a2e5a04d579c" />  
키를 중복으로 삽입할 수 없음! 이미 있으면 <iterator, false> 반환됨.  

operator[]  
<img width="617" height="294" alt="image" src="https://github.com/user-attachments/assets/5214abf8-ee1c-4c8f-9e57-91fe4907c5ea" />  
원본 바뀌게 할려고 keydp 대응하는 값을 참조로 반환받음.  
이 방식은 이미 있는 key의 value를 바꿔버림.  
없는 key값을 불러오면, 갑자기 기본값인 0으로 (k, v)삽입해서 없는걸 불러와버림..;;;  

자동 정렬  
<img width="848" height="243" alt="image" src="https://github.com/user-attachments/assets/6a96e4cb-ef0c-4125-8d51-b878181b5ded" />  

## 요소 찾기, 두 맵 교환, 맵 비우기, 요소 제거, 두 키를 비교하는 함수  
요소 찾기  
<img width="668" height="313" alt="image" src="https://github.com/user-attachments/assets/5b6d96a4-b4b9-4e7e-be10-f1dce119cca9" />  
end면 못찾은거임 (모든 종류의 컨테이너 호환하려고)  
find()  
<img width="754" height="201" alt="image" src="https://github.com/user-attachments/assets/e4354c1d-03f1-40af-9d0a-82ff1f9430a0" />  

swap(), clear()  
<img width="770" height="320" alt="image" src="https://github.com/user-attachments/assets/8fce764a-5ffe-4b48-b20c-68da4db72d90" />  

erase()  
<img width="700" height="246" alt="image" src="https://github.com/user-attachments/assets/2ffd7a9e-2ab5-4699-8686-6b87deaf27a6" />  

예: 개체를 키로 사용  
<img width="823" height="242" alt="image" src="https://github.com/user-attachments/assets/2aa99114-9d51-4ab6-8a7c-ad333e8e24e5" />  
: 뭔가 컴파일이 안됨. STL맵은 항상 정렬된다.   
이는 두 키를 비교하는 함수가 필요한 것임 operator<()  
<img width="553" height="182" alt="image" src="https://github.com/user-attachments/assets/6addd0cb-a427-45e8-a866-0bf0a25c2101" />  
클래스 안에 구현해줘야 함.  

map만들 때 comparer넣어줄수도 있음  
<img width="716" height="214" alt="image" src="https://github.com/user-attachments/assets/144f1ab8-cc4d-422f-b518-c2c5e5f0b67d" />  
그러곤 map<>에 추가해주는거임.  
저 커스텀 클래스를 내가 건드릴 권한이 없으면 이렇게 하고,  
내가 만든거라면 oop에 더 가까운 위에 방법 (클래스 내에 operator추가)이 좋음.  

**코드보기: 사용자 정의 자료형을 키로 사용 (시험문제 내기 좋은듯.. 다시 보기)**  

질의응답  
<img width="707" height="701" alt="image" src="https://github.com/user-attachments/assets/474334c8-bef3-4bb2-9616-2a73aeb6faec" />  

## 맵의 장단점  
<img width="834" height="191" alt="image" src="https://github.com/user-attachments/assets/a0a12f65-7f7d-4a92-881c-821a2dcae29b" />  
탐색은 O(logN). 해쉬맵이었으면 O(1)이었을것을... (C++11에 해결책이 있음)  

퀴즈
``` c++
#include <iostream>
#include <map>
#include <string>

int main()
{
    std::map<std::string, int> scores;

    if (scores["Lulu"])
    {
        scores["Lulu"] = 50;
    }
    else
    {
        scores.insert(std::pair<std::string, int>("Lulu", 100));
    }

    // ...

    return 0;
}
// ("Lulu", 0)먼저 들어가고, else에서 100으로 업데이트됨.
```

# 셋(Set)  
정렬되는 컨테이너. 중복되지 않는 키를 요소로 저장함. (키 이자 value)  
역시 오름차순 이진탐색트리 기반, 맵과 거의 같다  
<img width="735" height="334" alt="image" src="https://github.com/user-attachments/assets/9a9f6d68-9d5a-4517-96e9-c291ecc88ee7" />  

# 큐(Queue)  
first in first out (FIFO) 구조, Push, Pop  
<img width="758" height="334" alt="image" src="https://github.com/user-attachments/assets/9f220fcc-0f4e-4b46-b847-25fddceba092" />  
C++은 pop해서 개체를 반환하지 않는다. 따로 변수로 저장하고 있어야 한다.  

front(), back()  
<img width="828" height="315" alt="image" src="https://github.com/user-attachments/assets/e0c9d03a-ae3a-42fd-898f-9db29f64f36b" />  

size(): 들어있는 요소 수 반환, empty(): 비어있으면 true 아니면 false  

# 스택(Stack)  
last in first out (LIFO) 구조, Push, Pop  
<img width="526" height="325" alt="image" src="https://github.com/user-attachments/assets/5de45593-69ef-4d15-82b2-dc2c03ccca18" />  

top(): stack 가장 마지막에 저장된 요소를 참조로 반환  
bottom()함수 없음.  

# 리스트(List) (Doubly Linked List) 
<img width="758" height="274" alt="image" src="https://github.com/user-attachments/assets/e73f752c-2525-45da-9ef8-78a7b5aa31a9" />  
<img width="389" height="228" alt="image" src="https://github.com/user-attachments/assets/6a8e02fc-ad92-43db-b079-87ef90cefd72" />  
얘는 reserve함수가 없음.  

요소 삽입  
<img width="692" height="346" alt="image" src="https://github.com/user-attachments/assets/7ae1e207-5cf3-44fc-9f39-89756660cd2f" />  

제거  
<img width="514" height="256" alt="image" src="https://github.com/user-attachments/assets/d7703c90-c8fd-4be9-af58-ea77b2d41bdb" />  
<img width="623" height="292" alt="image" src="https://github.com/user-attachments/assets/b466fde7-5ade-40e1-a649-f722232cb100" />  

그 외 정렬, 두 리스트 합치기 등등... 메서드들 있음.  

장단점  
<img width="755" height="181" alt="image" src="https://github.com/user-attachments/assets/5beb0b71-8111-4566-a7bb-76eb057bc6fc" />  
메모리가 불연속적이라 cpu친화적이지 않음  

# 그 밖의 컨테이너들 (중요하지 않음) 
멀티셋(multi-set): 중복키 허용, 요소 수정 안됨  
멀티맵(multi-map): 중복키 허용  
덱(디큐, deque): double-dended queue의 약자, 양쪽 끝에서 요소 삽입,삭제 가능  
priority-queue: 자동 정렬되는 큐  

# STL 컨테이너의 목적  
모든 컨테이너에 적용되는 표준 인터페이스!  
std 알고리듬 (standard algorithm)은 많은 컨테이너에서 작동  
템플릿 프로그래밍 기반 (나중에 배움)  
메모리 자동 관리  

그러나, 과연 이게 좋을까?  
극단적으로 oop를 추구한 사례.  
빈번한 메모리 재할당은 메모리 단편화를 초래함: 앱 뻗을수도 있음, 디버깅 및 수정이 어렵다  
그래서, 자신만의 STL을 만들어서 쓰는 회사들이 있음  
<img width="716" height="308" alt="image" src="https://github.com/user-attachments/assets/79bb7062-6cf4-4f22-8e66-23a4445779c9" />  
