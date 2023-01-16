# Pointer  

다른함수에 전달 할 때 배열의 시작 주소만 넘겨줌. 원본을 다 너기지 않고 주소만 전달한다.  
Q: 주소를 사용해서 메모리 내에 변수에 접근할 수 있나 ?  
A : Pointer를 쓰면 가능함 !  

1. 어느 변수가 어느 주소에 저장됬는지 확인
``` c
void print_address(void)
{
    int num = 10;
    printf("Address of num : %p\n", (void*)&num);
}

int main(void)
{
    print_address();
    return 0;
}
```
&연산자는 여기서 주소연산자임. 비트연산자가 아님. 비트 연산자는 피연산작 두개, 주소연산자는 피연산자가 한개.  
&num : num변수가 위치한 메모리 주소  
보통 주소 보여줄 때 16진수 사용  
실행할 때 마다 주소 달라지게 컴파일러가 조작해줌. (요즘 os기준, 보안 강화용. 옛날 os는 안그렇대)  

2. 메모리 주소를 저장할 수 있음.  
데이터를 저장할 때는 변수를 씀. 메모리 주소도 변수에 저장 가능.  
``` c
void save_address(void)
{
    int num = 10;
    int num_address = &num;
}

==>>  compile error
저 숫자가 값을 나타내는 건지 주소를 나타내는 건지 알려주지 않아서 그럼.
```
값 : 산술연산 할때 사용하는 수.  
주소 : 메모리 위치.  
특별한 변수, 포인터가 필요함 !!!  

## Pointer  
주소를 저장하기 위한 변수형.  
메모리 주소를 저장하는 변수.  
변수인데, 속에 담긴 내용은 메모리 주소.  
주소를 가리키는 도구  

