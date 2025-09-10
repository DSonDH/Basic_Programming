템플릿 프로그래밍: STL을 돌게하는 원동력  
정말 필요한 곳에만 쓰자고 자제하고 있음  

# 함수 템플릿
템플릿이란? Java, C#에서의 generic메서드/클래스와 비슷.  
STL컨테이너도 템플릿. **덕분에 코드를 자료형마다 중복작성 안해도 됨**  

두 정수 더하는 예시:  
<img width="820" height="276" alt="image" src="https://github.com/user-attachments/assets/9f96589d-9369-4ba9-9836-edc94acb5e96" />  
컴파일 도중에 이뤄짐.  
<img width="741" height="334" alt="image" src="https://github.com/user-attachments/assets/81481389-3080-4b67-b8de-db9a3a3cea55" />  

함수 템플릿 호출할 때 템플릿 매개변수 생략 가능.  
Add<int>(3, 10);을 Add(3, 10);으로  

typename vs class 차이: 사실상 없음. 그냥 typename을 사용하자.  

템플릿은 어찌 작동할까?  
<img width="798" height="388" alt="image" src="https://github.com/user-attachments/assets/74270d6c-c9d2-4db1-946f-c7eb3912a393" />  
<img width="791" height="381" alt="image" src="https://github.com/user-attachments/assets/a1b1add8-1824-4802-a352-ae04104c4a7b" />  
컴파일 하는 도중에 빨간박스 코드 만들어줌. 파란박스 코드도 만들어줌.  

템플릿에 넣는 자료형 가짓수에 비례해서 exe파일 크기가 증가함  
컴파일 타임에 어느정도 다형성을 부여할 수 있음 (이와 관련 논란은 다음에 보자)  

# 클래스 템플릿
<img width="785" height="358" alt="image" src="https://github.com/user-attachments/assets/f3466b1b-0c58-4786-bfda-ebd1bf7fcea7" />  

(꼼수: enum { MAX = 3 }; 으로 정적으로 초기화 가능)  
(public에 enum { MAX = 3 }; 넣으면 MyIntArray::MAX해서 이넘값 불러올 수 있음)  

MyArray로 일반화해보자!  
<img width="864" height="359" alt="image" src="https://github.com/user-attachments/assets/61135d3c-c039-45cf-8114-563b777f8a8d" />  

근데, 이상한 에러들이 많이 생김.  
컴파일러가 Main.cpp 컴파일할 때, MyArray.cpp못찾음.  
MyArray.h로는 오직 MyArray클래스 선언만 볼 수 있음.  
따라서 컴파일러가 MyArray<int> 못만듦.  
전에 inline함수에서 헤더파일에 모든 구현 옮기는 식으로 해결했듯이 해야함.  
따라서 템플릿 프로그래밍에선 헤더에 구현을 옮기는게 일반적이다.  
<img width="275" height="377" alt="image" src="https://github.com/user-attachments/assets/f738d82f-ffbb-4c4b-8be9-0c10ec3f1227" />  

개체를 선언할때는 템플릿 매개변수를 명시해야함: MyArray<int> scores;  
함수 템플릿에는 생략해도 됬는데, 클래스 템플릿은 안됨.  
컴파일러가 알 수 있는 방법이 없음. 함수 템플릿은 컴파일러가 추측하는데, 여긴 방법이 없음  

