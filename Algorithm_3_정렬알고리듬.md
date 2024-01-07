# 정렬 알고리듬
정렬 알고리듬의 안정성
똑같은 키를 가진 데이터 순서가 바뀌는지 여부!  
어떤 알고리듬은 안정성 보장하고 어떤건 안하니 조심해야함! 버그 고치기 힘들어질 수 있음  

참고용으로 보기:  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c583b4b2-25e8-45a1-8494-f63d9d2083e7)  
병합 정렬의 경우 힙메모리먹어서 느림, 퀵은 스택메모리먹어서 빠름.  


* 상황에 따른 정렬 알고리듬 선택!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/78d0afe7-cdc3-4717-9fc1-d3733e51a50c)  

## 버블 정렬
버블정렬은 숨쉬듯 코드 작성할 수 있어야함!  
이웃 요소 둘을 비교해서 올바른 순서로 고치는 과정을 반복.  
한번 목록을 순회할 때마다 가장 큰 값이 제일 위로 올라감.  
기포가 수면 위로 떠오르는 모습을 닮았다고 해서 버블정렬.  
큰 기포일수록 수면 위로 빨리 떠오름.  
값이 같으면 그대로 둠.  

시간 복잡도  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/734d5f9d-ecfe-4907-b53d-bf203e93ce80)  

공간 복잡도  
O(1). 새로 추가한 배열 없음!  

안정성 있음!  
``` java
// public static void bubbleSort(int[] nums)
for (int i = 0; i < nums.size(); ++i) {
    for (int j = 0; j < nums.size() - i - 1; ++j) {
        if (nums[j] > nums[j + 1]) {
            int tmp = nums[j + 1];
            nums[j + 1] = nums[j];
            nums[j] = tmp;
        }
    }
}
```

## 선택 정렬
시간/공간 복잡도 : 버블정렬과 동일, 안정성 보장 "안"됨!  
``` java
// public static void selectiveSort(int[] nums)
for (int i = 0; i < nums.size(); ++i) {
    int minIdx = i;
    for (int j = 0; j < nums.size() - i - 1; ++j) {
        if (min > nums[j + 1]) {
            minIdx = j + 1;
        }
    }
    int tmp = nums[minIdx];
    nums[minIdx] = i;
    nums[i] = tmp;
}
```

## 삽입정렬
시간/공간 복잡도 : 버블정렬과 동일, 안정성 보장됨!  
현재 위치의 요소를 뽑음.  
이걸 과거 방문한 요소들 중에 어디 사이에 넣어야 정렬이 유지되는지 판단.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/330521ee-7b42-4cea-bcdb-7130358716da)  
그 위치에 swap, 맨 처음요소까지 swap 반복해야 할수도 있음.  

``` java
for (int i = 0; i < nums.size(); ++i) {
    j = i - 1;
    while(j >= 0) {
        if (nums[j] < nums[j + 1]) {
            int tmp = nums[j + 1];
            nums[j + 1] = nums[j];
            nums[j] = tmp;
        } else {
            break;
        }
        --j;
    }
}
```

## 퀵 정렬
언제라도 설명할 수 있어야 함!
실무에서 가장 많이 사용하는 정렬.  
진정한 분할 정복 알고리듬. 모든 요소를 방문하므로 decrease-and-conquer과 차이는 있음.  
어떤 값(pivot)을 기준으로 목록을 하위목록으로 2개로 나눔.  
- 목록 나누는 기준은 pivot보다 작냐/크냐  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/4f0221e1-ee8e-4f41-88c1-bfdac68a84df)  
pivot은 배열의 맨 오른쪽 값을 기준으로 한다 가정하자.  
left포인터는 배열 맨 왼쪽을 가리키며 시작함  
이후로 처음값 부터 순차적으로 훑으며 pivot보다 큰지 작은지 확인.  
작으면 pivot값이 아니라 left포인터가 가리키는 값과 swap하고, 좌포인터를 1칸 오른쪽으로 이동함.   
pivot보다 크면 아무것도 안하고 넘김.  
다 훑었으면, left위치의 값과 pivot위치 값을 swap하고 pivot위치 값 fix  
- 이 과정을 재귀적으로 반복
  left위치 왼쪽은 pivot보다 작은 아이들만 있고,  
  left위치나 오른쪽은 pivot보다 큰 아이들만 있어서  
  pivot의 최종위치는 찾을 수 있게 됨! swap해서!  