그 주소에 저장된 자료형은 아무꺼나 다 됨.  
![화면 캡처 2023-01-15 204220](https://user-images.githubusercontent.com/15919242/212538609-2d27c8f4-8850-4479-a70f-722132f44c11.png)  
같은 bit pattern이어도 읽으려는 type 따라서 다르게 읽음.  
따라서, 해당 주소에서 몇 바이트를 읽을지는 하드웨어에 알려줘야함.  
int 포인터, float 포인터, char 포인터 ... 이런 식으로 정의함.  
```c
void save_address(void)
{
    int num = 10;
    int* num_address = &num;
}
/* 포인터 정의 하려면 별표 붙임 
우리 코딩 표준은 int* address; 로 함. int *address;도 됨...
*/

/* 발음법 : pointer to an int 혹은 int포인터. 포인터만은 오른쪽에서 왼쪽으로 읽자. 별 부터 타입으로 읽자. */
```

포인터 변수는 어디 저장되지 ? 얘도 주소라는 값을 어딘가 저장해야하니까.
![image](https://user-images.githubusercontent.com/15919242/212538856-fbefac3b-5c6c-46e9-89e3-9302743412e7.png)  
리틀 엔디언 : 데이터가 끝나는 마지막 단위가 '가장 작은 메모리 주소'에 위치하는 저장 순서(인텔, amd cpu)  
빅 엔디언 : 데이터가 끝나는 마지막 단위가 '가장 큰 메모리 주소'에 위치하는 저장 순서(옛날 기계)  
![image](https://user-images.githubusercontent.com/15919242/212539054-6276c1cb-3852-4222-a47d-b656ddfe21d2.png)

반드시 알아야 할 ascii code : A: 65, a: 97, b:98, c:99  
포인터에 저장된 주소도 바꾸기 당연히 가능.  

포인터를 함수 매개변수로도 쓸 수 있음. 
``` c
void print_address(int* num)
{
    printf("address of num: %p\n", (void*)num);  /* 주소 출력 */
    printf("address of num: %d\n", *num);  /* 역참조 연산자. 주소에 저장된 값 출력 */
}
int score = 88;
print_address(&score);

주소에 저장된 값을 출력 하는 * 연산자를 역참조 연산자라 함
```

## 역참조 : 실제 데이터에 간접적으로 접근.  
indirect 연산자라고 함. indirection...  
```c
*pointer =  50;
*pointer = 123.4f;
로 주소에 있는 값 변경 가능. 다른 타입으로 바꾸는건 안될듯? 주소에 할당된 메모리 공간을 벗어나면
메모리 스톰핑 일어나는거 맞지?
```

함수 정의되면 stack 메모리에 생기고, 함수 리턴이 되면 stack 메모리가 비워지는데, 리턴된 정의된 지역변수들은 메모리에 남아있음. 다른 값들이 바꿀 수 있는 상태임.  
내가 있는 함수의 argument를 전달해준 다른 함수에 있는 변수값을 제어하고 싶으면, pointer 역참조를 하면 됨.  

함수 반환값으로 포인터도 가능하다.
``` int* add(const int op1, const int op2); ```  

댕글링 포인터 (dangling pointer)  
리터되서 사라진 함수에서 정의됬던 지역변수가 사용한 주소 자체가 사라지는 것은 아니고, 컴파일 오류가 나진 않음.  
포인터가 유효하지 않은 주소를 가리키는 것이 문제임.  
포인터를 반환해도 되는 경우.
1. 전역 변수  
data메모리에 들어간거라 ..
2. 파일 속 static 전역 변수  
data메모리에 들어간거라 ..
3. 함수 내 static 변수  
data메모리에 들어간거라 ..
4. 힙 메모리에 생성한 데이터
아예 다른 메모리(힙)에 들어간거라 ..  

## NULL pointer  
```num_ptr = NULL```  
아무것도 가리키지 않는 포인터.  
값이 0인 정수 상수 표현식. 또는 'void*'로 캐스팅된 표현식.  
```c
#define NULL ((void*)0)
/* 널 포인터를 표현할 때 이 매크로를 사용할 것 */
```  
코딩 표준 : 매크로 NULL을 반드시 사용할것.

함수 선조건(precondition)문제  
기본적으로 NULL이 안들어온다고 가정하고 함수를 작성할 것.  
NULL이 들어올 수 있는 함수는 매개변수명에서 분명히 밝힐 것.  
아니면 assert(current_price != NULL)로 하던지.
ex  
``` c
int get_score(const char* const student_id_or_null)
{
...
}
```
NULL 반환은 기본적으로 안함. 반환을 해야한다면 함수 이름에 NULL을 반환하는 것을 명시할 것.  
const char* get_name_or_null(const int id)  

NULL포인터는 사용 예시  
포인터 변수를 초기화하고 싶을 때, 아직 참조할 주소가 없을 때.  
포인터 변수가 유효한 주소를 참조하는지 확인하고 싶을 때 : NULL포인터 역 참조하면 표준 상 undefined behavior임.  
역참조 하기 전에 널포인어인지 확인 if ptr != NULL 하면 좋음.  
댕글링 포인터를 막기 위해. 포인터 변수에 저장된 메모리 주소를 0으로 초기화 해줌.  

## 포인터의 비교  
포인터는 주소를 저장하는 변수임. 동일한 크기를 가짐. 코드를 컴파일 하는 시스템 아키텍쳐에 따라 결정됨.  
보통 cpu가 한 번에 처리할 수 있는 데이터의 크기 (= word, 워드)와 동일함.  
32bit 아키텍쳐에서 포인트 크기는 4바이트  
64t 아키텍쳐에서 포인트 크기는 8바이트  

함수 매개변수로 전달한 배열의 sizeof()연산자는, 배열은 연속된 메모리. 그걸 다 스택에 넣을 수 없음. 따라서 시작위치의 메모리 주소만 전달했음.  

``` c
void print_scores(int scores[])
{
    size_t size = sizeof(scores);  /* 4 반환 */
}
--------
배열을 곧바로 포인터에 대입
int nums[6] = {0, 1, 2, 3, 4, 5};
int* ptr = NULL;
ptr = nums;  /* 컴파일 됨 */
ptr2 = nums[0];  /* int형이지 int*가 아님. 컴파일 안됨 */
ptr3 = &nums[0];  /* 컴파일 됨 */
```  

배열에서 각 요소 사이의 바이트 간격은 일정함. 따라서 첫 번재 요소의 주소와 자료형의 크기만 안다면 k 번째 요소 주소도 알 수 있음.  
근데 주의사항 !!
``` c
int* ptr = nums;
ptr = ptr + sizeof(int);  /* 4를 더함 */
포인터에 정수 1을 더한다 : 포인터의 메모리 위치를 다음 데이터의 위치로 옮기는 것. 
바이트 1 더하는게 아님. 다음 메모리 칸? 으로. 다만 이동하는 칸 크기는 자료형 크기에 따라 다름. 
뺄셈도 ++도 --도 마찬가지. 

int* ptr1 = nums + 3;  /* ptr1는 nums[3]을 가리킴 */
int* ptr2 = &nums[3];  /* ptr2는 nums[3]을 가리킴 */
```
