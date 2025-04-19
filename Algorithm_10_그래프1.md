# 그래프  

## 그래프의 정의: 데이터들의 관계를 잘 정리하는 방법 중 하나.  
데이터들과 그 관계를 보여주는 방법 중 하나!  
서로 연관 있는 노드의 집합.  
G = (N, E)  (Node, Edge)  
노드 (Node, Vertex): 한 개체를 나타냄  
엣지 (Edge, link): 두 노드(개체)간의 관계를 나타냄  
차수 (degree): 한 노드에 연결된 엣지 갯수  
루프 (loop): 노드 자신으로 돌아오는 엣지

네트워크 형태의 관계를 보여주기에 적합,  
복잡한 실세계의 문제를 모델링하기에 적절함.  
- 네트워크 형태가 명백하게 안 보이는 경우도 있음
- 그래프 이론을 적절히 적용하면 시간 복잡도를 확 줄일 수 있음

그래프의 예: 서울 지하철 노선표, POCU 선수과목, SNS친구들 간의 관계 (네트워크), 라면 끓이는 레시피, 게임 스킬트리 등등  
트리는 directed acyclic graph (DAG)임!  
그래프의 종류: 
directed / undirected graph  
방향 그래프 : 변이 한 방향만 가리킴. 일방통행만 가능  
무뱡향 그래프 : 변에 특별한 방향이 없음. 양방통행 가능 
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/9f9c05f4-aa3f-4244-8c26-a7d5525dc8e7)  


cyclic / acyclic graph  
cyclic: 그래프 안의 모든 노드에 대해 일단 떠나면 그 노드로 돌아오는 경로 없음.  
acyclic: 하나의 노드라도 떠난 뒤 그 노드로 돌아오는 경로가 있는 경우.  


weighted / unweighted graph  
가중 그래프: 각 변의 관계 정도(값)이 다름, 별도의 표기 필요할지도.  
비가중 그래프: 모든 변이 동일한 의미를 가짐, 값이 같음, 별도의 표기 불필요.  

그래프로 풀 수 있는 문제들 예시:  
- 여러 스케줄링 관련
- 두 위치 사이 여행 경로 관련
- 분자를 구성하는 원자들의 결합 관련
- 인터넷에서 데이터 패킷이 전달되는 경로 관련
- 대규모 프로젝트에서 일감 사이의 의존성 관련
- 도시 전기 공급 그리드 관련
- SNS에서 친구 관계 관련

그래프의 다양한 표현 방법:
원과 선 그림 / adjacency matrix / adjacency list  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/b98afd59-fdc4-4299-83d5-6343181dcdd3)  

인접 행렬  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/57644127-be2f-4527-8f7e-fcad75c1ee26)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/2f16b186-96d2-4929-acd5-1bbe43650aff)  
행 의미: 내가 누구를 가리키는지 정보  
열 의미: 누가 나를 가리키는지 정보  
undirected graph는 인접행렬이 symmetric함  

인접 행렬의 장단점  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/289820e1-655e-41b6-9c15-1965716438d6)  

인접 리스트  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/bc760c7a-b870-4b49-b94a-030de9eb9739)  

A -> B -> C 연결이라는게 아니고 A가 B랑 C랑 연결되어있다는 걸 의미함.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/16f1c913-80ec-4c10-8b18-774af4c1a7e7)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/264c2522-4017-47b3-83b7-d8ec6ee6bb0c)  

그 외에 indicence matrix, incidence list를 사용하기도 함. 궁금하면 직접 찾아보기.  

## 그래프의 깊이 우선 탐색 (Depth First Search)
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/743d8a62-7f30-4195-b406-499c1e009948)  
무한루프 돌면서 stackoverflow 발생하는 경우  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/97d5c4f4-d0cd-478a-91d7-f3fa62090ffa)  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/6e5cbce0-eebb-4d16-8c1b-a43564f51059)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/8a68f70b-0ecf-4437-9bbb-39c2242f0ec9)  
C가 두번 출력됨! 뭔가 잘못됨 ㅠㅠ  

올바른 노드 기억법!!  
1. 스택에 이미 들어간 노드는 다시 안 넣음
2. 스택에서 pop()을 한 후에 이미 방문했던 노드인지 확인
1번이 조금 더 효율적임.  
이른바 발견한 노드 기억하기! stack에 넣는 순간 발견했다고 체크하기  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/8eb433a2-256d-4a4e-9983-c3f6323ed6f6)  

방향 그래프에서도 작동할까?  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/ead5431b-8e7b-4b23-95bc-e62ef3c4e2fc)  
아니, B를 탐색 못함!  

