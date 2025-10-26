# 캐스팅(형변환, Casting)  
C 스타일 캐스팅: 암시적(Implicit) 캐스팅  
컴파일러가 형을 변환해줌. 단, 형 변환이 허용되고, 프로그래머가 명시적으로 변환 안할 때.  
``` c++
int number1 = 3;
long number2 = number1;  // implicit casting
```
**명시적(Explicit) 캐스팅** : 프로그래머가 형 변환을 위한 코드를 직접 작성  
C++캐스팅: static_cast, const_cast, dynamic_cast(예는 모던c++), reinterpret_cast  

왜 이렇게 많나? c스타일 캐스팅이 뭔가 이상해서.  
int score = (int)someVariable; 이라고 하면  
위 4개 종류를 모두 처리해서 명확하지 못한거였음.  
명백한 실수를 컴파일러가 캐치하지 못함. 이를 c++캐스팅이 해결해줌.  

static_cast  
<img width="1037" height="203" alt="image" src="https://github.com/user-attachments/assets/10d42c31-e212-4e68-acc1-77a722434e16" />  
컴파일 도중에 결정남. 오른쪽 문법들은 템플릿 프로그래밍에서 볼거임  

reinterpret_cast  
<img width="1050" height="173" alt="image" src="https://github.com/user-attachments/assets/09d69b9d-acaa-4b66-9798-d23a08c2c64f" />  
포인터 주소를 저장함.  

const_cast  
<img width="1006" height="246" alt="image" src="https://github.com/user-attachments/assets/7a10b2dd-1547-4114-8304-a463a0f96aac" />  
const임에도 const아닌 타입으로 캐스팅해서 내용 바꿔버리는 나쁜 코드.  

dynamic_cast  
<img width="1010" height="93" alt="image" src="https://github.com/user-attachments/assets/c15accf9-b1a2-46bc-9c2e-f179532cb589" />  
실행중에 일어나는 변환. static_cast는 컴파일 도중에 일어남.  

## static_cast 
값에 쓰일때  
<img width="847" height="373" alt="image" src="https://github.com/user-attachments/assets/b26e41af-4363-443a-a61c-69af61966277" />  
<img width="827" height="271" alt="image" src="https://github.com/user-attachments/assets/04a8e294-73bd-4798-a4ce-c90c47da4183" />  
개체 포인터에 쓰일때 (값에 쓰일때랑 많이 다름)  
<img width="775" height="330" alt="image" src="https://github.com/user-attachments/assets/746ffe43-0ad0-49bf-baf5-043458cbedb3" />  
컴파일은 되지만, Dog의 함수 호출하려고 하면, 엉뚱한 lookup table을 뒤지거나 이상하게 돌 수 있다.  
<img width="706" height="113" alt="image" src="https://github.com/user-attachments/assets/09fd70cf-40cd-4ce5-b6ce-2ab67c8f1264" />  
아예 상관없는 변환은 막아줌.  

``` c++
#pragma once

namespace samples
{
	void ObjectPointerCastingExample();
}
====
#include <iostream>

#include "Animal.h"
#include "Cat.h"
#include "Dog.h"
#include "ObjectPointerCastingExample.h"

using namespace std;

namespace samples
{
	void ObjectPointerCastingExample()
	{
		Animal* pet1 = new Cat(2, "Lulu");
		Animal* pet2 = new Dog(2, "Burnaby");
	
		Cat* cat = static_cast<Cat*>(pet1);
		Dog* dog1 = static_cast<Dog*>(pet2);
		Dog* dog2 = static_cast<Dog*>(pet1);  // 재밌는거! 컴파일 됨

		cout << "cat's name : " << cat->GetName() << endl;
		cout << "dog1's address :" << dog1->GetAddress() << endl;

		// prints cat's name instead
		cout << "dog2's address : " << dog2->GetAddress() << endl;
    // Dog의 주소가 아니라 Cat의 이름을 출력한다.
    // 정적바인딩이었음. virtual 아니었음!
    // 메모리에 우연히 있던 멤버변수 주소를 읽은것.
		delete pet1;
		delete pet2;
	}
}
```

