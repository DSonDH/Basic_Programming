# 새로 추가된 STL
std::unordered_map (그리고 unordered_multimap)  
std::unordered_set (그리고 unordered_multiset)  
std::array  

## 정렬 안된 맵(unordered_map)  
std::map은 자동으로 정렬되는 컨테이너.  
요소 삽입/제거가 빈번하면 성능이 저하됨.  
``` cpp
#include <iosteam>
#include <string>
#include <unordered_map>

int main()
{
  std::unordered_map<std::string, int> scores;
  scores["Nana"] = 60;
  scores["Mocha"] = 70;
  scores["Coco"] = 100;

  for (auto it = scores.begin(); it != scores.end(); ++it)
  {
    std::cout << it->first << ": " << it->second << std::endl;
    // 알파벳 순이 아닌, Coco, Nana, Mocha순서로 출력됨.
  }
  return 0;
}
```
key, value 쌍을 저장  
키는 중복 불가  
자동으로 정렬되지 않는 컨테이너  
해쉬맵 기반, O(1)으로 바뀜!!  
해쉬함수가 생성하는 index기반 bucket들로 요소가 구성됨!!  
* 같은 키 넣으면 순서 보장이될까? 버킷 기반 해시 컨테이너라서 순회 순서가 표준에서 보장되지 않는다
* 구현, 컴파일러, 버전, 재해싱 여부 등에 따라 순서가 바뀔 수 있다.

<img width="694" height="451" alt="image" src="https://github.com/user-attachments/assets/dcedc12f-192d-4034-a21a-63d254565150" />  

예시: 버킷 내용 보여주기  
<img width="735" height="374" alt="image" src="https://github.com/user-attachments/assets/ef1f5746-1cdb-4917-bbb9-e2d50536c8af" />  
<img width="867" height="286" alt="image" src="https://github.com/user-attachments/assets/c8227a69-83de-4e0c-843b-698dcc6bca6e" />  

## 정렬 안된 셋(unordered_set)
<img width="843" height="287" alt="image" src="https://github.com/user-attachments/assets/52ff0c09-add9-4f59-8eb4-bd9adc687494" />  

코드보기: 시간측정하는 방법 소개함.  

## 어레이(array) (중요하진 않음)
전에 만든 FixedVector 템플릿 클래스와 비슷  
허나, 요소 수를 기억하지 않음. 단순히 C스타일 배열을 추상화한 것  
<img width="661" height="355" alt="image" src="https://github.com/user-attachments/assets/dbb4d962-2988-48d7-b1ac-578393ea4d58" />  

numbers[0]을 했다는거는, FixedVector와 구현이 다른것임.  
즉 std::array는 요소 수를 기억안해줌!!  
그래서 그리 좋진않음.  

## 범위 기반 for loop
반복자보다 좋은 것. for each와 비슷함  
<img width="810" height="277" alt="image" src="https://github.com/user-attachments/assets/7593eec0-c627-46a2-a378-d105366193e9" />  

container아니어도 돈다!  
왼쪽은 값으로 복사 (원본 안바뀜), 오른쪽은 참조로 가져옴(원본 바꿀수 있음)  
for 반복문을 더 간단하게 쓸 수 있고 가독성 높아짐  
auto키워드도 쓸 수 있음. 컨테이너/배열 역순회는 안됨  
<img width="825" height="363" alt="image" src="https://github.com/user-attachments/assets/9496af14-64e8-45e8-82b0-e67d89434cd8" />  
<img width="819" height="363" alt="image" src="https://github.com/user-attachments/assets/d732965b-2d2f-499a-8237-c9f3352fcef1" />  

참고) for_each()
- C++03에 들어옴
- 컨테이너 각 요소마다 함수를 실행하는 알고리듬
- 범위기반 for만큼 가독성 좋진 않음
- 좀 이상함: 다른 언어들은 알고리듬 말고 언어 문법 자체에 있음
- 그러니 이거 말고 범위기반 for를 쓰자 ^_^/

# Smart 포인터
unique_ptr, shared_ptr, weak_ptr 세 종류가 있음.  
unique_ptr가 매우매우 좋고 중요함  

기존 포인터의 문제점  
할당하고 지우지 않으면 메모리 누수 난다!  
근데 이걸 스마트포인터가 해줌!!  
그리고 가비지 컬렉션보다 빠르다!!  