## 후위 순회 (DFS)
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/af13b167-2629-443e-87a5-cf1434406aa4)  

QnA: 정용훈님  
각 노드마다 방문했는지 여부를 기억하는걸 true false로 하지 않고 변수 하나를 두고  
해당값을 +1씩 해가면서 해당 값일경우를 true로 판단하고 아닐경우  
오버플로우시 버그가 발생할 수 있기 때문에 false일경우는 그 값 -1로 바꿔가면서  
판단하면 시작하기전에 각 노드를 한번 순회를 안해도 되겠군요!  

그래프 DFS의 시간 복잡도  
O(N+E)  
각 노드는 최대 한 번 처리됨: O(N)  
각 변은 최대 두 번 고려됨 : O(E)  

### 위상 정렬
topological sort  
그래프의 노드를 선형 (일직선)으로 정렬하는 방법  
우선순위가 바뀌지 않음  
(예: B노드를 가리키던 모든 노드들이 B 보다 전에 나옴)  
DAG만 유효한 위상 정렬이 가능  
순환하는 노드가 있다면 우선순위 판단이 불가능!  
시작점이 존재해야 함  
해답이 여럿일 수 있음!  

(참고) 위상 정렬 알고리듬  
몇 가지 알고리듬이 존재!  
깊이 우선 탐색(DFS), 칸 알고리듬 (Kahn's algorithm)  
실제로 위상 정렬을 함  
위상 정렬 가능한 그래프인지 판단  

(참고) DFS를 사용한 위상 정렬  
전위 순회? 후위 순회? 전위 순회는 말이 안됨!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/1855f56c-550c-4b59-a2a2-1bd81ade838e)  
후위 순회는 역순으로 따라하면 됨!  
13번 부터 첫 순서대로! (stack을 쓰던, linked-list를 쓰던)  

위상 정렬의 용도  
관계에서 순서를 정하는 매우 많은 곳에서 사용 가능  
프로젝트 일정 만들기  
CPU 명령어 실행 순서 결정  
스프레드 시트 셀 평가 순서 결정  
컴파일 순서 결정  
DB테이블 로딩 순서 결정  
선수 순위 결정  
(대부분 누군가 미리 만들어 놓은 함수들을 우리가 쓰던것들임)  

코드보기: POCU 수강 순서  
``` java
// Course.java
package academy.pocu.comp3500samples.w11.topologicalsort;

import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public final class Course {
    private final String title;
    private final ArrayList<Course> nextCourses = new ArrayList<>();

    public Course(final String title) {
        this.title = title;
    }

    public String getTitle() {
        return this.title;
    }

    public List<Course> getNextCourses() {
        return Collections.unmodifiableList(this.nextCourses);
    }

    public void addNext(final Course course) {
        this.nextCourses.add(course);
    }
}

// Program.java
package academy.pocu.comp3500samples.w11.topologicalsort;

import java.util.ArrayList;
import java.util.Collections;
import java.util.HashSet;
import java.util.LinkedList;

public class Program {
    public static void main(String[] args) {
        ArrayList<Course> courses = createCourseGraph();

        LinkedList<Course> sortedCourses = sortTopologically(courses);

        for (Course course : sortedCourses) {
            System.out.println(course.getTitle());
        }

        System.out.println("=======================================");

        Collections.shuffle(courses);

        sortedCourses = sortTopologically(courses);

        for (Course course : sortedCourses) {
            System.out.println(course.getTitle());
        }
    }

    private static LinkedList<Course> sortTopologically(ArrayList<Course> courses) {
        HashSet<Course> discovered = new HashSet<>();
        LinkedList<Course> sortedList = new LinkedList<>();

        for (Course course : courses) {
            if (discovered.contains(course)) {
                continue;
            }

            topologicalSortRecursive(course,
                    discovered,
                    sortedList);
        }

        return sortedList;
    }

    private static void topologicalSortRecursive(Course course, HashSet<Course> discovered, LinkedList<Course> linkedList) {
        discovered.add(course);

        for (Course nextCourse : course.getNextCourses()) {
            if (discovered.contains(nextCourse)) {
                continue;
            }

            topologicalSortRecursive(nextCourse,
                    discovered,
                    linkedList);
        }

        linkedList.addFirst(course);
    }

    private static ArrayList<Course> createCourseGraph() {
        final Course comp0000 = new Course("0000: Intro to Programming for Novices and Hobbyists (C#)");
        final Course comp1500 = new Course("1500: Intro to Professional Programming with C#");
        final Course comp1000 = new Course("1000: Math for Software Engineers");
        final Course comp1600 = new Course("1600: Visual Programming with C#");
        final Course comp2200 = new Course("2200: Unmanaged Programming with C");
        final Course comp2500 = new Course("2500: Object Oriented Programming and Design with Java");
        final Course comp4700 = new Course("4700: Database Programming with C#");
        final Course comp2300 = new Course("2300: Assembly");
        final Course comp3200 = new Course("3200: Unmanaged Programming with C++");
        final Course comp3500 = new Course("3500: Algorithm & Data Structure with Java");
        final Course comp3000 = new Course("3000: Computer Architecture (C or Assembly)");
        final Course comp4000 = new Course("4000: Operating Systems (C)");
        final Course comp4100 = new Course("4100: Data Comm (C or C++");

        comp0000.addNext(comp1500);

        comp1500.addNext(comp1000);
        comp1500.addNext(comp1600);
        comp1500.addNext(comp2200);
        comp1500.addNext(comp2500);

        comp1000.addNext(comp1600);
        comp1000.addNext(comp2200);
        comp1000.addNext(comp2500);

        comp1600.addNext(comp4700);

        comp2200.addNext(comp2300);
        comp2200.addNext(comp3200);
        comp2200.addNext(comp3000);

        comp2500.addNext(comp4700);
        comp2500.addNext(comp3200);
        comp2500.addNext(comp3500);

        comp2300.addNext(comp3000);

        comp3200.addNext(comp4000);
        comp3200.addNext(comp4100);

        comp3000.addNext(comp4000);

        ArrayList<Course> courses = new ArrayList<>();

        courses.add(comp0000);
        courses.add(comp1000);
        courses.add(comp1500);
        courses.add(comp1600);
        courses.add(comp2200);
        courses.add(comp2300);
        courses.add(comp2500);
        courses.add(comp3000);
        courses.add(comp3200);
        courses.add(comp3500);
        courses.add(comp4000);
        courses.add(comp4100);
        courses.add(comp4700);

        return courses;
    }
}
```

