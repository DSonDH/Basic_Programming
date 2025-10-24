# 새로운 C++ 기능
초기 c++기능에서 살아남은 소수의 기능만 알면 됨.  
bool, reference, oop 등등이 있음  

## Bool 데이터형
<img width="825" height="376" alt="image" src="https://github.com/user-attachments/assets/5c74e3d7-fe44-46a5-9b62-f19f33987bca" />  
0은 false, 나머지는 true  

## Reference
c#에는 있고 java에는 없는  
포인터를 사용하는 좀 더 안전한 방법.  
Java만큼 제한적이지는 않음.  
Call by value, call by reference, pointer  

32비트 컴파일러라 가정  
Call by reference (C)  
int* arg1: 주소를 받아온다. &num1은 주소를 반환해준다.  

Java는? dtype별로 다름. primitive type이 아닌 자료는 reference를 받으므로 원본 바뀜.  
C, C++의 경우는... call by valu, reference 둘 다 가능, 함수 시그내쳐로 볼 수 있음  
값에 의한 호출  
<img width="942" height="522" alt="image" src="https://github.com/user-attachments/assets/7267c85b-c461-436c-90fa-d72086c625ec" />  
<img width="927" height="513" alt="image" src="https://github.com/user-attachments/assets/196481ac-5a05-4fb9-bb1d-d6a504e23d44" />  

참조에 의한 호출  
<img width="721" height="487" alt="image" src="https://github.com/user-attachments/assets/554ddf83-36b4-4581-b34a-ab31ad5033c8" />  
<img width="718" height="480" alt="image" src="https://github.com/user-attachments/assets/ae6ecc8d-39d9-4337-8751-7535a714531d" />  

그래서, C++참조란, 
별칭이다.  
``` cpp
int number = 100;  
int& reference = number;  
int& reference = NULL; // error: NULL이 될 수 없음.  

//초기화 중에 반드시 선언되어야 함
int& reference;  // error: 참조하는 대상을 바꿀 수 없다

int n1 = 100;
int n2 = 200;
int& reference = n1;
reference = n2;  // 모든 값이 200이 됨...!
```
<img width="1009" height="494" alt="image" src="https://github.com/user-attachments/assets/1ff21841-b813-445f-98d8-a69e968712ca" />  

왼쪽 포인터는 NULL에 의한 오류가 생길 수 있지만, 참조는 NULL체크 안해도 됨.  
포인터에서는 포인터 연산으로 이상한 메모리 접근이 되는데,  
참조는 새로운 메모리 접근이 안되서 좋다.  
(오른쪽 참조 방법에서는 NULL검사할 방법이 전혀 없다고 함...)  

즉, 포인터랑 참조의 차이는  
포인터랑 달리 반드시 선언과 동시에 초기화, 이후 다른 변수로 바꿀 수 없음  
NULL 불가능 (항상 실제 변수 참조)  
포인터는 주소값만큼 (보통 8바이트) 메모리 차지하지만, 참조는 별도 메모리 사용 X (컴파일러가 원본 변수로 치환)  
포인터는 주소연산 가능하지만 (주소 이동 등) 참조는 연산 불가  
함수 전달 시 포인터는 원본의 주소를 넘겨주지만, 참조는 별칭으로 넘겨져서 원본 직접 접근  

```cpp
// 포인터 버전
void Refer(int* p) {
    if (p != nullptr) {
        *p = 3;  // 포인터가 가리키는 대상 수정
    }
}

int main() {
    int x = 10;
    Refer(&x);   // 주소를 넘겨야 함
    // x == 3
}

// 참조 버전
void Refer(int& p) {
    p = 100;   // 참조는 자동으로 원본에 연결
}

int main() {
    int x = 10;
    Refer(x);    // 그냥 변수 이름만 넘기면 됨
    // x == 100
}

// call by value
void Refer(int p) {
    p = 100;
}

int main() {
    int x = 10;
    Refer(x);    // 그냥 변수 이름만 넘기면 됨
    // x == 10
}
```

