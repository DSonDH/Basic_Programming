# 출력
Hello World!  
<img width="962" height="382" alt="image" src="https://github.com/user-attachments/assets/d89064c3-5955-4e02-b7db-8c7948e93006" />  

## namespace
Jave의 패키지, C# 네임스페이스와 비슷: 함수, 클래스, 기타 등등 이름 충돌 피하려고 만듦 네임스페이스 소문자로 시작함.  

<img width="765" height="467" alt="image" src="https://github.com/user-attachments/assets/5848903e-784a-4a9b-bed1-305773d8fa79" />  
콜론콜론으로 네임스페이스 내에 어떤 함수/클래스 등을 불러올건지 정함  
using 지시문: Jave의 import나 c#의 using과 비슷. 타이핑 양 줄이는 방법일 뿐.  
<img width="877" height="285" alt="image" src="https://github.com/user-attachments/assets/8cf5fe2e-1839-43c0-91b8-19ceb5b9f6e4" />  

C에서 #ifndef #define #endif와 비슷하게 헤더 파일의 중복 포함 방지를 위한 장치로 작동하는게 C++에 #pragma once임.  

## <<연산자
insertion operator, 밀어넣기 연산자, (출력 연산자)  
c++에서는 프로그래머가 연산자의 동작을 바꿀 수 있다!  
<img width="480" height="414" alt="image" src="https://github.com/user-attachments/assets/682fc91c-6a45-4213-a76b-96bf08a4d5e9" />  

## Output Formatting
16진수 출력 - printf()  
```c
int number = 10;
printf9"%#x\n", number);
```
를 Manipulator(조정자)로 읽기 쉽게 포매팅 함  
```cpp
int number = 10;
cout << showbase << hex << number << endl;
```

showpos, noshowpos
```cpp
cout << showpos << number;   // +123
cout << noshowpos << number; // 123
```
dec/hec/oct
```cpp
cout << dec << number;       // 123, 10진수
cout << hex << number;       // 7b, 16진수
cout << oct << number;       // 173, 8진수
```
uppercase/nouppercase
```cpp
cout << uppercase << hex << number;   // 7B
cout << nouppercase << hex << number; // 7b
```
showbase/noshowbase
```cpp
cout << showbase << hex << number << endl;   // 0x7b
cout << noshowbase << hex << number << endl; // 7b
```
left/internal/right
```cpp
cout << setw(6) << left << number;       // |-123    |
cout << setw(6) << internal << number;   // |-    123|
cout << setw(6) << right << number;      // |    -123|
```
set(6)는 잠시 뒤 나옴.  

showpoint/noshowpoint
```cpp
float decimal1 = 100.0;
float decimal2 = 100.12;
cout << noshowpoint << decimal1 << " " << decimal2; // 100 100.12
cout << showpoint << decimal1 << " " << decimal2;   // 100.000 100.120
```
fixed/scientific
```cpp
float number = 123.45;
cout << fixed << number;      // 123.45
cout << scientific << number; // 1.2345E+02
```
boolalpha/noboolalpha
```cpp
bool bReady = true;
cout << boolalpha << bReady;   // true
cout << noboolalpha << bReady; // 1
```

<img width="934" height="497" alt="image" src="https://github.com/user-attachments/assets/6f0d642d-5939-40d9-abd4-7f0d5094e721" />  

질의응답  
<img width="573" height="138" alt="image" src="https://github.com/user-attachments/assets/0119fa20-dd42-49f5-a6fe-774a494a7220" />  

```cpp
#pragma once

namespace samples
{
	void PrintMenuExample();
}
================================

#include <iomanip>
#include <iostream>
#include "PrintMenu.h"

using namespace std;

namespace samples
{
	void PrintMenuExample()
	{
		cout << "+------------------------------+" << endl;
		cout << "|      Print Menu Example      |" << endl;
		cout << "+------------------------------+" << endl;

		const float coffeePrice = 1.25f;
		const float lattePrice = 4.75f;
		const float breakfastComboPrice = 12.104f;

		const size_t nameColumnLength = 20;
		const size_t priceColumnLength = 10;

		cout << left << fixed << showpoint << setprecision(2);

		cout << setfill('-') << setw(nameColumnLength + priceColumnLength) << "" << endl << setfill(' ');
		cout << setw(nameColumnLength) << "Name" 
			<< setw(priceColumnLength) << "Price" << endl;
		cout << setfill('-') << setw(nameColumnLength + priceColumnLength) << "" << endl << setfill(' ');

		cout << setw(nameColumnLength) << "Coffee" 
			<< "$" << coffeePrice << endl;
		cout <<  setw(nameColumnLength) << "Latte"
			<< "$" << lattePrice << endl;
		cout << setw(nameColumnLength) << "Breakfast Combo" 
			<< "$" << breakfastComboPrice << endl;
	}
}
```

## Input Stream

Stream States

Discarding Input: clear(), ignore()

입력 버리기: get(), getline()



# 새로운 C++ 기능
Bool 데이터형

Reference

코딩표준


# String
std::string 클래스



# 파일 I/O
파일 열기, 닫기

한 문자, 한 줄, 한 단어 읽기

잘못된 입력이 있는 경우  

파일 읽기의 Best Practice

파일 쓰기, 바이너리 파일 읽기/쓰기, 파일 안에서의 탐색(seek)

d