코드보기: 템플릿 배열  
``` C++
#pragma once

namespace samples
{
	template<typename T>
	class MyArray
	{
	public:
		MyArray();

		bool Add(const T& data);  // T가 개체일 수 있어서 const T& 가능!
		size_t GetSize() const;

	private:
		enum { MAX = 3 };

		size_t mSize;
		T mArray[MAX];
	};

	template<typename T>
	MyArray<T>::MyArray()
		: mSize(0)
	{
	}

	template<typename T>
	size_t MyArray<T>::GetSize() const
	{
		return mSize;
	}

	template<typename T>
	bool MyArray<T>::Add(const T& data)
	{
		if (mSize >= MAX)
		{
			return false;
		}

		mArray[mSize++] = data;

		return true;
	}
}
======
#include <iostream>
#include "IntVector.h"
#include "MyArray.h"
#include "MyArrayExample.h"

using namespace std;

namespace samples
{
	void MyArrayExample()
	{
		MyArray<int> scores;
		scores.Add(10);
		scores.Add(50);
		
		cout << "scores - Size: " << scores.GetSize() << endl;
		
		MyArray<IntVector> intVectors;
		intVectors.Add(IntVector(1, 1));
		intVectors.Add(IntVector(5, 3));

		cout << "intVectors - Size: " << intVectors.GetSize() << endl;

		MyArray<IntVector*> intVectors2;

		IntVector* intVector = new IntVector(3, 2);
		intVectors2.Add(intVector);
		
		cout << "intVectors2  - Size: " << intVectors2.GetSize() << endl;

		delete intVector;
	}
}
```

## 클래스 템플릿 트릭  
<img width="738" height="296" alt="image" src="https://github.com/user-attachments/assets/29adea18-75d0-4b57-b417-6b796cd754c6" />  
벡터 만들 때 처음부터 최대 크기 강요해서, 동적으로 커지지 않게 하는 방법.  

코드보기: FixedVector (동영상 강의 다시 보기)  
``` cpp
#pragma once

namespace samples
{
	template<typename T, size_t N>
	class FixedVector
	{
	public:
		FixedVector();

		bool Add(const T& data);
		size_t GetSize() const;
		size_t GetCapacity() const;

	private:
		size_t mSize;
		T mArray[N];
	};

	template<typename T, size_t N>
	FixedVector<T, N>::FixedVector()
		: mSize(0)
	{
	}

	template<typename T, size_t N>
	size_t FixedVector<T, N>::GetSize() const
	{
		return mSize;
	}

	template<typename T, size_t N>
	size_t FixedVector<T, N>::GetCapacity() const
	{
		return N;
	}

	template<typename T, size_t N>
	bool FixedVector<T, N>::Add(const T& data)
	{
		if (mSize >= N)
		{
			return false;
		}

		mArray[mSize++] = data;

		return true;
	}
}
=====
#include <iostream>
#include "FixedVector.h"
#include "FixedVectorExample.h"
#include "IntVector.h"

using namespace std;

namespace samples
{
	void FixedVectorExample()
	{
		FixedVector<int, 3> scores;
		scores.Add(10);
		scores.Add(50);
		
		cout << "scores - <Size, Capacity>: " << "<" << scores.GetSize()
			<< ", " << scores.GetCapacity() << ">" << endl;

		FixedVector<IntVector, 5> intVectors;
		intVectors.Add(IntVector(2, 5));
		intVectors.Add(IntVector(4, 30));
		intVectors.Add(IntVector(22, 3));

		cout << "intVectors - <Size, Capacity>: " << "<" << intVectors.GetSize()
			<< ", " << intVectors.GetCapacity() << ">" << endl;

		FixedVector<IntVector*, 4> intVectors2;

		IntVector* intVector = new IntVector(3, 2);
		intVectors2.Add(intVector);
		
		cout << "intVectors2 - <Size, Capacity>: " << "<" << intVectors2.GetSize()
			<< ", " << intVectors2.GetCapacity() << ">" << endl;

		delete intVector;
	}
}
```

# 두 개의 템플릿 매개변수
MyPair 예시  
<img width="823" height="408" alt="image" src="https://github.com/user-attachments/assets/e0d30864-f354-4942-81cb-89036a79c2b0" />  

템플릿 매개변수를 MyPair<std::string, int> 이런식으로 하나 더 만들 수 있나?  
<img width="777" height="405" alt="image" src="https://github.com/user-attachments/assets/402df7af-7966-4b74-8be4-72f0d85fa11d" />  
처음꺼 T 두번째꺼 U  
<img width="784" height="224" alt="image" src="https://github.com/user-attachments/assets/24a6a97d-2e3b-4b32-941f-2efdbfdf9bf3" />  

