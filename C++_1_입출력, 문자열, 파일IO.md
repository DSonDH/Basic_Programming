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

코드보기: 메뉴판 출력  
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

<img width="917" height="332" alt="image" src="https://github.com/user-attachments/assets/e2e20a5e-525d-4fbf-aba6-bfeabf4e7076" />  
<img width="528" height="363" alt="image" src="https://github.com/user-attachments/assets/da4763ea-9888-4903-9f98-54248dc251bc" />  
<img width="988" height="471" alt="image" src="https://github.com/user-attachments/assets/77d10b7a-07f4-4ac7-8afe-d48b897592f7" />  

# 입력
## Input Stream
<img width="1011" height="347" alt="image" src="https://github.com/user-attachments/assets/4bf98948-b46b-4e83-b9eb-51176ab96fe2" />  
'>>' : extraction 연산자.  

```cpp
int hours;
cin >> hours;
cout << "Today I studied for " << hour << " hours." << endl;
```

부동소수점 읽기  
```cpp
float price;
cin >> price;
cout << "The price of this green tea is $" << price << "." << endl;
```

c에서 scanf()는 왜 위험했나?  
char배열에 "POPE"를 넣으면,  
char firstName[4];  
scanf("%s", firstName);  
하면 문장이 끝난걸 알려주는 '\n'를 못넣어서, 그 뒤에 이상한 메모리 공간까지 탐색해버림.  
즉 scanf()는 경계검사를 하지 않는다.  
그렇다면, cin은?  
char firstName[4];  
cin >> firstName;  
이것도 똑같은 문제가 발생함!!  
cin은 char배열의 길이를 모르고, 메모리 할당 이슈 존재함.  
(4자 이상의 단어를 입력할 경우 cin이 경계검사를 하지 않아 배열의 마지막에(firstName[3])에 \0을 포함하지 않는다.  
c보다는 조오오금 더 나은 방법이 나중에 나옴.  
``` c
char line[512];
char temp[512];
char firstName[4];

if (fgets(line, 512, stdin) != NULL)
{
    if (sscanf(line, "%s", temp) == 1 && strlen(temp) < 4)
	{
		strcpy(firstName, temp);
	}
}
```
c에선 이렇게 했는데 c++에서는 setw()로 이렇게 함
<img width="882" height="206" alt="image" src="https://github.com/user-attachments/assets/1c5f6f1b-2af2-424d-a72e-498570cd57bf" />  
<img width="840" height="406" alt="image" src="https://github.com/user-attachments/assets/50c193b4-6c2a-4ea9-b26c-f07ad43aba05" />  
<img width="581" height="285" alt="image" src="https://github.com/user-attachments/assets/e6ba5f87-adc1-4b20-82a4-a65168d66164" />  

## Stream States
<img width="896" height="320" alt="image" src="https://github.com/user-attachments/assets/d6d4ac53-d307-4218-9efd-fabe47b39e58" />  
예전 C스타일 NULL인지 검사하는게 직관적이지 않아서 c++에서 바뀐것.  
istream: input stream  
istream상태 (클래스: ios_base)  
비트 플래그: goodbit, eofbit, failbit, badbit  
메소드 버전: good(), eof(), fail(), bad()  

예시  
<img width="509" height="315" alt="image" src="https://github.com/user-attachments/assets/07c2e8d1-a416-4297-bc00-168ef9a547e7" />  
456abc: c에선 456읽고 a에서 멈춤. 멈춘지점이 eof아니라서 unset, 456실제로 읽어서 fail도 아님.  
abc: 숫자로 읽을 방법 없어서 실패, a에서 멈춰서 eof도 아님.  
eof: 숫자로 읽을 방법 없어서 실패, eof니까 eof설정 됨.  
456: 제대로 읽어서 failbit unset, !!!!! eofbit은 상황마다 다름 !!!!!  
콘솔에서는 입력하고 엔터(new line character) 넣으면 엔터는 eof아니므로, eofbit unset됨.  
그러나 입출력 redirection하면, 그 때는 eof처리 되서 eofbit set 되버림.  

## Discarding Input: clear(), ignore()
입력 버리기: 입력 상태와 관련해서, 유효하지 않은 입력 버리고 다시 받고플때.  

clear():  스트림을 좋은 상태(good state)로 돌려줌. cin.clear();  
ignore(): 아래 예제들은 파일 끝에 도달하거나 지정한 수만큼 문자를 버리면 멈춤.  
``` cpp
cin.ignore();    // 문자 1개를 버림
cin.ignore(10);  // 문자 10개를 버림
cin.ignore(10, '\n');  // 문자 10개 버리되, 뉴라인문자 버리면 바로 멈춤
cin.ignore(LLONG_MAX, '\n'); // 최대문자수 버리고, 그 전에 뉴라인 버리면 멈춤
```

질의응답  
<img width="865" height="809" alt="image" src="https://github.com/user-attachments/assets/d4b67592-3163-482c-82d1-01440d4f28e4" />  

입력 버리기: get(), getline()  
get(): 뉴라인문자를 만나기 직전까지의 모든 문자를 가져옴 (즉, 한 줄 가져옴)  
뉴라인 문자는 입력 스트림에 남아 있음  

``` cpp
// 99개 문자를 가져오거나 뉴라인문자가 나올때 까지의 문자를 가져오고,
// 가져온 문자들을 firstName에 배치함
get(firstName, 100);

// 99개 문자를 가져오거나 #문자가 나올 때 까지의 문자를 가져오고,
// 가져온 문자들을 firstName에 배치
get(fistName, 100, '#');
```

getline(): 뉴라인 문자를 만나기 직전까지 모든문자를 가져옴.  
근데 뉴라인 문자는 입력 스트림에서 버림! get은 뒤에 남기고, getline은 버리고  
두 번째 get() → 남아있던 '\n' 때문에 바로 종료 → 빈 문자열 저장  

코드보기: 정수 합 구하기  
``` cpp
#pragma once

namespace samples
{
	void AddIntegersExample();
}
==============
#include "AddIntegers.h"
#include <iostream>

using namespace std;

namespace samples
{
	void AddIntegersExample()
	{
		cout << "+------------------------------+" << endl;
		cout << "|     Add Integers Example     |" << endl;
		cout << "+------------------------------+" << endl;

		int number;
		int sum = 0;

		while (true)
		{
			cout << "Please enter an integer or EOF: ";
			cin >> number;
			if (cin.eof())
			{
				break;
			}

			if (cin.fail())
			{
				cout << "Invalid input" << endl;
				cin.clear();
				cin.ignore(LLONG_MAX, '\n');
				continue;
			}
			sum += number;
		}
		cin.clear();

		cout << "The sum is " << sum << endl;
	}
}
```

코드보기: 입력 문자열 뒤집기  
숫자던, 문자던, 문자로 읽는건 문제가 안됨. 단, eof만 fail로 뜸.  
``` cpp
#pragma once

namespace samples
{
	void ReverseInputStringExample();
}
==============
#include "ReverseInputString.h"
#include <iostream>

using namespace std;

namespace samples
{
	void ReverseInputStringExample()
	{
		cout << "+------------------------------+" << endl;
		cout << "|    Reverse String Example    |" << endl;
		cout << "+------------------------------+" << endl;

		const int LINE_SIZE = 512;
		char line[LINE_SIZE];

		cout << "Please enter a string to reverse" << endl
			<< "or EOF to quit: ";

		cin.getline(line, LINE_SIZE);
		if (cin.fail())
		{
			cin.clear();
			return;
		}

		char* p = line;
		char* q = line + strlen(line) - 1;
		while (p < q)
		{
			char temp = *p;
			*p = *q;
			*q = temp;

			++p;
			--q;
		}
		
		cout << "Reversed string: " << line << endl;
	}
}
```