## Unique 포인터 (C++11)
포인터 소유자가 하나밖에 없다!  
<img width="809" height="226" alt="image" src="https://github.com/user-attachments/assets/f5a8a791-3326-473e-8f17-a10d91668542" />  

std::unique_ptr  
- 포인터(원시 포인터라 부르자)를 단독으로 소유함
- 원시(naked) 포인터는 누구랑도 공유하지 않음
- 따라서 복사나 대입 불가
- unique_ptr가 scope벗어날 때, 원시포인터는 자동으로 delete됨
``` cpp
std::unique_ptr<Vector> myVector(new Vector(10.f, 30.f);
std::unique_ptr<Vector> copiedVector1 = myVector; // 컴파일 에러
std::unique_ptr<Vector> copiedVector2(myVector); // 컴파일 에러
```

다음의 세 경우에 적합함!  
1. 클래스 생성자/소멸자 (소멸자 귀찮게 짜던거 안해도 됨.)  
<img width="831" height="368" alt="image" src="https://github.com/user-attachments/assets/a4901bab-9357-46cb-8ea1-a2144005bcbf" />  

2. 지역변수 (scope 밖으로 가면 자동으로 지워지므로)  
<img width="831" height="337" alt="image" src="https://github.com/user-attachments/assets/22165faa-e9eb-443f-a96b-69bb1380da9a" />  

3. STL벡터에 포인터 저장하기 (for문으로 모든 요소 일일히 clear호출도 안해도 됨)  
<img width="824" height="347" alt="image" src="https://github.com/user-attachments/assets/a6238802-46b0-4608-a7a6-f535b369de9f" />  

### 유니크 포인터 만들기 (C++14이후)
문제: 원시 포인터 공유가 되서, 한 유니크 포인터를 바꾸면 다른 유니크 포인터가 나도 모르는 새 바뀜.  
<img width="609" height="363" alt="image" src="https://github.com/user-attachments/assets/545b5ef4-3c70-44d9-bfef-34dc5101561f" />  
<img width="603" height="360" alt="image" src="https://github.com/user-attachments/assets/86c9b0a1-1e95-49df-89a6-65fcc143a42c" />  
<img width="599" height="334" alt="image" src="https://github.com/user-attachments/assets/88a52800-66ec-44ad-8f7b-d1b067be93d5" />  

이를 해결하고자, 언어에 새로운 기능을 넣음  
std::make_unique<Vector>(10.f, 10.f); 이렇게 만들어서 대입하도록.  
``` cpp
#include <memory>
#include "Vector.h"
int main()
{
  // 힙할당 불필요. 사용법 보여주려고 함.
  std::unique_ptr<Vector> myVector = std::make_unique<Vector>(10.f, 30.f);
  myVector->Print();
  return 0;
}
```
주어진 매개변수와 자료형으로 new키워드를 호출해줌. 따라서 원시포인터와 같음.  
둘 이상의 std::unique_ptr이 원시 포인터를 공유할 수 없도록 막는게 전부.  
<img width="696" height="135" alt="image" src="https://github.com/user-attachments/assets/fc926e13-ea70-4a35-8598-7c38b705df40" />  

위 코드에 세가지 방법 전부 컴파일오류 남!!  
즉, 이미 만들어진 개체는 절대 make_unique할 수 없다.  
(인자로 개체 생성하도록 넘겨주는거면 make_unique안해도 되는건데, 추가 이득이 좀 더 있다고 함)  

<img width="716" height="337" alt="image" src="https://github.com/user-attachments/assets/fb97aa20-c383-4ae0-9c3d-66fa41e7db05" />  

가변인자 템플릿(... 이 부분), r-value 개념이 들어간 개념임.  

### 유니크 포인터 재설정, 원시 포인터 가져오기, 원시 포인터 소유권 박탈하기
유니크 포인터 재설정하기  
<img width="757" height="285" alt="image" src="https://github.com/user-attachments/assets/5fbf3641-0deb-47b9-890c-b31e2e5580a3" />  
<img width="713" height="357" alt="image" src="https://github.com/user-attachments/assets/ef84f9b0-c1b7-48de-87eb-279f13cb06a0" />  
<img width="772" height="356" alt="image" src="https://github.com/user-attachments/assets/5ec64bde-e977-4fc8-a735-0ae3abd19ce9" />  
<img width="720" height="385" alt="image" src="https://github.com/user-attachments/assets/a2811332-67f5-4ffc-b001-23fc27040318" />  

