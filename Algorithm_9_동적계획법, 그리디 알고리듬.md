# 동적 계획법(dynamic programming, DP)
특별한 속성을 가진 복잡한 문제를 푸는 방법  
복잡합 문제를 그보다 단순한 하위 문제로 나눠서 풂  
재귀적  
가잔 단순한 문제 +1은 그 다음으로 단순한 문제  
이걸 반복하면 원래의 복잡한 문제까지 해결  
특별한 속성이 있는 문제만 이 방식으로 풀 수 있다!  

## 주먹구구식 배낭 문제 풀기
knapsack문제: 크기와 가격이 다른 여러 풀건이 있는데, 값어치가 최대가 되도록 물건을 넣고자 함.  
배낭의 크기는 제한이 있음.  
판정 버전은 NP완전 문제.  
최소 어떤 값어치 v만큼 넣을 수 있는가? 판정은 다항식 시간 내로 됨.  
주먹구구식으로 풀면 모든 경우의 수를 따져봐야 함: O(2^n) 시간 복잡도  

## 메모이제이션
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/85d5b8ee-94ae-437a-ae30-2378392a12ae)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/b699e193-29b6-408e-83b5-130068986fa1)  

메모이제이션(memoization)  
계산 결과를 캐시에 저장한 뒤, 나중에 재사용하는 기법  
처음 계산할 때 그 결과를 캐시(배엶)에 저장  
나중에 동일 계산을 다시 하는 대신 저장해둔 값을 가져다 씀.  
값비싼 계산(깊은 재귀 호출)에 적합  
최적화 기법 중하나, 캐싱 기법 중 하나  
메모이제이션은 보통 함수가 매개변수에 따라 반화하는 값을 캐싱하는 것을 말함.  
컴퓨터 프로그래밍에서만 사용하는 용어임.  

* 메모이제이션을 사용한 피보나치 함수
색인으로 가장 빠르게 사용하는 배열을 사용하는 게 좋다.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/7f49faad-5992-4e98-9f96-1c0878dffd97)  

동적계획봅과 메모이제이션은 전혀 다른 개념임!  
메모이제이션: 실행된 결과를 기억해뒀다가 재사용하는 최적화 기법  
동적 계획법: 복잡한 문제를 하위 문제로 쪼개서 재귀적으로 푸는 방법  
동적 계획법에서 메모이제이션을 흔히 써서 같은 것 같지만,  
메모이제이션이 동적 계획법에 필수가 아니고 다른 곳에서도 메모이제이션을 쓰므로, 엄연히 다른 개념.  

top-down 동적 계획법  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/19dd9a5e-6537-482f-b882-ce9295b05938)  

## 타뷸레이션
최적의 피보나치 평가 순서가 있음!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/9dbaeb2b-b9ed-4ecd-a8e2-a44a56235abd)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c163da86-e3bd-42fb-9ca9-ffdacbbceab6)  
타뷸레이션, 다른 말로는 bottom-up 동적 계획법이라 함  
가장 작은 문제(리프)부터 시작  
순서대로 그보다 하나 더 큰 문제를 풀어나감  
필요하지 않은 하위 문제도 평가할 수 있음.  
문제를 잘 분석해서 최적의 순서를 찾아야 함.  
top-down 방식보다 보통 더 빠름  
CPU 캐시에 좀 더 친화적  
재귀 함수 호출을 피할 수 있음  
모든 하위 문제를 평가할 필요가 없는 경우에는 예외  

* 메모이제이션/타뷸레이션은 속도 향상을 위한 기법
* 그걸 위해 메모리를 더 사용함
* 이처럼, 시간 복잡도와 공간 복잡도는 반비례인 관계가 꽤 있음

### 동적 계획법으로 푸는 배낭 문제
작은 배남부터 최적의 해법을 찾아나감  
1칸 배낭 -> 2칸 배낭 -> 3칸 배낭 ...  
4칸배낭의 최적해법 = 1칸 배낭 최적해법 + 3칸 배낭 최적해법 ...  
일단 물품이 하나씩만 있다고 가정함.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/1d532dce-2174-4c9e-aa5c-d21c8a10b9d7)  
물건1에 대해 최적의 결과를 고려함.  
물건2를 추가로 고려할 때 최적 결과를 고려함.  
물건3을 고려할 때는 물건2까지 고려한 최적의 결과를 기초로 판단함.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c040ebe8-4806-4c2d-bc49-b1bc6772d620)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/43ac56dc-cbd7-4aae-98e1-182c291c498d)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e9f83ca7-8e00-4f6c-a727-0a259964c8ce)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/4578572f-7b03-402a-ab94-931e7b930801)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/3c5a734e-3be1-48c7-a1ff-245b5d60af1e)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/b2b23dda-e0ec-4009-b952-a43928565fc9)  