역참조(dereference): 포인터변수가 가리키는 메모리 주소에 접근하여, 그 안에 실제 값을 사용하는 것.  
``` cpp
int x = 10;
int* p = &x;     // p는 x의 주소를 저장
int y = *p;      // p를 역참조 → x의 값 10을 가져옴
*p = 20;         // p를 역참조 → x의 값을 20으로 변경
```
**nullptr(또는 초기화되지 않은 포인터)** 를 역참조하면 존재하지 않는 메모리에 접근 → 런타임 오류(segmentation fault).  
그래서 역참조하기 전에 포인터가 유효한지 반드시 확인하는 습관이 필요하다.  

컴퓨터는 참조가 뭔지 알까?  
모름! 포인터와 참조는 같은 어셈블리 명령어를 생성함.  
참조는 오직 인간을 위한 것임.  
컴파일러는 참조를 포인터로 바꿔줌. 기계가 이해할 수 있도록.  
C에는 없지만, C++에 있는 기능은 다른 프로그래머가 구현한것!  

코드보기: 참조를 사용한 swap  

## 코딩표준
<img width="829" height="380" alt="image" src="https://github.com/user-attachments/assets/a8e9d759-1b9f-43cf-8981-c1c007fdbbc2" />  

c#에서는 'out'키워드를 사용해서 명시할 수 있음.  

# String
std::string 클래스
기존에는  
char line{256];  
cin.getline(line, 256);  
으로 했고, 아무것도 읽지 못하거나 256길이 이상이면 작동하지 않았음.  
대안으로:  
std::string 클래스를 사용하면 된다.  
즉, string형 내부에 총 용량과, 현재 몇 자가 저장되어있는지 기록한다.  
``` cpp
#include <string>
std::string firstName;
str::cin >> firstName;
```
<img width="915" height="329" alt="image" src="https://github.com/user-attachments/assets/e875014a-0d9b-4488-b939-475731ece29c" />  

string array로 사용하던 것들을, 좀 더 쉽게 사용할 수 있게됨.  
안전해지기도 함!  

<img width="995" height="322" alt="image" src="https://github.com/user-attachments/assets/7d12b71c-0d4a-441d-b734-dd02678c2ac8" />  
<img width="873" height="405" alt="image" src="https://github.com/user-attachments/assets/9638190a-2ebe-473a-95c2-97b19c234086" />  

size()는 \n를 제외한 길이를 반환해줌.  
<img width="942" height="528" alt="image" src="https://github.com/user-attachments/assets/4c647960-7b3e-4630-8a95-a18dcdf6051d" />  
c는 옛날방식이고 c++는 c와 호환되도록 되어있어서, char*를 고려한 함수를 만든것.  

string속의 한 문자에 접근하기: C와 같음  
``` c++
string firstName = "POKE";
char letter = firstName[1];

firstName[2] = 'P';
// 나중에 보긴 할건데, firstName[2] 이게 함수라고 함.
// 함수 반환값을 참조형이어서 바로 변경이 되는 것임
```

at(): n번째 인덱스의 문자를 참조로 반환  

<img width="907" height="391" alt="image" src="https://github.com/user-attachments/assets/b04006f3-1404-424a-b386-98fc84a5cc41" />  

<sstream>: string stream  
<img width="621" height="325" alt="image" src="https://github.com/user-attachments/assets/0ddba57e-8c36-4ec7-a83c-64c83688d67c" />  

Q: C헤더를 써도 되나?  
A: 네. 현업 C++애플리케이션에서는 여전히 성능상의 이유로 많은 C함수들이 사용되고 있음.  
"이건 C++스럽지 않아서 틀림"이라 하는 사람은 그냥 무시하기!  
``` cpp
C: <string.h>, <stdio.h>, <ctype.h>  
cpp: <cstring>, <cstdio>, <cctype>  
```  
std::string은 문자 배열 길이 고민을 할 필요가 없지만,... 메모리 썻다 지웠다 하면서 작업이 이뤄짐.  
- heap 메모리 할당은 느림
- memory fragmentation 문제도 있음
- 내부 버퍼의 증가는 멀티 쓰레드 환경에서 안전하지 않을수도 있음
- 여전치 C++를 쓰는 업계가 어디인지 생각해보면 ..
- 그래서 여전히 sprintf와 char[]를 많이 쓰고 있다.
(memory fragmentation: 메모리 전체는 충분하지만, 연속된 블록이 부족하여 요청한 크기의 메모리를 할당할 수 없는 상태)  

