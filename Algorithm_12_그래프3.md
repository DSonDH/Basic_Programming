# 최소 신장 트리 (MST, Minimum Spanning Tree)
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/cfb5d2d5-1d3b-4c18-9030-e88d79d0cc69)  

신장 트리: 어떤 그래프 안에 있는 모든 노드를 연결하는 트리  
여러 방식이 있을 수 있음  
신장 트리 중 비용(모든 변의 가중치를 합한 값)이 최소인 트리  

순환(cycle) : 반복되는 노드가 시작 노드 끝 노드뿐인 경로  
컷(cut) : 어떤 그래프를 서로소(disjoint)인 두 하위 집합으로 나누는 행위  
그래프의 노드들을 두 그룹으로 분리시키는 것  
컷 세트(cut-set): 두 그룹을 연결하는 변들의 집합  
이 변들을 제거하면 그래프가 둘로 분리됨  

컷 속성(cut property)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c880bda5-e191-4af0-8c47-7a93efe9dda1)  

MST알고리듬의 기본 원리 (그리디 알고리즘)  
1. 그래프에 있는 노드 중 한 변을 확인
2. 이 변이 MST에 들어가야 하는지 검사.  
이때, cut property를 사용  
들어가야 하면 MST에 추가, 아니면 무시
3. MST의 모든 변을 찾지 못했다면 1로 돌아감

Kruskal's algorithm, Prim's algorithm이 있는데 여기선 크러스컬 만 배움.  
## 크러스컬(Kruskal's) 알고리듬
1. 그래프의 각 노드마다 그 노드만 포함하는 트리를 만듦
2. 모든 변을 가중치의 오름차순으로 정렬 => S배열
3. S가 비거나 MST가 완성될 때까지 다음의 과정을 반복
   - S에서 가중치가 가장 적은 변을 제거해서 고려
   - 이 변이 두 트리를 연결하는지 검사
   - 그렇다면 MST에 추가, 아니라면 버림
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c89c7444-f16f-4df7-9264-a81258bae736)

* disjoint set
합집합 찾기(union-find) 자료 구조라고도 함  
겹치지 않는 집합들을 저장하는 자료 구조  
서로 다른 트리는 겹치지 않는 집합  
이걸 서로소 집합에 저장하면 간단한 연산만으로 겹치는 지 알 수 있음  

disjoint-set의 연산  
1. MakeSet(element) : 새로운 집합을 만듦
2. Find(element) : element가 속한 집합을 찾음  
Find(x) == Find(y): 둘이 같은 집합에 속함  
Find(x) != Find(y): 둘이 다른 집합에 속함  
가장 간단한 구현: 그 집합에 속한 요소 중 하나를 결정론적으로 반환  
4. Union(element1, element2): 두 집합을 합침  
(element1이 속한 집합 + element2가 속한 집합)  

disjoint-set을 사용한 크러스컬 알고리듬  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/8035c394-ddc7-4cba-96f3-38c9f79719a8)  

시간복잡도  
변 정렬: O(ElogE)  
나머지 복잡도는 disjoint-set의 시간 복잡도에 따라 결정됨  
최적화된 disjoin-set 알고리듬이 존재하는데, 이 시간복잡도는 생략 ...  
최종 시간 복잡도: O(ElogE) = O(ElogV)  

Prim's algorithm  
1. 아무 노드나 하나 골라서 트리를 하나 만듦
2. 이 트리를 성장시킬 수 있는 변을 하나 고름  
아직 트리에 속하지 않은 노드와 연결하는 변 중 비용이 가장 작은 변  
이미 트리에 속해 있는 노드와 연결하는 변이면 무시
3. MST가 완성되거나 더 이상 고려한 변이 없을 때까지 2번 반복