``` 질의응답

인강:  코드보기: POCU 수강 순서
요약: 후위 순회 DFS를 이용한 위상정렬 알고리듬 만으로는 그래프가 순환하는지 알 수 없나요?
이 코드에서 의문점이 생겼습니다. 위상 정렬은 그래프에 cycle이 존재하는 경우 불가능하다고 배웠습니다.
현재 구현에서 아래와 같이 테스트를 해봤습니다.
"""
        var a = new Course("a");
        var b = new Course("b");
        var c = new Course("c");
        var d = new Course("d");
        a.addNext(b);
        b.addNext(c);
        c.addNext(d);
        d.addNext(a);
        var input = new ArrayList<>(List.of(a, b, c, d));
        var output = sortTopologically(input);
        for (var course : output) {
            System.out.println(course.title);
        }
""" 
일부러 그래프에 순환을 만들고 코드 샘플과 동일한 sortTopologically 함수를 호출해봤습니다.
지금 구현에서는 순환이 있어도 별 문제 없이 동작합니다.
제 생각에 처음에 방문하고 하위 깊이의 노드를 탐색하는 과정에서 상태를 나눠야 할 것 같습니다.
예를 들어 미방문/방문중/방문완료. 그리고 처음 방문하면 방문중 상태로 변경하고 재귀적으로 더 깊은 노드에 대한 탐색을 하고 
후위 순회로 링크드 리스트에 추가하는 연산을 하면 방문완료 상태로 바꿈
이런식으로 상태를 나눠야 후위 순회 DFS를 이용한 위상정렬에서 순환 그래프인지 확인할 수 있을 것 같습니다.
즉 위상 정렬을 순환이 있는 그래프에는 사용할 수 없고, 이 구현은 순환 그래프에서도 동작은 하고 이게 잘못된 동작인 것 같아 
의문이 들어서 질문드립니다.
1개의 댓글


[강사] 포프
방문 상태를 저장하지 않고 단순히 후위 순회 DFS만 사용하는 경우에는 그래프에 순환이 있는지 확인할 수 없습니다. 
이런 방식의 DFS 기반 위상 정렬 구현에서는 그래프에 사이클이 있어도 예외 없이 결과가 출력될 수 있는데, 
이는 겉보기에는 "별 문제 없이 동작하는 것처럼 보일 수 있지만", 실제로는 논리적으로 잘못된 결과를 내는 심각한 문제입니다.
사이클이 있는 그래프에서는 위상 정렬 자체가 정의되지 않기 때문에, 어떤 순서를 출력하더라도 그 순서를 따를 수 없습니다. 
예를 들어 A -> B -> C -> A처럼 순환 구조를 가지는 그래프에 대해 현재 구현을 돌리면 C B A와 같은 결과가 출력될 수 있지만, 
이 순서를 따라 수강한다고 가정하면 결국 A를 듣기 위해 C를 들어야 하고, C를 듣기 위해 다시 A를 들어야 하는 모순이 생깁니다. 
즉, 이 출력은 위상 정렬이 아니며, 논리적으로 틀린 결과입니다.
말씀하신 대로 노드의 방문 상태를 기억하는 로직까지 포함한 후위 순회 DFS는 그래프에 사이클이 있는지를 탐지할 수 있습니다. 
이 방식은 위상 정렬 구현에서 사이클을 감지하기 위한 대표적인 기법 중 하나입니다.
하지만 여기서 한 걸음 더 나아가 생각할 수 있는 질문은, 사이클을 감지한 후 어떻게 처리할 것인가입니다. 일반적으로 위상 정렬이 
목적이라면, 사이클이 감지되면 예외를 던지거나, null을 반환하거나, "순서를 정할 수 없음"이라는 명확한 실패 신호를 주는 방식으로 
정렬을 중단하는 것이 맞습니다. 더 나아가, 어떤 노드들이 순환에 포함되어 있는지를 사용자에게 명시적으로 알려주는 방식도 
가능합니다.
반면, 사이클을 무시하고 순서를 강제로 출력하거나, 일부 간선을 임의로 제거해서 위상 정렬을 시도하는 것은 원래 그래프의 
의미를 훼손하고, 결과적으로 잘못된 정보를 전달할 위험이 크기 때문에 일반적으로는 권장되지 않습니다.
```




