# 최단 경로 찾기

최단 경로 (shortest path, SP)  
순환이 없게끔 해야 함  
가장 간단한 방법은 brute forece.  
BFS를 사용하면 언.제.나. 최단 경로를 찾을 수 있음! O(N + E)  

BFS로 최단 경로 찾기  
기본적은 BFS와 비슷함.  
시작점부터 현재 노드 까지의 거리를 기억해야 함  
거리 = BFS깊이.  
기억방법: 해시맵에 모든 노드의 거리 저장  
2D 배열로 저장 (인접 행렬과 유사)  
각 노드 안에 거리를 저장 (BFS를 실행하기 전에 리셋해줘야 함, 올바른 oop는 아님)  

각 변의 거리가 같을 때 최단 경로 찾기  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/65cce26c-f9b1-4e21-916a-f27d59f67a9d)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/75d99d96-4fce-43c5-a473-ae33decd1541)  

각 변의 거리가 다른 최단 경로 찾기  
BFS로 간단히 해결할 수 없음!! 다른 알고리듬이 필요!  

## 다익스트라 알고리듬 (Dijkstra's algorithm)  
두 노드 사이의 최단 경로를 찾음  
방대한 노드 네트워크에 사용하기 충분히 빠름  
변의 가중치가 음수인 경우에는 제대로 작동하지 않음  
실세계에서 많이 사용 (지도/내비게이션, IP라우팅, 경유 항공편 찾기, 등)  

기초  
아래 그림에서는 m3에서 와서 다른 노드로 가는걸 찾는 과정을 보여주는 것.  
m3까지 오는데 거리가 2였고, +3이 되고 있는거임.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/7d554f1d-6233-4bc6-a818-3c4b137c7b2d)  
기존 거리는 무한대로 보통 설정되는것 같고,  
계속 이 경로 저 경로 비교하면서 각 노드의 거리를 계속 업데이트 하는 듯  
모든 노드를 방문하면 최단 거리를 찾음  
모든 노드를 거쳐 온 경로 중 최솟값을 취했기 때문! 동적계획법임! 언제나 최적의 해를 가짐  

다익스트라 알고리듬  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/70a12284-cf75-47b7-b6a5-3983ef143a5a)  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/db82677d-a74d-4830-b855-4bb5e00a6446)  
시작 노드의 거리는 0  
0번에서 갈 수 있는 다른 노드는 1번, 2번.  
원래 1번의 거리와, 0번의 거리에 연결된 엣지 거리 더한거를 비교해서, 짧은 것 선택!  
이제 2번과 3번에서 고민하면 됨  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e0c0b406-8700-419e-964c-24464c376bfe)  

인전행렬을 썼을 때 문제가 생길 수 있음  
노드는 수백만 개인데 변은 몇 개 안되면 공간낭비임!  
이를 해결하고자 인접리스트로 진짜 연결된 애들만 봐야 할 수도 있음  

인접리스트 사용 기준 시간복잡도  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/4f1864f9-3cff-456b-8c64-2194a9c656de)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/3786546f-7652-4ea0-a7bc-2eb195a6ebbf)  

인접행렬 사용 기준 시간 복잡도: O(N^2)  

더 빠른(?) 자료 구조  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/38981aa5-81a6-412d-8784-478d68571bd9)  

다익스트라와 음의 가중치  
음의 가중치면 다익스트라는 오작동함! 한 번 방문한 노드는 다시 방문 안하므로!  
다음의 거리는 언제나 이미 방문한 거리 이상의 거리를 가짐.  
음의 거리면 그 길 걸을 수록 개이득이므로  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/9173a931-7a71-4311-b124-36321780e9c8)  
밑에 노드는 s에서 이미 확인한 거리라서 위에 노드에서 고려가 안되는 부분임.  
이 문제를 해결하는 알고리즘이 벨만포드 알고리즘인데, 궁금하면 찾아보기!  

