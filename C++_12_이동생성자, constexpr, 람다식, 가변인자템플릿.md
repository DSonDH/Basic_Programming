# 이동 생성자 및 이동 대입 연산자
unique_ptr에서 나만 쓰는주소, 남한테 양도하는 과정에서 나온 것.  

## 값(value)의 분류  
lvalue: 단일 식을 넘어 지속되는 개체, 주소가 있음, 이름이 있는 변수, const 변수, 클래스 멤버, 문자열 리터럴, ...  
지금까지 봐온 클래스멤버, 문자열 리터럴, 비트필드, 등등  

rvalue: lvalue가 아닌 개체. 단일 식을 넘어 지속되지 않는 일시적인 값, 주소가 없는 개체, 리터럴 (문자열 리터럴 제외) 등등   
주소가 없는 개체, enum, lambda등  

``` cpp
int number = 10; // 10은 rvalue
10 = number;  // compile error. 10은 rvalue이므로
(number + 1) = 20 ;  // compile number + 1 결과는 rvalue이므로

int anotherNumber = 20;  // anotherNumber lvalue
int result = number + anotherNumber;  // (number + anotherNumber) 즉, 더하고 나온 결과는 rvalue

&number = 20; // compile error. rvalue이므로
```

과거 c++ 11이전에 문제가 있었는데,  
<img width="996" height="436" alt="image" src="https://github.com/user-attachments/assets/4a7222d6-68f9-48eb-8bc5-f2a3a8dd05f0" />  
<img width="993" height="437" alt="image" src="https://github.com/user-attachments/assets/e9b5c26b-d955-4037-9b8a-04ce68f3273f" />  
<img width="998" height="457" alt="image" src="https://github.com/user-attachments/assets/5d25b94b-566a-4707-a5dc-08eecbf4934b" />  
<img width="996" height="444" alt="image" src="https://github.com/user-attachments/assets/6a24abf1-f6f0-468d-b533-0c8028965ae1" />  
<img width="997" height="441" alt="image" src="https://github.com/user-attachments/assets/15c8d0b6-ed7b-4250-8fcf-c254c15c689e" />  
<img width="996" height="437" alt="image" src="https://github.com/user-attachments/assets/da27750e-475d-4b93-9451-620126ca68da" />  
결국에는 저 세 칸만 남는데, 그 과정은 복잡하더라...  
이 복사를 어떻게 막을까? rvalue참조와 이동문법으로 해결할 수 있다!  

rvalue 참조 (&&)  
C++11이후에 새로 나온 연산자, 기능상 &연산자와 비슷.  
&연산자는 lvalue참조에, &&연산자는 rvalue참조에 사용  
``` cpp
float CalculateAverage()
{
  float average;
  // ...
  return average;
}

int main()
{
  int number = 10;
  int&& rNumber = number;  // Error! number는 lvalue
  int&& rNumber1 = 10;     // OK, 10은 rvalue
  float&& rAverage = CalculateAverage();  // OK, CalculateAverage()는 rvalue
}
```

std::move()  
rvalue참조를 반환, lvalue를 rvalue로 변환  
이동생성자랑 쓰는 패턴만 알아도 됨.  

이동생성자  
<img width="919" height="431" alt="image" src="https://github.com/user-attachments/assets/0c9e57ab-031a-4be5-9cb7-eb600cbdf4ff" />  
MyString.cpp에서 복사는 없음.  
<img width="947" height="447" alt="image" src="https://github.com/user-attachments/assets/bd140190-2184-4dbd-9e06-5cf3ee2d6719" />  
다른 개체 멤버 변수의 소유권을 가져옴  
복사생성자보다 빠름, 얕은 복사랑 비슷한 느낌  
``` cpp
MyString::MyString(MyString&& other) {...}
```

이동 대입 연산자  
이동생성자: 새 개체 만들때 다른 개체 털기  
이동대입연산자: 기존꺼 있고, 다른 개체 털고, 기존 내꺼는 지워주고  
<img width="1013" height="456" alt="image" src="https://github.com/user-attachments/assets/8f4148c7-17ba-4b2e-81eb-5c50f269036b" />  
이동 생성자와 같은 개념, 메모리 재할당 안함, 얕은복사 비슷  
``` cpp
MyString::MyString::operator=(MyString&& other) {...}
```

STL컨테이너용 이동문법: C++11이후, 따로 구현할 필요는 없음.  
<img width="985" height="434" alt="image" src="https://github.com/user-attachments/assets/52e076e9-a0c8-401b-bf7d-8c7257c51dce" />  
<img width="975" height="441" alt="image" src="https://github.com/user-attachments/assets/26eeaf3b-7c7b-4dea-b12a-ab5127af8b45" />  

rvalue 최적화  
- 한때 잘못 사용한 또 다른 C++ 프로그래밍 유행어
- 이동생성자와 이동대입연산자는 아직 유효함
- 포인터 대신 개체 자체를 반환하는 함수
  - 반환값 최적화 (Return Value Optimization)이라 하는 컴파일러 최적화를 깨뜨림
