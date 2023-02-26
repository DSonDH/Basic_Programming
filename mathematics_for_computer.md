# 숫자 체계
진법 : 수를 표기하는 방법. 한 자리에 쓸 수 있는 숫자의 수가 몇 개인지 알려줌.

## 10진법
한자리에 사용가능한 숫자가 10개.  
사람에게 익숙한 숫자 체계  
컴퓨터는 전류가 흐르냐 안흐르냐로 판단할 수 있는 2진법 또는 16진법 많이 씀.  
87345 :  
$ 8*10^4 + 7*10^3 + 3*10^2 + 4*10^1 + 5*10^0 $  

9에서 1을 증가시키면, 다음자리수는 1이 되고, 현재 자리수는 최솟값인 0이 됨. (carry-over)  
빼기는 윗자리수를 하나 내리고, 현재 자리수를 최댓값으로. (borrowing)  

## 2진법
0, 1을 사용해서 수를 표현하는 방법.  
![image](https://user-images.githubusercontent.com/15919242/214197138-d9ea158e-da31-41b0-a5d5-1a5b57e409d8.png)

## 8진법
8개의 숫자를 사용해서 수를 표현하는 방법.  

## 16 진법
16개의 숫자를 사용해서 수를 표현하는 방법.  
0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F  

Hexa decimal 의 x 를 따와서 0x로 표현  
![image](https://user-images.githubusercontent.com/15919242/214197929-1ce64918-eae1-485d-93f4-4057f658d3f3.png)

2진수 <-> 8진수 변환 : 2진수 3자리 씩 끊어서 8진수로 바꾸면 됨.  
2진수 <-> 16진수 변환 : 2진수 4자리 씩 끊어서 16진수로 바꾸면 됨.  
2진수는 너무 길어서 가독성 때문에 16진수 많이 씀.  
ex : RGB 흰색 : 빨강255, 초록255, 파랑255 : #FF,FF,FF  

<br>
<br>

# Bit, Byte
## 컴퓨터 구성요소
transistor (반도체 소자)  
표현가능한 상태는 단 두 개 뿐  
전류가 흐르지 않는다 : 0  
전류가 흐른다 : 1  
하나의 트랜지스터의 상태를 기록하는 최소 단위를 비트라고 부름.  
2진법/2진수 가 딱임.  
$$2^n 
$$

저장 단위는 1byte로 함.
한 입 베어 문 조각. bite에서 byte로 바뀜.  
8비트.  1byte = 8bit. (8b = 1B)  
8비트로 16진수 두 자리씩 정확히 표현할 수 있으므로 컴퓨터공학에서 가장 많이 씀.  
![image](https://user-images.githubusercontent.com/15919242/214203813-1d90954f-04a0-47ce-b237-3a51c5c27ead.png)
컴퓨터에서 1K는 1000이 아니라 1024임.  
![image](https://user-images.githubusercontent.com/15919242/214204337-5e1d486f-820c-4356-96da-642a10637bbf.png)
<br>
<br>


# 컴퓨터의 정수 표현법
양의 정수 : unsigned  
비트를 몇 개 사용하느냐에 따라 표현 가능한 수의 갯수가 결점됨.  
8비트 쓰면 0부터 255까지 표현할 수 있음.  
16비트 쓰면 0부터 65535까지 표현할 수 있음.  

* overflow  
11111111(2) + 1(2) = 100000000(2) 은 표현 가능한 비트범위를 넘어서므로 0으로 처리됨.  
연산 결과가 최댓값보다 커질 때 overflow가 발생한다고 함. 자릿수 넘은 1은 버림.  
표현가능 최댓값 보다 클 경우 최솟값으로 돌아간다 ! 도돌이표처럼.  
0보다 작음을 표현하려다가 65535와 비교하게 될 수 있음.  


음의 정수 : signed  
컴퓨터는 0과 1밖에 모르므로 마이너스 기호를 표현하기 위해선 다른 방법이 필요함.  
8비트 안에서, 맨 위 비트는 양수면 0, 음수면 1로 표현하고 나머지 7비트로 절댓값을 표현한다.  
표현 가능한 절댓값 범위가 반토막남. (-127 ~ 127)  
![image](https://user-images.githubusercontent.com/15919242/214243448-812cb2fd-2730-42a3-901b-9116e0418e56.png)

근데 .. 00000000(2) 이랑 1000000(2) 둘 다 0을 표현하므로 낭비임.  
10000000(2) + 00000001(2) = -2 ??? 이상하게 됨.  
컴퓨터는 사칙연산 중에 덧셈만 할 줄 암 ...  암튼 덧셈만 함.  
이를 해결하기 위해 보수를 도입함.  

## 보수 (complement) 
N진법에는 두 가지 보수가 있음.  N의 보수, N-1의 보수
N의 보수 : N진법 수 중 다음 자릿수가 되기 위해 필요한 값.  
  
9의 보수 : 각 자릿수를 9로 만들기 위한 수.  
10의 보수는 9의 보수를 구한 다음 1을 더하면 됨. 9의 보수는 계산하기 쉬우니까  
  
보수와 뺄셈  
![image](https://user-images.githubusercontent.com/15919242/214245989-63a135a0-4075-47f7-84c6-f759af528804.png)
오버플로우를 이용해서 뺄셈 함.  
0012 - 0003 할 때 0003의 10의 보수를 누군가 계산 해주면 그 보수랑 0012랑 더해서 오버플로는 없애서 빼기연산 가능.  
![image](https://user-images.githubusercontent.com/15919242/214249712-df63e5d7-fe20-4525-9ed7-06c0ffccd521.png)

### 1의 보수(one's complement)  
![image](https://user-images.githubusercontent.com/15919242/221391513-46953f76-0dd1-4dc3-8330-dbea2034479c.png)  

1의 보수를 구하는 방법  
![image](https://user-images.githubusercontent.com/15919242/221391546-05ef2591-fb25-4e40-9a71-ca90149b9cc2.png)  

1의 보수의 표현 범위 : 가장 왼쪽 비트가 부호(sign bit)가 됨.  

Quiz 4개
``` C
/* -1(10)을 1의 보수를 이용해서 8비트로 표현하면 ? */
/* >>>  1111 1110(2) */

/* 127(10)을 1의 보수를 이용해서 8비트로 표현하면 ? */
/* >>>  0111 1111(2) */

/* 1의 보수를 이용해서 8비트로 1010 1010(2)인 값은 10진수로 몇 ? */
/* >>>  -85(10) */

/* 1의 보수를 이용해서 8비트로 0101 0111(2)인 값은 10진수로 몇 ? */
/* >>>  86(10) */
```    

1의 보수의 장점 : 간단히 뺄셈 가능.  
한계점 : 0이 두개임.  
뺄셈 할 때 따로 +1 해줘야 하는 예외상황이 생김.  
![image](https://user-images.githubusercontent.com/15919242/221409356-25ecaa55-0114-45d0-8bd1-f79a09a8e03d.png)  
이를 2의 보수로 해결할 수 있음 !!

### 2의 보수(two's complement)  
현재 부호 있는 정수를 표현하는 가장 흔한 방법.  
![image](https://user-images.githubusercontent.com/15919242/221409423-29eae377-689d-4975-bc44-a34ab038db51.png)  
가장 왼쪽 비트가 부호를 나타냄.  
2^(n-1) -1 ~ -2^(n-1)
![image](https://user-images.githubusercontent.com/15919242/221409471-e898dfad-0405-490d-9904-4460d964e752.png)  

장점 : 음수 하나 더 많이 표현함. 따로 +1을 처리하는 예외도 없음.  
오늘날 음수를 표현할 때 가장 많이  방법.  
![image](https://user-images.githubusercontent.com/15919242/221409805-a5d133c5-4b7a-475a-a723-01afa09447ba.png)
![image](https://user-images.githubusercontent.com/15919242/221409833-01adb24b-65ed-46cd-b7d9-201410bf3093.png)
![image](https://user-images.githubusercontent.com/15919242/221409868-db441546-5300-4045-b4c3-00d4c92674ff.png)  
![image](https://user-images.githubusercontent.com/15919242/221409876-fb791a48-677b-4455-ad57-1654463c9bf6.png)
표현 가능 한 부호의 범위를 벗어나지 않게 조심해야함 !!  
최댓값 보다 큰 값이 결과로 나올 경우 오버플로가 발생한 것,  
최솟값 보다 작은 값이 결과로 나올 경우 언더플로가 발생했다고 함.  

![image](https://user-images.githubusercontent.com/15919242/221410154-1742c49f-ec5b-470b-82be-04363c7debe3.png)  
![image](https://user-images.githubusercontent.com/15919242/221410161-e87d392f-bb1f-46e8-9311-f970fca001bc.png)  

### 2진수의 곱셈  
bit shift 와 같음.  
1101(2) X 10(2) = 11010(2)  
1001(2) X 101(2) = 1001(2) x 100(2) + 1001(2) x 1(2)  
음수가 있으면 양수로 바꾸고 계산.  

### 2진수의 곱셈  
bit shift 와 같음.  
1100(2) / 10(2) = 110(2)  
![image](https://user-images.githubusercontent.com/15919242/221411719-b05fea58-f67b-4a06-bbfd-4bd07e7341c7.png)  


Quiz 4개
``` C
/* 1010(2) * 1100(2) (부호없음) ? */
/* >>>  111 1000(2) */

/* 1001(2) * 1011(2) (부호 있음. 2의 보수 사용) ? */
/* >>>  010 0011(2) */

/* 1111(2) / 0011(2) (부호없음) ? */
/* >>>  0101(2) */

/* 1100(2) / 1110(2) (부호 있음. 2의 보수 사용) ? */
/* >>>  0010(2) */
```   

* 정수는 정확히 수를 표현한다.  
부동소수점은 정확히 표현하지 못하고 근사치로 표현하게되는 경우가 있음.  


# 컴퓨터의 문자 표현법 (ASCII)  
American Standard Code for Information Interchange (ASCII)  
65 : A  
97 : a  
숫자, 영어 알파벳, 특수문자 및 공백, 제어문자(화면 출력은 불가능) 표현 가능  
65 + 1 하면 B가 출력 됨. 1관 '1'은 비트패턴이 다름.  

ASNI, 멀티바이트, 유니코드  
ANSI : MS Windows에서 라틴문자 기반의 언어를 표현하기 위해 만든 문자 인코딩.  
1바이트로 표현 가능.  

멀티바이트 : 아스키코드에 없는 문자들은 2바이트으로 표현.  
Extended Unix Code (EUC) : 한국어, 일본어, 중국어를 위한 멀티바이트 문자 인코딩.  
EUC-KR, EUC-CN, EUC-JP 같이 이름 붙음.  

유니코드  
멀티바이트의 한계로, 여러 언어를 한번에 표현 못했음.  
전 세계의 모든 문자 및 이모지까지 일관되게 표현할 수 있는 규격.  
![image](https://user-images.githubusercontent.com/15919242/221413224-a2ceffbe-7556-4982-84d8-125e85d444a5.png)  

유니코드 인코딩 종류  
![image](https://user-images.githubusercontent.com/15919242/221413308-a850c53f-5d98-4c75-a143-eb93e18a4a1d.png)  

요즘은 UTF-8만 쓴다.  
![image](https://user-images.githubusercontent.com/15919242/221413420-660775ac-8150-4d82-8046-099146d024b2.png)  
![image](https://user-images.githubusercontent.com/15919242/221413473-b3f7273a-daee-47c3-9eee-61ad69203c70.png)  

* 리틀 엔디언, 빅 엔디언  
![image](https://user-images.githubusercontent.com/15919242/221413497-9ec9d689-9142-48e3-ad37-91009cef5268.png)  

UTF-8의 장점  
거의 모든 문자에 1바이트 또는 3바이트를 사용.  
한국어는 대부분 3바이트 필요.  

예시)  
![image](https://user-images.githubusercontent.com/15919242/221413813-3c6f0ad2-bc6b-4b7a-9445-86aececb82fa.png)  


UTF-16  
![image](https://user-images.githubusercontent.com/15919242/221413912-4e5af546-3d06-4f76-be55-f14ef610498f.png)  

UTF-32  
![image](https://user-images.githubusercontent.com/15919242/221413924-5b533e21-99c9-4c18-b3d7-f85fc641d252.png)  


# 컴퓨터의 실수 (Real number)   