## reinterpret_cast
뭔가 재해석함. C에서 가장 위험한 캐스팅, C++에서 가장 위험한 캐스팅 중 하나.  
<img width="1036" height="113" alt="image" src="https://github.com/user-attachments/assets/fc953bef-48a9-4a8e-be34-7f4f91f020f1" />  
<img width="694" height="386" alt="image" src="https://github.com/user-attachments/assets/84e52407-f188-4521-b708-2c284b358562" />  
이진수 표기는 달라지지 않는다는게 중요한 포인트!  
같은 이진수 패턴을 어떻게 해석하느냐의 문제임  
메모리를 보자!  
<img width="1063" height="436" alt="image" src="https://github.com/user-attachments/assets/fe1a1c39-885f-4261-91d7-8eafb014e3f7" />  

static_cast와 비교  
<img width="923" height="346" alt="image" src="https://github.com/user-attachments/assets/8c5f7ead-f82e-4655-9165-50a9004b9982" />  
QnA  
<img width="886" height="470" alt="image" src="https://github.com/user-attachments/assets/aea01a00-a55d-44af-9c4a-eb971d1ea389" />  

코드보기: Tiger 개체의 주소 저장하기 (건전하게 필요한 경우)  
object의 주소 기반 offset으로 원하는 object주소 추정할 때.  
``` c++
#pragma once

namespace samples
{
	void ObjectAddressSavingExample();
}
=======
#include <iostream>
#include "ObjectAddressSavingExample.h"
#include "Tiger.h"

using namespace std;

namespace samples
{
	void ObjectAddressSavingExample()
	{
		Tiger* tiger = new Tiger(5);
		unsigned int intAddress = reinterpret_cast<unsigned int>(tiger);

		cout << "saving address as int: " << intAddress << endl;
		cout << "read int address to pointer" << endl;

		tiger = reinterpret_cast<Tiger*>(intAddress);
		tiger->PretendIAmAZebra();

		delete tiger;
	}
}
```

## const_cast
하지 말아야할 캐스팅  
<img width="1011" height="214" alt="image" src="https://github.com/user-attachments/assets/bc646f2c-ba47-4e4e-88d6-6feaf87ce459" />  
<img width="921" height="345" alt="image" src="https://github.com/user-attachments/assets/b878721a-b556-4482-93ec-4af051661e53" />  
포인터 형에 사용할 때만 말이 됨. 값 형은 언제나 복사되니깐.  
const_cast를 코드에서 쓰려고 한다면, 뭔가 잘못하고 있는거임!  
근데, 써야만 할 때: 써드파티 라이브러리가 const를 제대로 사용하지 않을 때  
<img width="718" height="162" alt="image" src="https://github.com/user-attachments/assets/76363c93-1620-49d2-9f85-57809624aac4" />  

## dynamic_cast(별로 안중요함)
<img width="988" height="364" alt="image" src="https://github.com/user-attachments/assets/f66f7511-74d2-4ff1-9f9f-f63e09c5321a" />  

실행중에 형을 판단. 포인터 또는 참조형을 캐스팅할 때만 사용가능.  
호환되지 않는 자식형으로 캐스팅하려하면 NULL반환. 따라서 static_cast보다 안전.  
그러나, 이걸 쓰려면 RTTI(실시간 타입 정보, real time type information)을 켜야함.  
그러나, 보통 c++에선 성능을 중시하므로 RTTI, exception 보통 끔.  

뭔가 자질구레하게 많네... best practice를 정하자!  
캐스팅 규칙  
<img width="929" height="422" alt="image" src="https://github.com/user-attachments/assets/f1e25e08-275c-4f9f-acd7-6804118c3c82" />  