새로운 물건이 추가되는 경우: 2배만큼 계산할게 늘어나지 않음!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/7260abd3-1e37-49a5-91e9-2b5fc651d4e2)  
지금 껏 어떤 물품을 샀는지는 따로 저장하지 않는 한 궂이 알 필요는 없음.  
그냥 최적의 값만 가지고 있으면 되는 알고리즘임.  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/4bb33c18-8093-43de-8b98-bfb16342744e)  
이 방법은 타뷸레이션임. 재귀 + 메모이제이션으로도 풀 수 있음. 구현은 알아서.  

### 동적 계획법을 적용할 수 있는 문제
1. 최적 부분 구조(optimal substructure)
  - 하위 문제의 최적 해법으로 큰 문제의 최적 해법을 구할 수 있음
  - 동적 계획법과 그리디 알고리듬의 유용성 판단에 사용
  - 강화 학습에서 흔히 등장하는 벨만 방정식도 이에 기초
  - ex: 최단 경로 찾기
2. 하위 문제의 반복
  - 똑같은 평가를 반복해야 함 (다다익선!)
  - 하위 문제의 크기가 작아야 함
  - ex: 피보나치 수열

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/0c250604-80cc-43ee-ad86-bedfb4904697)  
예를 들어, 병합 정렬, 퀵 정렬이 동적 계획법이 아닌 이유는, 하위 배열이 반복되지 않고 다른 배열들이기 때문임.  

동적 계획법으로 문제를 푸는 과정  
1. 문제에 동적 계획법을 사용할 수 있는지 판단
2. 상태, 매개변수 결정
3. 상태간 관계 정립
4. 종료조건 결정
5. 메모이제이션 / 타뷸레이션 추가
2~3은 재귀함수 구성과 마찬가지. 1번이 가장 까다로운데, 많은 문제풀이 경험밖에 답이 없더라 ...  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/97c98a64-0761-440a-80fa-8be8bd9ddf63)  

동적 계획법으로 풀 수 있는 문제들:  
- 최단 경로 찾기 (다익스트라 알고리듬)
- 최장 공통부분 문자열
- 와일드카드 패턴 매칭
- 부분집합 합
- 레벤슈타인 거리 (편집 거리)
- 연속 행렬 곱셈
- etc ...

코드보기 : 배낭문제  

### 그리디(greedy)하게 푸는 배낭 문제
greedy algorithm  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/8e2f6d4f-fabe-4301-9b12-38f48579f41c)  

기준에 따라 여러 방법이 가능함.  
1. 가장 비싼 물건부터 훔침
2. 제일 작은 물건부터 훔침
3. 단위 면적당 값어치가 가장 높은 물건부터 훔침
방법에 따라 값이 달라짐  
하지만 꽤 괜찮은 결정을 빨리 내릴 수 있음  
정렬 후 순서대로 훑으면 O(nlogn)으로 결정 가능  

쪼갤 수 있는 배낭 문제  
일부만 취할 수 있는 경우는? fractional 배낭 문제라고 함  
이런 경우는 단위 면적당 값어치가 높은 알고리즘이 그리디 알고리듬이 최적의 해법을 찾음.  

그리디 알고리듬을 사용할 수 있는 경우  
제대로된 해법을 구하는 알고리듬 복잡도가 너무 높은 경우  
적당히 좋은 해법도 상관없는 경우  
동적 계획법을 사용할 수 없는 경우 (중복되는 하위 문제가 없음)  
두가지 특성이 필요함  
1. 최적 부분 구조
2. 그리디 선택 속성: 한 번 내린 결정은 다시 돌아보지 않음
(과거의 선택: 현재 선택에 영향을 미칠 수 있음, 미래의 선택: 현재 선택에 영향을 안 미침)  

팁  
보통 최소/최대화 문제  
여러 그리디 선택이 가능하면 모두 시도 혹은 반례를 통해 제거하기  
정렬을 해야 속도가 빨라질 수도 있음  

동전 교환 문제  
각 동전 종류별로 무제한으로 있는 경우  
1. 동전 배열을 내림차순으로 정렬
2. 가액이 잔액 이하인 가장 큰 동전을 결과에 추가
3. 잔액에서 그 동전 가액을 뺌
4. 잔액이 0이 아니면 2단계로 돌아감
시간복잡도 O(nlogn)  
위 그리기 알고리즘은 일부 동전 체계에서만 최적인 해법임  

