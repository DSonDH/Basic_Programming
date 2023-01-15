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