reset은 nullptr와 같다.  
- vector.reset();, vector = nullptr; 두 코드는 같다.  
- nullptr이 가독성이 더 높음
- 하지만 reset()은 vector가 원시포인터가 아님을 분명하게 보여줌
- 포프님은 개인적으로 nullptr선호

``` cpp
std::vector<std::unique_ptr<int>> v;

std::unique_ptr<int> p1 = std::make_unique<int>(10);
std::unique_ptr<int> p2 = std::make_unique<int>(20);

v.push_back(p1);  // p1 은 lvalue라서 복사를 시도하게 되는데, unique_ptr 는 복사 생성/복사 대입이 삭제(delete) 되어 있어서 컴파일 오류
v.push_back(std::move(p2));  // OK
```

get()  
naked 포인터 반환  
<img width="860" height="327" alt="image" src="https://github.com/user-attachments/assets/bc5cb0cd-2461-4538-848f-3c48c0f7d8b3" />  

release()  
naked 포인터 소유권을 다른 포인터에 넘겨줌. 좋은 함수는 아님.  
``` cpp
std::unique_ptr<Vector> vector = std::make_unique<Vector>(10.f, 30.f);
Vector* vectorPtr = vector.release();
// ...
```
release()호출 후 get() 호출하면 nullptr반환됨.  

### 소유권 이전하기
유니크 포인터를 복사는 못해도, 소유권을 이전해줄 수만 있음.  
<img width="726" height="364" alt="image" src="https://github.com/user-attachments/assets/ff7ccf26-353b-4018-acb0-00e3364d870d" />  
<img width="718" height="386" alt="image" src="https://github.com/user-attachments/assets/60c74468-215e-4e6e-b033-e443d5d1464c" />  

대입x 복사x 이전o  
const면 당연히 못옮기니 컴파일 에러  

std::move()  
- 개체A의 모든 멤버를 포기하고 그 소유권을 B에 준다
- 메모리 할당, 해제가 일어나지 않음
- A에 있는 모든 포인터를 B에 대입하고 A에는 nullptr넣는것
- "난 멤버변수를 옮기고 있다(MOVING)"
- 어떻게 도는지 알려면 r-value, 이동(move)생성자를 배워야 함: 나중에 나옴

* release(), move()차이

| 구분 | release() | std::move() |  
| - | - | - |  
| 소유권          | 포기함                        | "다른 unique_ptr 에게" 이전함 |  
| 반환값          | raw pointer                | 없음                     |  
| 이후 delete 책임 | 사용자                        | unique_ptr 자동 관리       |  
| 위험성          | 매우 높음                      | 안전함                    |  
| 사용 의도        | 스마트 포인터 → 생 포인터로 넘기는 특수 상황 | unique_ptr 간 소유권 이전    |  

예시: STL벡터에 요소 추가하기  
``` cpp
std::vector<std::unique_ptr<Player>> players;
std::unique_ptr<Player> coco = std::make_unique<Player>("Coco");
players.push_back(std::move(coco));

std::unique_ptr<Player> lulu = std::make_unique<Player>("Lulu");
players.push_back(std::move(lulu));
```

### BP
std::unique_ptr의 비밀 공개  
``` cpp
// 매우 단순화시킨 코드
tmeplate<typename T>
class unique_ptr<T> final
{
public:
  unique_ptr(T* ptr) : mPtr(ptr) {}
  ~unique_ptr() { delete mPtr; }
  T* get() { return mPtr };
  unique_ptr(const unique_ptr&) = delete;
  unique_ptr& operator=(const unique_ptr&) = delete;
private:
  T* mPtr = nullptr;
}
```
이제 다들 이걸 씀. 직접 메모리 관리하는 것만큼 빠름.  
RAII(Resource Acquisition Is Initialization) 원칙에도 잘 맞음.  
실수하기 어려우니까 모든 곳에 쓰자!!  

## 가비지 콜렉션 (Gargage collection)
자동 메모리 관리는, 가비지 컬렉션, 참조 카운팅 두 가지 방법이 있음.  