- BP
  - 기본적으로 그냥 개체를 반환하자..
  - 더 빨라진다고 입증된 경우에만 rvalue로 반환하도록 바꾸자

코드보기: 이동생성자와 이동대입연산자  

# constexpr
템플릿 메타프로그래밍:  
<img width="932" height="467" alt="image" src="https://github.com/user-attachments/assets/8131590c-f079-4cb3-9ffb-a5135035e3af" />  
음.. 문제가 복잡해져도 엄청 복잡해질거같음!  
컴파일 도중에 값을 평가하려고 이런짓을 했는데,  
실행중에 값을 평가하려면 그거 전용 함수 따로 만들어야 함.  

constexpr함수, 변수  
위 템플릿 메타프로그래밍의 핵을 해결하기위해 나온것.  
그러면 컴파일시, 실행시 둘 다 값을 평가할 수 있게 됨.  
``` cpp
constexpr unsigned int fibonacci(unsigned int i)
{
  return (i <= 1u) ? i : (fibonacci(i - 1) + fibonacci(i - 2));
}
```
constexpr가 프로그래머의 의도를 보여주는 더 나은 방법임: 컴파일 도중에 값을 평가  
컴파일러가 컴파일 도중에 변수들을 결정지어줌. 못하면 컴파일오류  
함수는 최대한 결정하려 노력. 결정못해도 조용히 넘어가고, 실행 시 그 함수가 호출됨  

예: 함수와 constexpr  
``` cpp
constexpr int Factorial(int n)
{
  return n <= 1? 1: n * Factorial(n - 1);
}

int main()
{
  int value = 3;
  int result1 = Factorial(value);  // OK
  constexpr int result2 = Factorial(value);  // 컴파일 에러
  constexpr int result3 = Factorial(3);  // OK
}
```
판단안되는걸 판단하라고 하니 컴파일 에러.  밑에는 3이 들어왔으니 평가가능.  

컴파일 도중 평가 vs 실행중 평가  
<img width="967" height="350" alt="image" src="https://github.com/user-attachments/assets/7280ac4b-1379-4d98-8cac-5b7878b1f347" />  
파란색은 컴파일평가 되서 값 가르키고, 빨간거는 실행중 함수 호출하도록 함.  
이렇게 컴파일 도중에 반드시 값이 결정되게 하려면 constexpr변수를 쓰자.  
근데, 너무 무거운 연산은 컴파일러가 거부(컴파일 에러)함.  

constexpr활용  
<img width="944" height="371" alt="image" src="https://github.com/user-attachments/assets/49e83963-fa68-4fef-b9f1-da66b12b2a23" />  
이때, 해쉬함수에 활용할 수 있다!  
- 코드가 문자열 참조하는 경우 문자열을 비교해야 함
- 문자열 비교에는 O(N)의 비용이 듦
- 비용을 절감하려면
  - 문자열 해쉬 생성: O(N)
  - 그 후에 해쉬값(정수) 비교: O(1)
- 문자열 해쉬를 컴파일 도중에 만들 수 있면, 문자열 비교에 드는 런타임 비용은 언제나 O(1)이다!
- constexpr로 컴파일 타임에 문자열 해쉬를 만들 수 있게됨!
<img width="918" height="393" alt="image" src="https://github.com/user-attachments/assets/02740651-2526-42ae-8216-6064b95c9df7" />  

const vs constexpr변수: 결국 둘 다 const임  
컴파일 시 결정된 값이니, 당연히 실행 시 바뀌지 않는 cosnt  
``` cpp
const int num = 1;   // OK
num = 10;  // 컴파일 에러

constexpr int num1= 2;   // OK
num1 = 10;  // 컴파일 에러

int num2 = 3;
constexpr int num3 = num2;  // 컴파일 에러

const int num4 = 4;
constexpr int num5 = num4;  // OK

constexpr int num6 = 6;  // OK
constexpr int num7 = num6;  // OK
```
<img width="966" height="550" alt="image" src="https://github.com/user-attachments/assets/09f4f526-6f46-4ec0-a9fb-7a7e5624ceec" />  

이 그림에 Fibonacci 바디는 일부러 생략한 것. 시그내쳐만 보시라.  
- constexpr 함수는 비멤버 함수에도 적용할 수 있다.  
- const 함수는 멤버 함수에만 가능하다.  

코드보기: 간단한 해쉬맵. 동영상 강의 다시 보기  

# Lambda Expression
이름없는 함수. 내포되는 함수(함수 안에 람다 식 정의 하므로)  
람다 식 기본 문법  
[](float a, float b) { return (a>b); }  
<img width="840" height="276" alt="image" src="https://github.com/user-attachments/assets/ae3e3239-8c4f-4de0-a45e-55ab78d0d32b" />  