# 인라인 함수(Inline Functions)
코드 가독성, 성능을 모두 고려한 개념.  
함수 호출 시, 함수는 메모리 안에 할당되어있고, 함수 호출 단계는  
변수들을 스택에 push, 함수 주소로 점프, 함수 실행, 호출자 함수로 다시 점프, 스택에 push된 변수들을 다시 pop  
즉 여러 단계라서 좀 느림. cpu캐시에 최적이 아닐수도, 모던cpu아키텍처에서는 더 느림.  
그래서 모든걸 함수로 만들어라는 조언은 개소리임.  
<img width="649" height="235" alt="image" src="https://github.com/user-attachments/assets/79f63831-8884-4427-9a50-54e258cbf558" />  

수학 연산들은 함수화 하면 좋음.  
해법은 인라인 함수!  
<img width="749" height="372" alt="image" src="https://github.com/user-attachments/assets/36b7ea89-5a0e-429b-be73-81a69b12146f" />  

인라인 함수의 동작 원리  
int age = myCat->GetAge();로 원래 되어잇는데, 컴파일러가 아래처럼 바꿔줌.  
<img width="855" height="207" alt="image" src="https://github.com/user-attachments/assets/dc109fef-6fd4-4f1e-aca2-7558dcd5e3b3" />  

물론, access권한 있는지 컴파일러가 검사해주고 이렇게 바꿈.  

비슷해 보이는데, 인라인 대신 매크로를 써도 되나? No.  
매크로는 디버깅 힘들고, 콜스택에 함수이름 안보이고, 중단점도 설정 불가.  
매크로는 scope를 준수하지 않음. 매크로 써야만 하는 상황 아니면 인라인 함수를 쓰자.  
<img width="813" height="226" alt="image" src="https://github.com/user-attachments/assets/9b293f23-4823-43ca-b715-74b80a5825cc" />  

인라인 주의점  
인라인 키워드 안써도, 컴파일러가 인라인화 할 수도 있고,  
인라인 붙은 함수를 인라인화 안할수도 있음 (힌트역할일 뿐).  
인라인 함수 구현이 헤더파일에 위치해야함.  
  - 복붙하려면 컴파일러가 그 구현체를 볼 수 있어야 하므로
  - 각 cpp파일은 따로 컴파일됨
  - 따라서 b.h를 include하는 a.cpp 파일을 컴파일 할 때, 컴파일러는 b.cpp에 뭐가 있는지 모름

간단한 함수에 적합함. getter, setter등...  
실행파일 크기 증가가 쉬움. 동일한 코드를 여러 번 복붙하니까  
그래서 남용금지!  
실행파일이 작을수록 cpu캐시하고 잘 작동해서 속도가 빨라질 수 있음  

QnA: 컴파일 중에 인라인 함수를 복사+붙여넣기 하기 때문에, 정적 바인딩에 해당하는 함수들만 인라인 함수로 사용할 수 있는건가요?? 제가 제대로 이해했다면, 가상함수들은 동적 바인딩에 속하므로, 인라인을 못쓰는게 맞는건지요?  
A: 네 그렇습니다.  

# static 키워드
<img width="694" height="249" alt="image" src="https://github.com/user-attachments/assets/3c76c3e8-6de5-4adb-8935-5de01ffd3bf0" />  

static: scope의 범위를 받는 **전역변수**  
파일 속, 네임스페이스 속, 클래스 속, 함수 속  

extern 키워드: 다른 파일의 전역변수에 접군가능하게 해줌.  
<img width="698" height="301" alt="image" src="https://github.com/user-attachments/assets/17418e17-2935-4c59-92b5-a2f924f76770" />  

main.c obj와 externtest.c obj를 링커에서 연결해주면서 extern 변수 주소를 찾게됨.  
근데 static 키워드를 넣으면,  
<img width="684" height="326" alt="image" src="https://github.com/user-attachments/assets/8bffe7d4-e5d4-4f10-bd8f-d700b91c54b6" />  

외부 파일에서 함부로 쓰지 못하게 범위 제한했었음.  

## static 변수, 멤버변수
<img width="812" height="371" alt="image" src="https://github.com/user-attachments/assets/cf36d2ac-f155-44e4-8178-b8664e86546b" />  

c++ static 변수 초기화는 한번만 됨.  