참고  
const pointer읽는법: 오른쪽에서 왼쪽으로  
const char* : pointer to const char : pointer는 바꿀 수 있고 (주소변경 가능), character를 바꿀 수 없다 (읽기전용).  
char* const : pointer가 const. const to char pointer. 주소변경 불가능, character는 바꿀 수 있다 (원본수정 가능).  

코드보기: 문자열 미러링  
```c++
#pragma once

namespace samples
{
	void MirrorStringExample();
}
==========
#include <iostream>
#include <string>
#include "MirrorString.h"

using namespace std;

namespace samples
{
	void MirrorStringExample()
	{
		cout << "+------------------------------+" << endl;
		cout << "|    Mirror String Example     |" << endl;
		cout << "+------------------------------+" << endl;

		string line = "Hello World!";

		cout << "string to mirror: " << line << endl;

		for (int i = (int)line.size() - 1; i >= 0; --i)
		{
			line += line[i];
		}
		cout << "mirrored string" << line << endl;
	}
}
```

# 파일 I/O
## 파일 열기, 닫기  
ifstream: 파일 입력  
ofstream: 파일 출력  
fstream: 파일 입출력  
파일스트림에 <<, >>, manipulator 등도 쓸 수 있음  
<img width="1013" height="435" alt="image" src="https://github.com/user-attachments/assets/7a024bc3-3526-4c08-8fce-cfbe86f5ba76" />  

### open()  
각 스트림마다 open() 메서드가 있음  
``` cpp
fin.open("HelloWorld.txt", ios_base::in | ios_base::binary);
```
모드 플래그(mode flags)
  - ios_base 네임스페이스
  - in, out, ate(at the end라는 뜻), app(append라는 뜻), trunc, binary가 있음  

open 두번째 인자가 비트플래그임.  
모드 플래그 별 유효하지 않은 조합들이 있다고 함.  

파일 열기 모드의 예  
<img width="661" height="315" alt="image" src="https://github.com/user-attachments/assets/5284a7a4-3ced-4e1e-8995-09675776d29b" />  

### 파일 닫기  
<img width="913" height="241" alt="image" src="https://github.com/user-attachments/assets/70b549e0-1c04-4ec9-b638-45d15620dc5f" />  

fin이 object.  

### stream 상태 확인하기  
<img width="852" height="302" alt="image" src="https://github.com/user-attachments/assets/192642e2-8670-4e9e-9d0b-ba5e49bfb4d7" />  

C에서는 상태 부적절하면 NULL들어왔었음.  

close(): 각 스트림마다 close() 메서드가 있음. fin.close(); 처럼  
is_open(): 파일이 열려있는지 확인. if (fs.is_open()) {...}  


## 한 문자, 한 줄, 한 단어 읽기
<img width="859" height="429" alt="image" src="https://github.com/user-attachments/assets/15543fd7-ac80-45be-8748-02f14368e4de" />  

fin.fail()인 경우는 eof만난 경우. 나머지는 숫자던 문자던 읽을 수 있음.  

get(), getline(), >> : 어떤 스트림(ex: cin, istringstream)을 넣어도 동일하게 동작함 (추상화!)  
``` cpp
fin.get(character);

fin.getline(firstName, 20);  // 파일에서 문자 20개를 읽음
getline(fin, line);          // 파일에서 한 줄을 읽음
fin >> word;                 // 파일에서 한 단어를 읽음
```  