가비지 콜렉션: 보통 tracing garbage collection을 의미함.  
주기적으로 컬렉션을 실행해서 메모리 누수를 막으려는 시도.  
충분한 여유메모리가 없으면 컬렉션이 실행됨.  
매 주기마다 GC는 root를 확인함 (전역변수, 스택, 레지스터)  
힙에 있는 개체에 루트를 통해 접근할 수 있는지 판단  
접근할 수 없다면 가비지로 간주해서 해제  
(이 과정을 최적화 하는게 seasonal GC임)  
(generation gc인거같은데, 0세대, 1세대, 2세대 ... 이렇게 구분해서  
세대별로 컬렉팅 수행해서 모든 메모리를 훑지 않도록 한거라고 함)  
GC의 문제점: 사용되지 않는 메모리를 즉시 정리하지 않음  
GC가 메모리 해제판단하는 동안 앱이 멈추거나 버벅일 수 있다  

### 참조 카운팅 (Ref. Counting)
개체에 대한 참조가 없을 때 개체가 해제됨.  
참조 횟수를 활용해서 특정 개체가 몇 번이나 참조되는지 판단 가능.  
scope를 벗어나는 경우 등등에서 참조 횟수 감소함.  
<img width="797" height="350" alt="image" src="https://github.com/user-attachments/assets/93ad4c01-5624-4d1b-9a3f-aca51793687d" />  
<img width="805" height="337" alt="image" src="https://github.com/user-attachments/assets/d80f2f61-46a9-481f-b183-d87d7d128a99" />  

예시: 수동 참조 카운팅  
<img width="1256" height="578" alt="image" src="https://github.com/user-attachments/assets/ec5a4ec5-f382-4aeb-b7dc-aae090abe2c1" />  

COM(즉 DirectX)이 수동 참조 카운팅을 지원.  
std::shared_ptr는 이걸 자동으로 해줌!  

강한(Strong) 참조: 개체A가 개체B를 참조할 때, B는 절대 소멸되지 않음을 의미  
강한참조 수를 저장하기 위해 강한 참조 카운트를 사용  
새 개체에 대한 참조를 만들 때 강한참조 횟수가 늘어나고, 0이 되면 해당 개체는 소멸됨  

참조 카운팅의 문제점: 참조횟수는 너무 자주 바뀜.  
멀티쓰레드 환경에서 안전하려면, lock이나 atomic연산이 필요.  
++mRefCount보다 확연히 느림  
순환참조문제 해결이 안됨! (곧 배울텐데, c++에 해결책이 있음)  
- 전통적인 메모리 누수는 없음
  - 즉, delete 잊은 경우.
- 하지만 여전히 메모리 누수발생 가능
  - 예: 순환참조
  - 이런 실수는 덜 하지만, 발견한들 고치기 쉽지 않음
    
가비지컬렉션 vs 참조카운팅  
- 가비지컬렉션
  - 사용하기 훨씬 쉽다
  - 실시간/고성능 프로그램에 부적합 (계속 정지되는 순간 존재)
- 참조 카운팅
  - 사용하기 쉽다
  - 실시간/고성능 프로그램에 적합
  - 멀티스레드 환경에서는 순수한 포인터보다 훨씬 느림

## 공유(Shared) 포인터
std::shared_ptr만들기  
``` cpp
std::shared_ptr<Vector> vector = std::make_shared<Vector>(10.f, 30.f);
```
<img width="900" height="435" alt="image" src="https://github.com/user-attachments/assets/0474b0ea-4ece-495a-94bd-356ce968ddac" />  

예시: 포인터 공유하기  
<img width="1002" height="332" alt="image" src="https://github.com/user-attachments/assets/c5d052ba-dd87-488d-aee3-c5148f04b322" />  
<img width="829" height="422" alt="image" src="https://github.com/user-attachments/assets/a55e4a50-5ecb-477a-a490-2099c4eb2d0e" />  

예시: 포인터 재설정하기(reset())  
<img width="813" height="448" alt="image" src="https://github.com/user-attachments/assets/56ac02d2-3c12-40a4-9aad-98af1ce90538" />  
<img width="916" height="433" alt="image" src="https://github.com/user-attachments/assets/c4c3a424-d582-42b0-991d-95a011dcafc9" />  

원시 포인터를 해제한다. 참조 카운트가 1 줄어듦  

예시: 참조 횟수 구하기 (안중요)  
``` cpp
std::shared_ptr<Vector> vector = std::make_shared<Vector>(10.f, 30.f);
std::cout << "Vector: " << vector.use_count() << std::endl;  // vector:1

std::shared_ptr<Vector> copiedVector = vector;
std::cout << "Vector: " << vector.use_count() << std::endl;  // vector:2
std::cout << "copiedVector: " << vector.use_count() << std::endl;  // copiedVector:2
```