코드보기: 우선순위 큐를 사용한 다익스트라 알고리듬  
```java
// Node.java
package academy.pocu.comp3500samples.w12.dijkstra;

import java.util.HashMap;
import java.util.Map;

public final class Node {
    private final String name;
    private final HashMap<Node, Integer> roads = new HashMap<>();

    public Node(final String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public Map<Node, Integer> getRoads() {
        return this.roads;
    }

    public void addRoad(final Node to,
                        final int dist) {
        this.roads.put(to, dist);
    }

    public int getDistance(final Node to) {
        return this.roads.get(to);
    }
}

// Dijkstra.java
package academy.pocu.comp3500samples.w12.dijkstra;

import java.util.HashMap;
import java.util.Map;
import java.util.PriorityQueue;

public class Dijkstra {
    private Dijkstra() {
    }

    public static HashMap<String, Integer> run(final HashMap<String, Node> nodes, final String from, final HashMap<String, String> prevs) {
        HashMap<String, Integer> minDists = new HashMap<>();

        final int INF = Integer.MAX_VALUE;
        for (var entry : nodes.entrySet()) {
            String name = entry.getKey();

            minDists.put(name, INF);
        }

        minDists.put(from, 0);

        prevs.put(from, null);

        PriorityQueue<Candidate> open = new PriorityQueue<>();

        Node s = nodes.get(from);
        Candidate candidate = new Candidate(s, 0);

        open.add(candidate);

        while (!open.isEmpty()) {
            candidate = open.poll();

            Node n = candidate.getNode();
            String nodeName = n.getName();

            int minDist = minDists.get(nodeName);
            int dist = candidate.getDistance();

            if (minDist < dist) {
                continue;
            }

            Map<Node, Integer> roads = n
                    .getRoads();

            for (var e : roads.entrySet()) {
                Node next = e.getKey();

                int weight = e.getValue();
                int newDist = minDist + weight;

                String nextName = next.getName();
                int nextMinDist = minDists
                        .get(nextName);

                if (newDist >= nextMinDist) {
                    continue;
                }

                minDists.put(nextName, newDist);
                prevs.put(nextName, nodeName);

                Candidate newCandidate = new Candidate(next, newDist);

                open.add(newCandidate);
            }
        }

        return minDists;
    }
}

// Candiate.java
package academy.pocu.comp3500samples.w12.dijkstra;

public final class Candidate implements Comparable<Candidate> {
    private final Node node;
    private final int distance;

    public Candidate(final Node node, final int distance) {
        this.node = node;
        this.distance = distance;
    }

    public Node getNode() {
        return this.node;
    }

    public int getDistance() {
        return this.distance;
    }

    @Override
    public int compareTo(Candidate o) {
        return this.distance - o.distance;
    }
}

// Program.java
package academy.pocu.comp3500samples.w12.dijkstra;

import java.util.HashMap;
import java.util.LinkedList;

public class Program {
    public static void main(String[] args) {
        HashMap<String, Node> nodes = createNodes();

        HashMap<String, String> prevs = new HashMap<>();

        HashMap<String, Integer> minDists = Dijkstra.run(nodes, "Home", prevs);

        int schoolDist = minDists.get("School");
        System.out.println(schoolDist);

        int bankDist = minDists.get("Bank");
        System.out.println(bankDist);

        int libDists = minDists.get("Library");
        System.out.println(libDists);

        LinkedList<String> path = new LinkedList<>();

        String name = "School";
        while (name != null) {
            path.addFirst(name);
            name = prevs.get(name);
        }

        String pathString = String.join(" -> ",
                path);

        System.out.println(pathString);
    }

    private static HashMap<String, Node> createNodes() {
        Node home = new Node("Home");
        Node policeStation = new Node("Police Station");
        Node school = new Node("School");
        Node park = new Node("Park");
        Node bank = new Node("Bank");
        Node library = new Node("Library");

        home.addRoad(policeStation, 2);
        policeStation.addRoad(home, 2);

        home.addRoad(park, 3);
        park.addRoad(home, 3);

        policeStation.addRoad(bank, 1);
        bank.addRoad(policeStation, 1);

        policeStation.addRoad(school, 6);
        school.addRoad(policeStation, 6);

        bank.addRoad(library, 2);
        library.addRoad(bank, 2);

        bank.addRoad(park, 2);
        park.addRoad(bank, 2);

        school.addRoad(library, 1);
        library.addRoad(school, 1);

        HashMap<String, Node> nodes = new HashMap<>();

        nodes.put(home.getName(), home);
        nodes.put(policeStation.getName(), policeStation);
        nodes.put(school.getName(), school);
        nodes.put(park.getName(), park);
        nodes.put(bank.getName(), bank);
        nodes.put(library.getName(), library);

        return nodes;
    }
}
```