파일에서 한 줄씩 읽기 (완벽하지 않은 코드)  
``` cpp
ifstream fin:
fin.open("Hello World.txt);

string line;
while (!fin.eof())
{
    getline(fin, line);
    cout << line << endl;
}

fin.close();
```
위 코드의 happy path 시나리오:  
<img width="999" height="555" alt="image" src="https://github.com/user-attachments/assets/a6151f7e-e166-4581-997d-0c9e5fe95e1f" />  
<img width="987" height="542" alt="image" src="https://github.com/user-attachments/assets/72b775c6-eb1e-4bd3-9e8c-3403cbbe3338" />  
<img width="993" height="538" alt="image" src="https://github.com/user-attachments/assets/2f34a775-694e-4896-878c-c5f9e1217e10" />  
<img width="992" height="534" alt="image" src="https://github.com/user-attachments/assets/3d99c9b1-e886-49a3-8970-e0a1c9fad793" />  

빈 파일 읽기:  
<img width="808" height="433" alt="image" src="https://github.com/user-attachments/assets/365e5cb2-cb10-4913-ae72-466ffc60aaca" />  
<img width="826" height="435" alt="image" src="https://github.com/user-attachments/assets/e4ab2247-a687-48c1-96b6-56d2708f9312" />  
아무 내용도 없는데 빈 줄이 나옴...  

파일에서 한 단어씩 읽기 (완벽하지 않은 코드)  
``` C++
ifstream fin;
fin.open("Hello World.txt);

string name;
float balance;
while (!fin.eof())
{
    fin >> name >> balance;  // space 하나까지 읽음
    cout << name << ": $" << balance << endl;
}

fin.close();
```
<img width="1003" height="533" alt="image" src="https://github.com/user-attachments/assets/045b75d0-b90d-41d9-9623-bdb5ce39e988" />  
<img width="1008" height="527" alt="image" src="https://github.com/user-attachments/assets/a3e4c443-b95a-405b-bb6a-67e25201ff4d" />  
<img width="1007" height="528" alt="image" src="https://github.com/user-attachments/assets/5aa76117-386f-499d-93d3-ccb44eb93693" />  
<img width="728" height="501" alt="image" src="https://github.com/user-attachments/assets/6be6394c-66b9-4ec8-9770-05a8c6856a17" />  

숫자들만 있는 경우  
<img width="656" height="390" alt="image" src="https://github.com/user-attachments/assets/4e9e60c2-fd95-48bd-8215-d4cb09c13dac" />  
<img width="859" height="388" alt="image" src="https://github.com/user-attachments/assets/9cb4e229-8836-4f00-8bda-1665dd298efa" />  
<img width="997" height="428" alt="image" src="https://github.com/user-attachments/assets/4560f2e1-3feb-4c37-b641-9b07a6863e69" />  
<img width="1005" height="440" alt="image" src="https://github.com/user-attachments/assets/c33746d9-a2d0-4ad5-b549-916584c21f42" />  
<img width="680" height="383" alt="image" src="https://github.com/user-attachments/assets/175e1a28-9cbc-43f1-b6db-a71d23624b09" />  

### 잘못된 입력이 있는 경우  
eof앞에 \n 있는 경우  
<img width="651" height="409" alt="image" src="https://github.com/user-attachments/assets/216a0c29-0b48-40c0-aa4a-f2a6655eddf3" />  
<img width="808" height="440" alt="image" src="https://github.com/user-attachments/assets/4dcc4bfc-77eb-4c5e-a2e0-6560a06efd52" />  
eofbit이 false로 유지되서 다시 읽어버림!  
<img width="826" height="443" alt="image" src="https://github.com/user-attachments/assets/3958c9b0-e35c-4b60-b020-6f492e5776bf" />  
<img width="802" height="426" alt="image" src="https://github.com/user-attachments/assets/3b110189-4095-440a-834b-3616cbd8f253" />  
300 들어간게 다시 출력되고, 끝남.  