## 캡쳐 블록  
람다 식을 품는 scope안에 있는 변수를 람다 식에 넘겨둘 때 사용  
캡쳐의 종류  
```
[]
: 비어있음. 캡쳐하지 않음

=
: 값에의한 캡쳐. 모든 외부변수를 캡쳐함, 람다식 안에서 수정 불가

&
: 참조에 의한 캡쳐. 모든 외부변수 캡쳐, 람다식 안에서 수정 가능

<변수이름>
: 특정 변수를 값으로 캡쳐, 람다식 안에서 수정 불가

&<변수이름>
: 특정 변수를 참조로 캡쳐, 람다식 안에서 수정 가능
```
예: 외부 변수 사용하기  
``` cpp
float score1 = 80.f;
float score2 = 20.f;

auto max = []() { return score1 > score2 ? score1 : score2; }; // 람다식에 넘겨준게 없고, scope달라서 컴파일 에러
// ...
```

예: 값에 의한 캡쳐  
<img width="822" height="397" alt="image" src="https://github.com/user-attachments/assets/0ff0e621-371c-4e96-a0bb-5e6eefe35f32" />  
``` cpp
float score1 = 80.f;
float score2 = 20.f;

auto changeValue = [=]()
{
  score1 = 100.f;  // 컴파일 에러, score1 수정 불가
};

changeValue();
// ...
```
이 사례는 궂이 값복사를 해도, 값 못바꾸도록 컴파일오류 나게 구현되있다는걸 말해줌.  

예: 참조에 의한 캡쳐  
<img width="884" height="423" alt="image" src="https://github.com/user-attachments/assets/81933f48-f849-4a89-af47-c0095f0b15dc" />  
코드가 위에서 아래로 흐르다가 changeValue()만나서 다시 위 {}안으로 들어감. 그때의 변수 상황은  
외부 변수도 바뀌어있는거임.  

예: 캡쳐 옵션 섞기  
``` cpp
float score1 = 80.f;
float score2 = 20.f;

auto changeValue = [=, &score1]()  //올바름
{
  score1 = 100.f;  // 참조에 의한 캡쳐
  std::cout << score2; //값에 의한 캡쳐
};

changeValue();

auto magic2 = [=, &y, z]() { y = 10; w = 0; return w + x + y + z;  }; // 컴파일 오류: =로 들어왔는데 z또 추가하면 안됨
// &z로 들어오는건 다른 의도가 있는거니 OK

// ...
```

## 매개변수 목록  
<img width="902" height="457" alt="image" src="https://github.com/user-attachments/assets/2d50ef7d-3c99-4a6f-9a3a-93eab1186915" />  

()를 생략할 순 있다.  
[] 안에 넣는 것은 외부 변수(스코프 밖 변수)를 람다 안으로 가져오는 방법  
() 안에 넣는 것은 람다가 호출될 때 전달되는 '매개변수'  

정렬하기처럼 한번 쓰고 말 함수는 람다식이 좋다.  
<img width="953" height="386" alt="image" src="https://github.com/user-attachments/assets/da344cc1-cbf5-4cf8-9a8b-ca11ab331d7c" />  

## 지정자, 변환 형  
<img width="839" height="319" alt="image" src="https://github.com/user-attachments/assets/1e1d517e-37ab-424c-9bab-026d14e02697" />  
값에의해 캡쳐된 개체를 수정할 수 있게 함.  
<img width="945" height="335" alt="image" src="https://github.com/user-attachments/assets/2169ad5f-19fa-4e59-bab6-25dd03ab66c3" />  
전에는 컴파일오류 났는데, 이 키워드 넣으면 수정 가능  

**반환 형**  
<img width="841" height="307" alt="image" src="https://github.com/user-attachments/assets/460a6212-76be-4d09-9540-98243aec57dd" />  

장단점  
간단한 함수를 빠르게 작성할 수 있음.  
허나, 디버깅하기 힘들어짐  
함수 재사용성이 낮음 (대규모 프로그래밍에서 람다 함수는 눈에 잘 안띄어서 코드중복 잘 생김)  

BP  
1. 기본적으로 이름있는 함수 쓴다
2. 자잘한 함수는 람다로 쓴다 (한 줄짜리 함수)
3. 정렬함수처럼 STL컨테이너에 매개변수로 전달할 함수, qsort() 함수 포인터 등도 람다 함수 추천

# 가변 인자(Variadic) 템플릿 (안중요함)
다양한 매개변수 갯수와 자료형을 지원하는 클래스 또는 함수 템플릿  
매개변수 목록에서 생략부호(...)를 쓴다.  

``` c++
template<typename ... Arguments>
class <class_name> {};

template<typename ... Arguments>
<return_type> <function_name> (Arguments... args);
```

예시 std::make_unique()  
<img width="832" height="143" alt="image" src="https://github.com/user-attachments/assets/32936107-7f7e-40eb-9712-a0f8cb943faf" />  

활용방법: 별로없음. 실용적이지 않음. 