순환참조 예시  
<img width="987" height="323" alt="image" src="https://github.com/user-attachments/assets/b0edd32b-571b-4f0f-894d-1c0f002eb3fe" />  
<img width="916" height="411" alt="image" src="https://github.com/user-attachments/assets/899f12f3-9b9b-4ccb-9a72-f7e1966668c0" />  

Pet, Owner가 서로 참조하고 아무도 그 둘을 안쓰고 있어서 그럼!  
이는 또 다른 스마트포인터인 weak포인터로 고칠 수 있음  

코드보기: 공유포인터와 단일연결리스트  

## 약한(Weak 포인터)  
약한참조! 원시포인터 해제에 영향을 끼치지 않음  
약한참조로 참조되는 개체는 강한참조 카운트가 0이 될 때 소멸됨  
순환참조 문제의 해결책  

약한 포인터 만들기  
<img width="898" height="449" alt="image" src="https://github.com/user-attachments/assets/8f0f9c97-1331-4ba5-949b-b7c1321110d6" />  

약한참조는 강한참조 shared pointer에서 만들어진다.  
<img width="863" height="201" alt="image" src="https://github.com/user-attachments/assets/93afd03c-2553-43cc-b52f-015b133b1e68" />  

### 약한 포인터로 공유포인터 만들기  
<img width="1002" height="427" alt="image" src="https://github.com/user-attachments/assets/2701ea71-1975-4ded-8320-2848beafa886" />  

lock()으로 참조를 하나 더 넣어줌.  
<img width="957" height="423" alt="image" src="https://github.com/user-attachments/assets/64fe3c43-6776-43c1-8fa2-1f733edd1ba9" />  

lock(): 내가 쓰고있는 도중에 남이 지우지 못하게 한다.  

공유포인터 존재 확인하기: expired()  
<img width="1042" height="436" alt="image" src="https://github.com/user-attachments/assets/ac248b7e-462c-4aac-8dbf-d25b32d9f20c" />  

expired()만으로 안전하게 프로그래밍은 힘듬. true면 죽은거 확인 가능한데,  
false라고 쓰려고 했는데 그 순간 남이 죽여버릴수도 있거든.  

약한 포인터로 순환 참조를 해결해보자  
<img width="1033" height="429" alt="image" src="https://github.com/user-attachments/assets/9cf992e7-403a-4648-b187-f4c39b6aa6b9" />  

스마트 포인터와 이중연결리스트  
<img width="979" height="279" alt="image" src="https://github.com/user-attachments/assets/62571e70-a514-47b2-a79d-0422518b19d7" />  
<img width="1024" height="223" alt="image" src="https://github.com/user-attachments/assets/719faea9-3e2d-4fd5-bb7b-dde78dd2be53" />  
<img width="1034" height="296" alt="image" src="https://github.com/user-attachments/assets/edd6e029-29c2-4b0f-9b6f-7c4a46f84725" />  

첫번째 노드, 두번쨰 노드 사이를 끊어보자 ...  
<img width="1023" height="248" alt="image" src="https://github.com/user-attachments/assets/117dbe12-cf6d-4818-8855-5e9369deb77e" />  

해제 불가능! 약한포인터로 해결해보자!  
<img width="1011" height="216" alt="image" src="https://github.com/user-attachments/assets/dd260e9b-1015-4d51-99fc-488e395caca5" />  
<img width="968" height="189" alt="image" src="https://github.com/user-attachments/assets/01668f33-f75e-425e-b095-4bb8b3e53c6e" />  
<img width="1009" height="188" alt="image" src="https://github.com/user-attachments/assets/00e45dad-14ac-45c4-a395-1e741f3b5b3a" />  
<img width="997" height="313" alt="image" src="https://github.com/user-attachments/assets/1e74706a-3d07-4727-9a0a-227ee274b3ef" />  

뒤에 강한참조 횟수가 순차적으로 0이 되면서 하나씩 사라질것임.  
그래서 첫번째 노드만 남음  

<img width="1041" height="289" alt="image" src="https://github.com/user-attachments/assets/d1971e11-76e8-4421-8d75-ed13e8f74afe" />  

코드보기: 간단한 Cache  