인터벌 스케줄링 (Interval Scheduling)  
각 기관별 interval이 가능한 곂치지 않게 가장 많은 개체를 뽑고싶음  
시설들의 점검 시간을 '어떤 순서'대로 고려한 뒤  
이미 털기로 결정한 시설과 곂치지 않은 시설을 차례로 뽑음  
어떤 순서대로 뽑느냐에 따라서 상황이 달라지느데, 종료시간이 이른것부터 고르는게 최적임  

의사코드  
1. 점검 종료 시간이 이른 것이 앞에 오도록 시설 목록을 정렬
2. 이미 뽑은 것과 곂치지 않는 한 순서대로 시설을 뽑음

그리디 접근법으로 풀 수 있는 문제  
- inverval pertitioning
- minimizing lateness
- Dijikstra's shortest path
- 운영체제 job scheduling
- k-center problem
- decision tree learing
- Huffman coding
- etc ...

## 압축 알고리듬
데이터 압축: 원본 데이터보다 적은 비트 수록 정보를 표현하는 방법  
저장공간 절약, 전송속도 단축!  

몇 가지 압축 알고리듬 및 파일 포맷  
ZIP, RLE(Run-Length Encoding), JPEG, MP3  
zip, rle는 무손실, jpeg, mp3는 손실  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/6c616b95-158f-4004-a316-9094eee1fdc0)  

### 양자화(quantization)
원본에서 비슷한 값들을 합쳐 값의 갯수를 줄이는 방법  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/52e5a047-a335-4dd2-8ee4-a294cf6b8678)  
반올림으로 그나마 오차 적도록 함.  
jpeg에서는 이미지를 주파수 도메인으로 바꾸고, 주파수 도메인에서 양자화 하여 복원:  
용량 줄고 이미지는 비슷하게 보이고 그럼!  
DXT1 이미지는 4x4블록마다 16비트 RGB 5:6:5색상 둘을 사용 (green이 사람이 좀 더 민감해서 가중치 높임)  
보간(interpolation)  

전송 데이터 비트 수 줄이기  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/90512c81-16ee-407f-bb81-137a697c911f)  
원래는 문자10개니까 80비트 필요한데, 더 줄이고 싶음  
백과사전급의 많은 string을 느린 네트워크로 보내고 싶은 게 문제임  

### 허프만 코딩 (Huffman coding)
입력 문자들에 적합한 가변 부포(code)를 선택하는 알고리듬  
최적 접두어 코드(optimal prefix code)를 사용  
헷갈리지 않고 각 코드를 제대로 된 문자로 디코딩 가능  
어떤 문자에 할당된 코드는 다른 문자에 할당된 코드의 접두어가 아님  

허프만 코딩은 그리디임!  
문자마다 사용하는 코드의 비트 수가 다를 수 있음  
비트 수를 최소화하는 방법은 자주 나오는 문자에 적은 비트 수를 줌  
위 과정을 허프만 트리로 구현함!  

허프만 트리 (Huffman tree)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/7d5d3b10-1017-4add-8b3c-3271fbe59d60)  
동그란 노드 내부 숫자는 빈도  
네모 노드가 리프 노드  

허프만 트리 만들기  
빈도 내림차순으로 문자 정렬  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/4453cacb-4d1a-463d-b6ab-2ea63ffaa3af)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/9812973b-0197-4be8-852c-4cda1fb30ad0)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/a155e1d2-6791-4b5e-84f7-b6e0fb033c2b)  
루트노드 부터 각 문자가 있는 leaf를 찾아가면서 만나는 0 또는 1패턴으로 테이블을 완성함  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/15a78a80-1a0a-4f55-ae74-9bc009ca104e)  
그리디 알고리즘이므로 최적의 압축률을 보장하지는 않음!  

허프만 디코딩  
인코딩 된 메시지의 비트를 순서대로 고려  
1. 트리에서 비트 값과 일치하는 변(edge)를 따라감
2. 리프 노드에 도달하지 않았다면 1로 돌아감
3. 리프 노드에 있는 문자를 출력 후 루트 노드로 복귀
4. 모든 비트를 읽지 않았다면 1로 돌아감
전제조건: 인코딩에 사용한 허프만 트리를 알고 있음!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/11c46149-165b-4e3b-9e25-0ab26012b17d)  

디코더에 허프만 트리 전달방법: 문자 빈도 표로 보내거나 허프만 트리를 같이 보내거나.  