코드보기: Math (동영상 강의 한번 더 보기)  
질의응답  
<img width="715" height="271" alt="image" src="https://github.com/user-attachments/assets/0010f1ea-b300-4b74-88dc-3dbec4af8a79" />  

# 템플릿 특수화(Specialization) (안중요함)
일반화 하다보니, 한두개만 좀 튀는 애들이 있음. 얘네를 위한 개념임.  
특정 템플릿 매개변수를 받도록 템플릿 코드를 커스터마이즈할 수 있다.  
특수화 쓸 일이 거의 없긴함.  

예1 bool  
<img width="627" height="200" alt="image" src="https://github.com/user-attachments/assets/d1185869-0b1b-4f38-a308-ab2303d4ba56" />  
T가 아니라 bool로 되어있음. bool로 특수화된건데 왜 bool만?  
메모리가 쪼들리는 플랫폼이라면 가치가 좀 있음.  
예2 Power(): 우리가 알던대로 구현하면 좀 이상한데, 특수한 방법이 필요함  

템플릿 특수화 2가지  
<img width="707" height="339" alt="image" src="https://github.com/user-attachments/assets/b89a2365-72af-4be0-b411-7523a03cd559" />  
클래스 템플릿 특수화  
<img width="616" height="389" alt="image" src="https://github.com/user-attachments/assets/129f1d7b-89d5-407b-a472-7702e9a6b779" />  

# 장단점, BP  
<img width="703" height="333" alt="image" src="https://github.com/user-attachments/assets/984a222d-8593-47c4-b2df-38089af0ac2b" />  
<img width="715" height="339" alt="image" src="https://github.com/user-attachments/assets/f7b44d6d-ebbb-4f42-b806-ed9aeab567d9" />  
<img width="813" height="359" alt="image" src="https://github.com/user-attachments/assets/158049ee-b2ca-4750-a84a-045daba09caa" />  

Best Practice  
컨테이너의 경우 매우 적함. 아주 다양한 형들을 저장할 수 있음  
그런 이유로 Java와 C#제네릭이 주로 컨테이너에 쓰이는 것  
컨테이너가 아니면, 서넛 이상의 자료형을 다룬다면 템플릿 쓰고, 그 이하면 그냥 각각 만들자!  

# STL 알고리듬 (안중요함) 
STL 알고리듬이란? 요소 범위에서 쓸 수 있는 함수들 [처음, 마지막)  
배열 또는 몇몇 STL컨테이너에 쓸 수 있음  
반복자를 통해 컨테이너에 접근  
컨테이너의 크기를 변경하지 않음(따라서 추가 메모리 할당도 없음)  

STL알고리듬 유형  
<img width="667" height="292" alt="image" src="https://github.com/user-attachments/assets/8fbb5ed3-8207-4151-8c7c-9d9aa808da3b" />  

두 벡터가 있을 때 복사하기  
<img width="498" height="382" alt="image" src="https://github.com/user-attachments/assets/41e3dd6d-904b-40cc-8b77-f7d0af2333e6" />  
copy()  
<img width="647" height="310" alt="image" src="https://github.com/user-attachments/assets/6204bdfc-3a6e-4cff-89e0-6b16c476b88f" />  
copy() 구현  
<img width="496" height="231" alt="image" src="https://github.com/user-attachments/assets/b79df9ee-936c-4dc8-81f8-d649662fc233" />  
(for loop ; 다음 마지막에 _Dest, _First 둘 다 넣어서 둘 다 증가시킴)  
코드보기: find() 알고리듬  

STL 알고리듬 목록은 많은데, 필요하면 쓰기.  

<img width="617" height="358" alt="image" src="https://github.com/user-attachments/assets/cbd0884a-446c-4012-8017-ee4561a7ce79" />