코드보기: 크러스컬 알고리듬  
``` java
// Edge.java
package academy.pocu.comp3500samples.w13.kruskal;

public final class Edge implements Comparable<Edge> {
    private final String node1;
    private final String node2;
    private final int weight;

    public Edge(final String node1,
                final String node2,
                final int weight) {
        this.node1 = node1;
        this.node2 = node2;
        this.weight = weight;
    }

    public String getNode1() {
        return this.node1;
    }

    public String getNode2() {
        return this.node2;
    }

    public int getWeight() {
        return this.weight;
    }

    @Override
    public int compareTo(Edge e) {
        return this.weight - e.weight;
    }
}

// DisjointSet.java
package academy.pocu.comp3500samples.w13.kruskal;

import java.util.HashMap;

public final class DisjointSet {
    private class SetNode {
        private String parent;
        private int size;

        public SetNode(final String parent, final int size) {
            this.parent = parent;
            this.size = size;
        }
    }

    private final HashMap<String, SetNode> sets = new HashMap<>(64);

    public DisjointSet(final String[] nodes) {
        for (String s : nodes) {
            SetNode setNode = new SetNode(s, 1);
            this.sets.put(s, setNode);
        }
    }

    public String find(final String node) {
        assert (this.sets.containsKey(node));

        SetNode n = this.sets.get(node);
        String parent = n.parent;
        if (parent.equals(node)) {
            return node;
        }

        n.parent = find(n.parent);

        return n.parent;
    }

    public void union(final String node1, final String node2) {
        assert (this.sets.containsKey(node1));
        assert (this.sets.containsKey(node2));

        String root1 = find(node1);
        String root2 = find(node2);

        if (root1.equals(root2)) {
            return;
        }

        SetNode parent = this.sets.get(root1);
        SetNode child = this.sets.get(root2);

        if (parent.size < child.size) {
            SetNode temp = parent;

            parent = child;
            child = temp;
        }

        child.parent = parent.parent;
        parent.size = child.size + parent.size;
    }
}

// Kruskal.java
package academy.pocu.comp3500samples.w13.kruskal;

import java.util.ArrayList;
import java.util.Arrays;

public final class Kruskal {
    private Kruskal() {
    }

    public static ArrayList<Edge> run(final String[] nodes, final Edge[] edges) {
        DisjointSet set = new DisjointSet(nodes);

        ArrayList<Edge> mst = new ArrayList<>(edges.length);

        Arrays.sort(edges);

        for (int i = 0; i < edges.length; ++i) {
            String n1 = edges[i].getNode1();
            String n2 = edges[i].getNode2();

            String root1 = set.find(n1);
            String root2 = set.find(n2);

            if (!root1.equals(root2)) {
                mst.add(edges[i]);
                set.union(n1, n2);
            }
        }

        return mst;
    }
}

// Program.java
package academy.pocu.comp3500samples.w13.kruskal;

import java.util.ArrayList;

public class Program {
    public static void main(String[] args) {
        String[] nodes = new String[]{
                "0",
                "1",
                "2",
                "3",
                "4",
                "5",
                "6",
                "7"
        };

        Edge[] edges = new Edge[]{
                new Edge("0", "4", 9),
                new Edge("0", "5", 2),
                new Edge("0", "2", 2),
                new Edge("1", "4", 6),
                new Edge("1", "5", 10),
                new Edge("2", "5", 1),
                new Edge("2", "7", 11),
                new Edge("2", "3", 5),
                new Edge("5", "7", 8),
                new Edge("5", "4", 3),
                new Edge("6", "7", 13)
        };

        ArrayList<Edge> mst = Kruskal
                .run(nodes, edges);

        for (Edge e : mst) {
            String edgeString = String
                    .format("(%s, %s)",
                            e.getNode1(),
                            e.getNode2());

            System.out.println(edgeString);
        }
    }
}
```

## 외판원 문제 (Traveling Salesman Problem)
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/5b00ffe2-511a-4349-80f5-f5f823773703)  
모든 노드를 최소한의 거리로 돌아다니기  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c8ad28f4-c1cf-4d0a-890f-df79be88bcca)  
NP 난해 문제임 !!  
다만, 다양한 근사 알고리듬이 존재함  
특정 조건을 만족하는 그래프에만 적합한 알고리듬  
실제 최소 비용보다 최대 k배까지 허용하는 알고리듬  
주시위를 굴리는 알고리듬 등등  

우리가 볼 TSP 그래프  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/4c5539cb-39bc-4095-bf6a-54e33594d4aa)  
+변의 가중치는 삼각 부등식을 만족!  

해밀턴 경로(Hamiltonian path): 모든 노드를 방문하는 경로  
해밀턴 사이클(Hamiltonian cycle): 모든 노드를 방문하고 원래 노드에 돌아오는 경로  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/a96807d1-aca5-49bd-8226-01dd8ffa1bc4)  

TSP 2-근사 알고리듬  
아무리 커도 최소 비용보다 2배인 경로를 찾음  
참고: k배인 근사 알고리듬은 k-근사 알고리듬이라 함  
삼각 부등식을 만족하는 TSP에 사용 가능!  

1. MST (최소 신장 트리) 를 만듦  
TSP 경로 비용의 하한  
중간에 끊어진 노드가 없기에 언제나 만들 수 있음  
크러스컬 이용 시 O(ElogV)  
2. MST를 그냥 한 바퀴 돎  
아무리 느려도 각 변을 2번 방문하는 게 끝  
이미 방문한 노드는 건너 뜀(완전 그래프라 가능)  
그 한 바퀴 도는 경로가 해밀턴 순환  