잘못된 입력과 숫자들  
<img width="796" height="436" alt="image" src="https://github.com/user-attachments/assets/49f70574-fb47-4bf2-996d-30a793b075b6" />  
<img width="852" height="441" alt="image" src="https://github.com/user-attachments/assets/6655aaa3-ad8e-48c1-96f0-6b5e8f64f018" />  
<img width="870" height="441" alt="image" src="https://github.com/user-attachments/assets/c60a78a7-a13a-4274-8092-2693bd8fda46" />  

!!! 고치는 법 !!!  
<img width="1001" height="440" alt="image" src="https://github.com/user-attachments/assets/fd5f1978-4fb1-4d3e-8598-5362fa30755b" />  
이는 사례4(잘못된 입력과 숫자들)의 문제는 해결할 수 없음.  

<img width="1001" height="516" alt="image" src="https://github.com/user-attachments/assets/ab7d8116-be3c-4dd1-aa75-ba1909fc8fb3" />  
근데, 탭(\t), 스페이드 둘 다 있으면 또 안됨.  
<img width="1008" height="531" alt="image" src="https://github.com/user-attachments/assets/7c7a248a-712b-412c-afba-ce0226221c8d" />  

숫자만 읽을때 되는 코드  
<img width="848" height="507" alt="image" src="https://github.com/user-attachments/assets/4f79e178-41dd-4dda-a783-c0206d5fe482" />  
fin >> trash;는 일단 문제 있는걸 받아와서, 아무것도 안하고 바로 넘어가는 거임  

또 다른 문제...  
<img width="954" height="518" alt="image" src="https://github.com/user-attachments/assets/fee4a58d-9246-40c4-b24f-4b4b463921ff" />  
failbit일때 cin >> trash;가 작동 안해버린다!!  
<img width="813" height="353" alt="image" src="https://github.com/user-attachments/assets/8a38823c-af91-470f-b77b-2a2a42524ed7" />  
그러고는 아래 cin.clear();해서 failbit이 다시 false로 돌아옴.  
그러면 또 읽어려하고, 무한루프 걸림.  
<img width="962" height="400" alt="image" src="https://github.com/user-attachments/assets/9c089a1c-08bc-4d5a-b337-0d02f45884af" />  

### 파일 읽기의 Best Practice
eof처리는 까다롭다. 입출력 연산이 스트림 상태 비트를 변경한다는 사실을 기억하자!  
eof 잘못 처리 하면 무한 반복 초래. clear() 쓸 때는 두 번 생각하자  
이런 입력 처리 문제는 업계에서 매우 흔한 문제임.  
자신만의 reader를 만드는 경우가 흔함.  
결국, 상태n개면, $2^n$개 테스트 많이 해보는게 중요함.  

**훌륭한 테스트 케이스**  
<img width="747" height="529" alt="image" src="https://github.com/user-attachments/assets/2196ec2e-236b-422f-87f5-fdb66cc2462e" />  

## 파일 쓰기, 바이너리 파일 읽기/쓰기, 파일 안에서의 탐색(seek)
<img width="871" height="360" alt="image" src="https://github.com/user-attachments/assets/77401a5c-5d51-4274-8400-30fa7bca7c97" />  
endl: stream flush하고 '\n'은 stream flush안하고 차이 있음.  

put(): 문자를 써 넣음 fout.put(character);  
<<: 밀어넣기 (ex: fout << line << endl);)  

바이너리 파일 읽기  
<img width="941" height="330" alt="image" src="https://github.com/user-attachments/assets/a7149acb-a9fd-4eac-af59-b03316628bbc" />  

ifstream::read()  
read(char*, streamsize)  
fin.read(firstName, 20) : 파일로부터 문자 20자를 읽어 firstName에 저장  