함수 속 정적 변수는, 함수 밖에서는 접근 불가함.  
<img width="781" height="320" alt="image" src="https://github.com/user-attachments/assets/661b62d5-1376-400d-9a43-2c716d7ed3a2" />  

클래스 속 정적 멤버변수  
<img width="697" height="367" alt="image" src="https://github.com/user-attachments/assets/70e2643b-ffe1-45b2-8e3a-dfcf0bf9bbc4" /> 

클래스당 하나의 copy만 존재  
각 개체의 메모리 레이아웃의 일부가 아님  
클래스 메모리 레이아웃에 포함됨. 오직 하나!  
exe파일 안에 필요한 메모리가 잡혀있음.  

**정적 멤버 변수 BP**  
함수 안에 정적 변수를 넣지 말고, 클래스 안에 넣기  
범위제한을 위해 전역변수 대신 정적 멤버변수를 쓸 것  
C스타일 정적변수를 쓸 이유가 이제 없음  

<img width="791" height="348" alt="image" src="https://github.com/user-attachments/assets/c581a100-a07d-405b-a239-4b0557d96c25" />  

메모리에 mCount변수는 1개 생기고 mCount 값4임.  
mCount는 데이터섹션의 메모리. 각 개체는 힙 메모리에.  

``` c++
#pragma once

namespace samples
{
	class Cat2
	{
	public:
		Cat2(int age, const char* name);
		virtual ~Cat2();

		static const char* GetType();

	private:
		static const char* mAnimalType;

		int mAge;
		char* mName;
	};
}
=====
#include <iostream>
#include "Cat2.h"

namespace samples
{
	const char* Cat2::mAnimalType = "Cat";
	// 헤더에 이미 static키워드 있어서 여긴 static 안씀

	Cat2::Cat2(int age, const char* name)
		: mAge(age)
	{
		mName = new char[strlen(name) + 1];
		memcpy(mName, name, strlen(name) + 1);
	}

	Cat2::~Cat2()
	{
		delete[] mName;
	}

	// static function
	const char* Cat2::GetType()
	{
		return mAnimalType;
	}
}
=====
#pragma once

namespace samples
{
	void StaticMemberVariableExample();
}
=====
#include <iostream>
#include "Cat2.h"
#include "StaticMemberVariableExample.h"

using namespace std;

namespace samples
{
	void StaticMemberVariableExample()
	{
		Cat2* myCat1 = new Cat2(2, "Lulu");
		Cat2* myCat2 = new Cat2(5, "Poppy");
		Cat2* myCat3 = new Cat2(3, "Teemo");
		Cat2* myCat4 = new Cat2(7, "Amumu");

		cout << "myCat1's type : " << myCat1->GetType() <<endl;
		cout << "myCat2's type : " << myCat2->GetType() << endl;
		cout << "myCat3's type : " << myCat3->GetType() << endl;
		cout << "myCat4's type : " << myCat4->GetType() << endl;
		// 위 네개 모두 같은거 호출함
		cout << "global cat type :" << Cat2::GetType() << endl;
		// 개체 아니고 클래스소유이므로 클래스명으로 바로 호출 가능
		delete myCat1;
		delete myCat2;
		delete myCat3;
		delete myCat4;
	}
}
```

## 정적 멤버 함수
<img width="830" height="368" alt="image" src="https://github.com/user-attachments/assets/7a5913e2-fa51-4eab-99eb-2847c60c2d72" />  

논리적인 scope에 제한된 전역함수  
해당 클래스의 정적 멤버에만 접근 가능  
개체없이도 정적함수 호출 가능. Math::Square(10);  

정적메서드에서 비정적 멤버변수 쓰려고 하면, 어떤 개체를 봐야할지 특정불가하므로, 컴파일오류 뜸.  

올림함수 트릭:  
<img width="681" height="407" alt="image" src="https://github.com/user-attachments/assets/136f312c-476b-4694-a98d-ddb16bb20f78" />  

내림함수 트릭: return static_cast<int>(value);  
반올림 트릭: static_cast<int>(value + 0.5f);  