MST에서 해밀턴 순환 만들기  
a) MST의 노드를 DFS로 전위 순회하며 목록에 저장  
b) 저장된 노드를 차례로 방문하며 해밀터 순환 H를 만듦  
첫 방문인 경우, H에 추가  
이전에 방문했었다면, 무시  

TSP 알고리듬의 실제 사용례  
여러 장소 방문 문제 (학교 버스 경로 게산, 배당 경로 계산)  
효율적인 공정 계획 (예: 회로 기판에 구멍 뚫는 순서)  
DNA 염기서열 분석  
엑스선 결정학 분야에서의 결저구조 해석 등등  

(참고) TSP 변형과 꼼수  
변형1: 완전 그래프가 아닌 경우  
1. 연결 안 된 노드들을 연결
2. 새 변의 가중치를 매우 높게 대입
3. TSP 알고리듬을 실행

변형2: 비대칭(asymmetric) TSP  
이거 전용 알고리즘이 있지만, 꼼수를 볼 것임  
1. 고스트 노드를 추가하여 대칭 TSP로 변환  
고스트끼리 연결하지 않음. 원본 노드까리 연결하지 않음. 이는 무한대 거리로 표현.  
2. TSP 알고리듬 실행  
3. 고스트 노드를 원래 노드에 합침!  

삼각 부등식이 성립 안 하는 TSP  
다항식 시간 안에 괜찮은 해법을 찾을 수 없음  
근사 알고리듬 써도 마찬가지.. 모순에 의한 증명으로 증명 가능  
물론 P=NP면 다른 얘기!  

# 흐름 네트워크와 최대 유량
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/58e34d83-3aa8-4d87-816f-9362b8311789)  

네트워크 유량 문제: 어떤 흐름 네트워크에서 유량을 결정하는 문제  
- 최대 유량(maximum flow) 문제
- 최소 비용 유량(minimum-cost flow) 문제
- 다중 상품 흐름(multi-commodity flow) 문제
- 0일 곳이 없는 흐름(nowhere-zero flow) 문제

## maximum flow 문제
어떤 노드에서 다른 노드까지 보낼 수 있는 최대 양을 결정하는 문제  
최고 데이터 전송 속도, 최대 교통량 등등  
병렬연결로 유량이 늘어날 수 있음  
병목으로 유량이 줄 수도 있음  

수요와 유통 문제  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/40a3059a-4b73-4f3b-8331-d0e419bc26ef)  
여러 알고리듬이 있음. 가장 단순한 방법은 brute force (간단한 BFS)  
효율적인 대표 알고리듬: 포드풀커슨(Ford-Fulkerson) 알고리듬, 에드몬드-카프(Edmonds-Karp) 알고리듬  

## 에드몬드-카프 알고리듬  
각 변마다 용량이 0인 back edge 추가  
모든 변의 유량을 0으로 초기화  
- 용량이 남아있는 변둘 즁에 시작점 -> 도착점까지의 최단 경로를 찾음 (BFS)
  - 최단 경로에 있는 각 변의 잔여 용량 중 최솟값을 취함
  - 그 값을 경로 상에 있는 각 변의 유량에 더함
  - 대칭 변에서 그만큼의 유량을 뺌
- 아직도 찾을 최단경로가 있다면 BFS과정으로 돌아감
- 도착점으로 들어오는 모든 유량의 합을 반환!

back edge (역방향 변)이라는 개념을 도입하여 위 알고리듬 돌리면 최적의 해법 구할 수 있음!  
유량을 분산시키기 위해 사용하는 멋진 꼼수!  
이미 존재하는 변과 방향이 반대인 가상의 변  
용량은 0임: 의도치 않게 역류하는 경우 방지, 용량에 여유가 있는 다른 변에 유량을 분산시키기 위해서만 존재  
유량의 대칭성이랑 개념을 이용! u->v가 유량 3이면 v->u 유량은 -3  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/aa708fb0-f7f9-418e-86ac-0c6bf6f291f9)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/97edb76f-31b8-4864-bf3f-29c6cb0e4676)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/995805fc-70dd-4613-82c3-0fe7307fa3a5)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e698da2c-1553-4255-8eae-fd339f687ad5)  
이제 갈 수 있는 경로 없음!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/4ff6d35f-6cdd-43bf-9724-611be01423f3)  

최대 유량 문제 예  
순환-수요 문제  
야구 탈락 문제  
단체 미팅 문제  
항공운행 스케줄 짜기 문제  
프로젝트 선택 문제  
이미지 segmentation 등  

* 기타 그래프 문제들
clique, graph coloring, independent set, bipartite graph, vertex cover, matching, etc ..