- 재귀 단계가 깊어질 때마다 새로운 pivot값을 뽑음
- 안정성 보장 안됨

* 퀵 정렬 코드
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e490ede9-2ba6-40c4-a5ea-2556232827ce)  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/8bfe660d-c75a-4bf2-be55-f8b50e5824f8)  
``` java
int i = left;

for(int j = left; j < right; ++j) {
   if(nums[j] < pivot) {
      swap(nums, i, j)
      ++i;
      }
}

int pivotPos = i;
swap(nums, pivotPos, right);

return pivotPos;
```
사진 속 코드 말고 아래처럼 인덱싱하고 순서 살짝 바꿔도 됨. (i에 하나 빼고 말고 차이)

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/6df73a7b-d120-485f-88a2-ef1bdfe15702)  

최악의 상황 피하기? pivot을 왼쪽에서 뽑던 오른쪽에서 뽑던 어디에서 뽑던 최악의 가능성은 있음.  
그럼에도 O(N^2)을 절대 허용할 수 없다면, 다른 정렬법을 써야함!  

우리가 오른쪽에서 기준값을 뽑은 방법이 로무토 (Lomuto) 분할법임.  
왼쪽에서 오른쪽 으로만 진행하는 방식. 보통 가장자리 값을 기준으로 선택할 때 잘 작동.  

왼쪽에서 오른족, 오른쪽에서 왼쪽으로 번갈아 진행하는 방법이 호어 (Hoare) 분할법  
어떤 값을 기준값으로 선택해도 잘 작동함. 궁금하면 찾아보기  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/66122eb3-23a0-4637-9d29-6b8204ee1190)  

코드보기 : 안정성  


## 병합 정렬
정렬된 두 배열 합치기 알고리듬을 응용한 개념  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d490bb2c-2f21-4a0e-876d-ac9ee7cee268)  
정렬된 배열 합치기는 시간 복잡도 O(N), 공간복잡도 O(N)  

1. 원본 배열을 정렬된 여러 배열들로 만듦
단, 원본 배열을 정렬하면 안됨  
2. 그 다음 정렬된 배열들을 아까 본 방법으로 합치면 끝!  
안정성 보장됨!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e7569438-7b07-48dc-b52f-a1a85ee8bdb0)  


## 힙 정렬
안정성 보장 안됨!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/9d96cf46-e2ef-4054-8082-670617fda97a)  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/2a4b6dec-7955-4c33-944d-5fa6d1345d62)  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/75e2199b-5ec2-433f-aa00-8cc2da70c8d1)  
힙 속성에 맞게 제거하다보면 정렬된 새로운 배열이 완성됨 !!  


코드보기 : 배열 요소의 최소 차이 찾기  
정렬이 빈번히 필요하지 않으면 정렬 한번 하고 탐색알고리즘 돌리면 빠르게 찾을 수 있음.  
정렬을 했다면, 정렬된 배열의 각 요소의 이웃과의 차이만 비교하면 되지, 전체 차이를 비교할 필요가 없다는게 핵심!!  
``` java
package academy.pocu.comp3500samples.w03.minimumdiff;

import java.util.Arrays;
import java.util.Random;

public class Program {

    public static void main(String[] args) {
        Random random = new Random(512);

        int[] nums = new int[15];

        for (int i = 0; i < nums.length; ++i) {
            nums[i] = random.nextInt(1000);
        }

        printNums(nums);

        Arrays.sort(nums);

        int minDiff = Integer.MAX_VALUE;
        int num1 = 0;
        int num2 = 0;

        for (int i = 0; i < nums.length - 1; ++i) {
            int diff = Math.abs(nums[i] - nums[i + 1]);

            if (diff < minDiff) {
                minDiff = diff;
                num1 = nums[i];
                num2 = nums[i + 1];
            }
        }

        System.out.println(String.format("minimum difference: %d", minDiff));
        System.out.println(String.format("num1: %d, num2: %d", num1, num2));
    }

    private static void printNums(int[] nums) {
        String[] s = new String[nums.length];

        for (int i = 0; i < nums.length; ++i) {
            s[i] = String.format("%d", nums[i]);
        }

        System.out.println(String.format("[ %s ]", String.join(", ", s)));
    }
}
```

