# Pointer  

다른함수에 전달 할 때 배열의 시작 주소만 넘겨줌. 원본을 다 넘기지 않고 주소만 전달한다.  
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
메모리 주소를 저장하기 위한 변수형.  
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
주소 바로 다음에 실제 저장된 값 bit pattern이 메모리에 저장되네 ?  

![image](https://user-images.githubusercontent.com/15919242/219949191-2643c6e1-7a2d-43f5-8997-5af2ef2781d8.png)  
![image](https://user-images.githubusercontent.com/15919242/219949206-0deff7b3-a3fd-4de6-95dd-2996a6f17445.png)  
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

## 역참조 연산자 : 실제 데이터에 간접적으로 접근.  
C에서 포인터로 부르는 것들이 다른 언어에서는 참조로 불린대.  
지금까지는 모든 데이터를 복사해서 썻는데, 주소로 원본에 접근하는 방식이 생긴것임.  
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
리턴되서 사라진 함수에서 정의됬던 지역변수가 사용한 주소 자체가 사라지는 것은 아니고, 컴파일 오류가 나진 않음.  
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

함수 매개변수로 전달한 배열의 sizeof()연산자는 배열 시작위치의 메모리 주소만 전달했음.  
``` c
void print_scores(int scores[], int scores2[5])
{
    size_t size = sizeof(scores);  /* 4 반환 */
    size_t size = sizeof(scores2);  /* 4 반환 */
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

궂이 주소에 자료형 크기만큼 아니고 1 단위로 제어하고 싶으면 (char*)로 casting 하여 더하면 됨.  

int* ptr1 = nums + 3;  /* ptr1는 nums[3]을 가리킴 */
int* ptr2 = &nums[3];  /* ptr2는 nums[3]을 가리킴 */
int* ptr3 = nums + 4;  /* nums[0]의 주소는 0x100 일 때 ptr3 은 Ox116이 아니라 Ox110이다... 16진수니까 */
int* ptr2 = &nums[0] - 1;  /* 0xFC */
```
![image](https://user-images.githubusercontent.com/15919242/219953703-7e6b1e63-5a04-450c-a765-1c6fe6e01ee6.png)  

빅 엔디언 방식은 낮은 주소에 데이터의 높은 바이트(MSB, Most Significant Bit)부터 저장하는 방식  
리틀 엔디언 방식은 낮은 주소에 데이터의 낮은 바이트(LSB, Least Significant Bit)부터 저장하는 방식  

<br>

두 주소 간의 사칙연산
뺄셈 말고는 모두 지원 안함. 의미가 이상하기 때문.  
뺄셈은 두 주소 사이에 들어갈 수 있는 데이터 수를 반환.  
포인터가 아니라 정수를반환. 자동으로 주소 거리(바이트 단위)를 자료형 크기 만큼 나눠서 반환함.  

<br>
배열 요소에 포인터로 접근하기.  
배열명은 시작 주소이므로, 포인터 변수에 대입 가능하다고 했음. 
배열의 첨자 연산자([])도 포인터에 쓸 수 있음. 

``` 
printf("%d, %d, %d\n", nums[1], ptr[1], *(ptr + 1)); 
출력값 모두다 같음.
연속되는 메모리의 시작에서 한 칸 건너뛰어서 두번째를 보여줘.
```

C에서 주소얻는 방법은 &연산자, 배열의 이름으로 배열 시작 주소 가져오기 이것들 단 두가지 !!!  

딱 한 바이트만 옮기고 싶으면 한 바이트짜리 포인터로 캐스팅.  
``` c
int_ptr = (char*)int_ptr + 1;
/* char 형 크기만큼 1을 더하라는 뜻. */ ```  
어떤 포인터 형도 크기는 같다. 4바이트. 다만, 실제 그 주소로 가서 데이터를 몇 바이트씩으로 읽어야 하는지가 바뀌는 것.  

```
![image](https://user-images.githubusercontent.com/15919242/219954891-368f86d1-361b-4b43-a659-330bcc122dc0.png)  
![image](https://user-images.githubusercontent.com/15919242/219954992-b7b91654-02cd-413d-b8b4-31f351d1eafb.png)  
``` C
#include <stdio.h>

int main(void)
{
    int arr[5] = { 5, 10, 15, 20, 25 };
    int* ptr = arr + 2;

    arr = ptr + 1;
    printf("%d %d", *arr, *ptr);

    return 0;
    /* 배열에 메모리 주소를 저장할 수 없으므로 컴파일 오류 */
}
```

포인터 연산자와 우선순위 및 결합 법칙  
![image](https://user-images.githubusercontent.com/15919242/219955508-5b68a372-1f7c-4f79-baa8-3adbfc0638fa.png)  


1순위 후위연산 : 연산자 결합 법칙 ->, 2순위 전위연산, * : 연산자 겹합 법칙 <-  
``` C
int num = *p++;  : p++먼저 * 나중에 : p값에 *로 접근, num에 대입 나중에 p에 값 더함.  
*++p; 는 *랑 ++는 같은 순위인데 연산자 결합 법칙에 따라 오른족에서 왼쪽임. *(++p); 랑 같음.  
++*p는 p주소에 있는 값 접근, 값 + 1해줌.  
(*p)++ 는 p주소에 있는 값에 접근, num에 그 값 대입, 그다음 p값 1증가.  
괄호 써주면 초보자 배려 됨...  

int nums[] = { 134, 68, 47956 };
int* p = nums; /* 변수 nums의 주소가 0x104라 가정 */
int num = *p++;  /* num: 134, p: 0x108 */
```  


조금 더 빠른 배열 요소 더하기 함수.  
``` c
int sum(int* start, int* end)
{
    int result = 0;
    int* p = start;
    
    while (p < end) {
        result += *P++;
    }
    
    return result
}

/* 메인 함수 */
int num[] = {10, 20, 30, 40, 50};
int result = sum(nums, nums + 5);

/* 배열은 첫 주소 + 요소 위치까지의 오프셋 만큼 데이터타입 크기에 곱해서 주소 확정하고
 원하는 원소에 접근함
 
포인터는 다음 주소를 확정할 때 오프셋 곱하는것 없이 상수로 고정. 먼저 이동.
포인터 변수 주소값이 가 있으므로 바로 참조*/
```  

## 포인터와 const
1. 메모리 주소 보호 const  
int* const p = &num;  
"p is a const pointer to int"  
const가 아닌 변수에 대입은 가능  
const포인터가 가리키는 대상의 값은 변경 가능  

2. 값을 보호하는 const  
```c
const int* p = &num1;  /* 코딩 표준. 이렇게 쓰는 사람이 더 많대 */
int const * p = &num1;   
```
다른 주소를 가리킬 수 있고, 가리키는 주소에 있는 값은 못바꿈.  

오른쪽에서 왼쪽으로 읽으면 이해하기 쉽다.  
![image](https://user-images.githubusercontent.com/15919242/212917960-10362b2d-c2a0-412a-9cd9-5a72861eb4d6.png)  

개념 주의 !!  
![image](https://user-images.githubusercontent.com/15919242/219956306-ce0d2b0f-d7ea-4513-af5c-e8e8607344ce.png)  


포인터의 용도
1. 큰 데이터를 매개변수로 할 때 주소만 전달할 때  
2. 반환 값이 둘 이상일 때 return으로는 안되니까 포인터를 사용해서 함수 안에서 원본을 직접 변경.  
3. 동적 메모리 할당 (나중에 배움). 힙 메모리 사용시.
4. 데이터 구조 구현할 때. 임베디드 프로그래밍 등에서 하드웨어에 있는 메모리에 직접 접근할 때.  

포인터 배열 : 포인터를 저장하는 배열.  
``` c
int nums1[3] = { 11, 22, 33 };
int nums2[1] = { 90 };
int nums3[4] = { 88, 36, 37 };

int* num_pointers[3];
num_pointers[0] = nums1;  /* 11의 주소 */
num_pointers[1] = nums2;  /* 90의 주소 */
num_pointers[2] = nums3;  /* 88의 주소 */
```

2차원 배열은 어차피 한덩어리 메모리라 주솟값이 저장된 곳이 맨 앞에 한 곳 뿐.  
``` c
void do_magic(int matrix[][10], size_t m)  /* 10은 열의 갯수를 알려줌. */
{
    /* 10을 알려줘야만 matrix[1][]할 때 몇 개를 (몇개 열을) 건너 뛰어야 하는지 알게됨. 
    컴파일러가 알아서 인식해줌.
    행 수는 따로 전달을 받아야 함 여기 예에선 m으로. */
}
==============
3x5 이차원 행렬의 경우
printf("nums[0] address: %p\n", (void*)nums[0]);  /* 1행 시작 주소 */
printf("nums[1] address: %p\n", (void*)nums[1]);  /* 2행 시작 주소 */
printf("nums[2] address: %p\n", (void*)nums[2]);  /* 3행 시작 주소 */

printf("nums[2]'s offset from nums[0]: %d\n", nums[2] - nums[0]);  /* 10 */
printf("nums[1]'s offset from nums[0]: %d\n", nums[1] - nums[0]);  /* 5 */

printf("nums2[2]'s offset from nums2[0]: %d\n", &nums2[2] - &nums2[0]);  /* 2 */
printf("nums2[1]'s offset from nums2[0]: %d\n", &nums2[1] - &nums2[0]);  /* 1 */

/* 포인터의 사칙연산에서 주소끼리 뺄셈하면 데이터 크기만큼 나눠서 자동으로 반환됨 !!!!!!! */
```