## 강한 결합 요소  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/2965664a-0de6-49d2-8249-e8966ffa2f3a)  
여기서 순환하는 부분이 있음!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c45c33ad-c5cb-455c-a696-5d08554d372b)  
그래서, 노드4랑, 보라색 클러스터, 빨간 클러스터 3개 부분으로 나뉜 모양이 됨!  
그럼 클러스터 빨강에 연결하면 끝!  

강한 결합 요소 (Strongly Connected Component)  
방향 그래프에서 끈끈한 관계를 가지는 노드들의 최대 그룹!  
그 그룹에 속한 두 노드는 어떻게든 연결되어 있음  
반드시 이웃은 아님  
주 용도는 최적화! 고려해야 할 정점 수를 줄여줌  
다른 예)  
  그래프를 여러 SCC로 분리  
  각 SCC에 대해 알고리듬 실행  
  그 결과 합침  
실제 문제를 풀기 위해 SCC를 사용하는 경우도 있음  
위상 정렬과 강한 결합 요소  
위상 정렬은 순환을 해결할 수 없으므로, 순환하는 부분을 묶어서 위상 정렬하기도 함  

DFS 기반 알고리듬  
Kosaraju's algorithm  
Tarzan's algorithm  
경로 기반 알고리듬  
도달 가능성 기반 알고리듬 (분할 정복)  

코사라주 알고리듬  
1. 그래프 G를 DFS 후위 순회 (역순) 한다
2. 전치 그래프 G^T를 계산한다 (변의 방향이 반대인 그래프)  
3. G^T의 각 노드에서 DFS를 실행한다  
(1에서 찾은 순서대로, 각 DFS 실행에서 얻은 목록이 강한 결합 요소!)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/38905d0b-3960-4500-a5b7-bf6b5693c7b0)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/2fed3313-198f-4ec7-b7e1-41fcd03102fe)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e0d2bbba-c1e5-4c0b-92a1-2784c11d648f)  

코사라주 알고리듬의 이해 (증명은 각자 찾기)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/8842ad7d-0ff7-4df4-999c-d256c16f7184)  
두 번째 단계 (transpose하는 것) : component사이의 연결 방향만 바뀜.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e52a5010-ef21-430c-885c-70da6b1b97ed)  

강한 결합 요소의 용도? 주로 복잡한 네트워크 관계 관련, 신경과학에서도 사용  
방대한 양의 데이터에서 연관된 그룹 찾기에 유용!  
예:  
여전히 진입이 가능하게 보장하면서 일방 통행로 봉쇄하기  
한 도시에서 다른 도시로 비행기 여행이 가능한지 확인  
SNS에서 직장동료, 학교 동기 찾기  
SNS에서 취미나 성향이 같은 사람 찾기  

## 그래프의 너비 우선 탐색  
트리에서 봤던 너비 우선 탐색. 단, 그래프에서는 방문한 노드를 기억해야 함  
실제로는 발견한 노드를 기억. 깊이 우선 탐색에서 한 대로!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/0c00322f-734e-4b87-973b-336cbf4e9ee8)  

시간 복잡도 O(N + E)  