바이너리 파일 쓰기  
<img width="1024" height="424" alt="image" src="https://github.com/user-attachments/assets/ae322a63-3168-47c9-99fc-d656d8b50660" />  
ofstream::write()  
write(const char*, streamsize)  
fout.write(firstName, 20: firstName에 저장 되어있는 문자 20자를 파일에 씀  

파일 안에서의 탐색(seek)  
원하는 위치에서 file pointer 설정해서 읽기 시작하기  
<img width="1034" height="419" alt="image" src="https://github.com/user-attachments/assets/4f466a2e-536d-4fb0-86b4-1cc620959321" />  
seekp :seek put  

seek 유형  
절대적: 특정위치로 가는데, tellp() (쓰기 포인터 위치)나 tellg() (읽기 포인터 위치)를  
사용해서 기억해 놨던 위치로 돌아갈 때 사용  

상대적: 파일의 끝에서 ?바이트 앞의 위치로 이동  
ios_base::beg // 시작부터 ?바이트 뒤  
ios_base::cur // 현재부터 ?바이트 뒤  
ios_base::end // 끝부터 ? 바이트 앞  

ios::pos_type pos = fout.tellp();  
seekp() 절대적, 상대적  
fout.seekp(0); // 처음 위치로 이동  
fout.seekp(20, ios_base::cur); // 현재 위치에서 20바이트 뒤로 이동  

fout.seekg(0); // 읽기포인터 처음 위치로 이동  
fout.seekg(-10, ios_base::end); // 읽기포인터 파일 끝에서 10바이트 앞으로 이동  

기타 정보  
<img width="637" height="309" alt="image" src="https://github.com/user-attachments/assets/15e8cb7d-6f91-414a-8d06-e6174c513e17" />  
std::ws를 생략해서 ws라고 쓴거임.  

코드보기: 파일 입출력  
```cpp
#pragma once

#include <iostream>
#include <string>

struct Record
{
	std::string FirstName;
	std::string LastName;
	std::string StudentID;
	std::string Score;
};

namespace samples
{
	Record ReadRecord(std::istream& stream, bool bPrompt);

	void WriteFileRecord(std::fstream& outputStream, const Record& record);

	void DisplayRecords(std::fstream& fileStream);

	void ManageRecordsExample();
}
========
#include <fstream>
#include <iomanip>
#include "PrintRecords.h"

using namespace std;

namespace samples
{
	Record ReadRecord(istream& stream, bool bPrompt)
	{
		Record record;

		if (bPrompt)
		{
			cout << "First name: ";
		}
		stream >> record.FirstName;

		if (bPrompt)
		{
			cout << "Last name: ";
		}
		stream >> record.LastName;

		if (bPrompt)
		{
			cout << "Student ID: ";
		}
		stream >> record.StudentID;

		if (bPrompt)
		{
			cout << "Score:  ";
		}
		stream >> record.Score;

		return record;
	}

	void DisplayRecords(fstream& fileStream)
	{
		fileStream.seekg(0);

		string line;
		while (true)
		{
			getline(fileStream, line);

			if (fileStream.eof())
			{
				fileStream.clear();
				break;
			}
			cout << line << endl;
		}
	}

	void WriteFileRecord(fstream& outputStream, const Record& record)
	{
		outputStream.seekp(0, ios_base::end);

		outputStream << record.FirstName << " "
			<< record.LastName << " "
			<< record.StudentID << " "
			<< record.Score << endl;

		outputStream.flush();
	}

	void ManageRecordsExample()
	{
		cout << "+------------------------------+" << endl;
		cout << "|    Manage Records Example    |" << endl;
		cout << "+------------------------------+" << endl;

		fstream fileStream;
		fileStream.open("studentRecords.dat", ios_base::in | ios_base::out);

		bool bExit = false;
		while (!bExit)
		{
			char command = ' ';

			cout << "a: add" << endl
				<< "d: display" << endl
				<< "x: exit" << endl;

			cin >> command;
			cin.ignore(LLONG_MAX, '\n');

			switch (command)
			{
			case 'a':
			{
				Record record = ReadRecord(cin, true);
				WriteFileRecord(fileStream, record);
				break;
			}
			case 'd':
			{
				DisplayRecords(fileStream);
				break;
			}
			case 'x':
			{
				bExit = true;
				break;
			}
			default:
			{
				cout << "invalid input" << endl;
				break;
			}
			}
		}

		fileStream.close();
	}
}
```