## A* 알고리듬
다익스트라는 언제나 목적지까지의 최단 경로를 찾아줌.  
그러나, 불필요한 부분까지도 너무 많이 고려함.  

A* 알고리듬  
다익스트라와 기본은 같은 알고리듬, 하지만 쓸데없는 평가를 피할 수 있음  
이를 위해 다음 노드 선택 시 기준을 하나 더 추가  
다익스트라의 기준은 시작점부터 노드까지의 거리,  
A* 가 추가하는 기준은 그 노드로부터 목적지 까지의 거리  

현재 노드부터 목적지까지의 거리  
목적지까지 탐색을 다 하기 전까지는 확실히 모름  
따라서 A* 가 추가한 기준은 결정적이 아님! 휴리스틱이고 근사치임  
이 휴리스틱 함수에 따라 A* 의 성능이 달라짐  
대부분의 경우 다익스트라보다 빠른데, 데이터에 따라 느릴 수도 있음  

### A* 의 두 가지 노드 선택 기준  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d410d24e-d6e8-407b-b00e-1adba7221f58)  

h(n)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/759de04c-8d38-406f-8274-8367143084ec)  

다익스트라와의 차이점:  
OPEN이란 이름의 노드 집합이 있음 -> 방문할 최단 경로 후보 노드들이 들어있음  
오픈 안에 있는 후보 선택 시 최소 f(n)을 이용  
같은 노드를 두 번 이상 방문할 수 있음 (이유는 나중에 설명)  

A* 알고리듬  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/97e5a159-3e5b-461d-bde6-58ab15d77fcb)  
길이 업데이트는 똑같고, 노드 샘플링만 다름!  

예시:  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/88e7631f-0faa-470f-adb0-d9d682a5d327)  
주황색 표기: OPEN에 들어간 것  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/9ac448ef-36de-43d7-817a-9e294febb117)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/8ee66a50-2cca-41e5-9816-7a3fe6e02f05)  
f(경찰서)는 6, f(공원)은 10으로 공원이 더 크니깐 경찰서 선택  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/07543a51-22a7-43e5-92fc-ded537814ac4)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/11c79d41-813c-46f6-ab80-7e86c6702564)  
집은 업데이트 안됬으니 OPEN에 추가 안함. 학교, 은행이 오픈됨  
f(학교), f(공원), f(은행) 셋 중 가장 작은걸 뽑음  
학교가 선택되고, 최단경로 찾고 끝!  
근데 실제 최단경로는 은행 도서관 거치는건데 휴리스틱이라서 이렇게 끝나버림!  

h(n) 함수에 대한 이해  
이 함수의 결과와 실제 결과의 관계에 따라 A* 알고리듬 행동이 바뀜!  
h'(n)을 n -> 목적지로 이동하는 실제 비용이라 하자  
h(n)이 언제나 0인 경우: A* 가 언제나 다익스트라 알고리듬과 같이 동작함. f(n) = g(n)이 되니까  
h(n)이 h'(n)보다 작거나 같은 경우: 추정 거리가 실제 거리 이하인 경우. 이때의 h(n)을 admissible (허용할 수 있다)고 함  
언제나 이러면 A* 는 최단 거리를 찾음. 하나라도 안 그러면 보장 못 함  
h(n)이 h'(n)보다 훨씬 작은 경우: 추정 거리가 실제 거리보다 훨씬 작음 h에 따른 변별력이 적어지고  
g에 의존도가 커져 다익스트라와 유사해짐 A*가 더 많은 경로를 탐색! 탐색 범위가 넓어짐! 속도 느려짐!  
h(n) == h'(n)이면 추정 거리가 실제 거리와 같음. 언제나 최고의 경로를 따라가고 매우 빠름!  

QnA 박승훈님: 즈음에 "다익스트라는 A* 의 특수한 케이스다"라고 말씀하셨는데,  
"A*는 다익스트라의 특수한 케이스이다."도 성립할까요?  
A: 그건 논리적으로 말이 안되는 말 같습니다.  
A가 B의 스페셜 케이스이고, 그와 동시에 B가 A의 스페셜 케이스이면.. A와 B가 동치여야 하거든요.  

A* 의 중복 방문과 시간 복잡도  
다익스트라는 새로 방문하는 노드의 실제 거리가 최소  
- 실제 거리 g(n)만 노드를 뽑는 기준으로 사용하므로.  
- 이미 최소니까 더 이상 작아질 수 없음. (동적 계획법의 장점)  

A* 는 새로 방문하는 노드의 거리가 실제 거리가 아님. 추정치도 있음!  
- h(n)으로 추정하는 부분이 있음  
- 지금 최소 거리라 믿고 뽑은 노드가 실제 최소가 아닐 수 있어서 다시 돌아가서 확인해야 함  
- 나중에 다른 경로를 통해 방문하면 거리가 작아질 수도 있음  

그러나 h(n)이 특정 조건을 만족하면 노드를 한 번씩만 방문함  
- 일관적(consistant) / 단조로운(monotone) 휴리스틱  
- (참고) 특정 조건: h(n) <= dist(n, neighbor) + h(neighbor)  

시간 복잡도  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/71e7c52c-ff18-4a16-bccf-433dbe011d3a)  
b: branch factor, d: depth  

## 플로이드 워셜 알고리듬  
여태 본 문제들은 단일 출발지 최단 경로  
SSSP, Single-Source Shortest Path  
모든 노드 쌍에 대해 최단 경로를 찾는 문제들도 있음  
APSP, All-Pairs Shortest Path  
SSSP 알고리듬을 모든 노드에서 한 번씩 시작해도 해법은 나옴  
다만 N 배 시간복잡도가 나빠짐. 더 나은 APSP 전용 알고리듬이 있음!!  


![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/24ac3502-ff84-4b7d-bf54-881e69e889a7)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/2d1a5b2c-1878-445f-8166-fdbb8fdb0181)  
sp(i, j, k): shortest path, i에서 j로 가는 최단 경로  
단, 중간에 1 ~ k 노드를 거쳐도 됨. k+1 ~ N 노드는 거치지 않음  

플로이드 워셜 공식  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/38be8819-70fa-42e2-96f9-4d59b1755b02)  
이 공식으로 그리드 만들어야 함!  
3차원 ㄴㄴ 2차원으로  
1. 4x4 행렬 만듦  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/cb4a6f6c-f9ac-4ee0-bac9-4700995b4bca)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/0e50c828-a4f9-4dce-8015-53068a624d60)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/76be73b5-979b-4390-bf94-d87ea58e7148)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/2ca690bf-d2af-47a4-bc87-e2f340527b0e)  
... 아무것도 업데이트 안됨!  
아무것도 업데이트 안됨  
k = 1일때는?  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c5ccd1b1-facf-44ba-ac5c-df68880aee40)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c31958ef-9c4a-4a43-9918-6f25ae3853ed)  
위 두 경우가 업데트 됨!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/57c34c97-cb44-4ec6-b846-74bd7975ee76)  
최종 결과
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/9b685b5e-1979-4729-981d-000fc9a047ee)  

시간복잡도, 공간복잡도  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/58113e8e-fee8-42e0-aa8d-ac7b4b41db77)  

