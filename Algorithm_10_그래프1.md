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

그래프 DFS의 시간 복잡도

### 위상 정렬
DFS를 사용한 위상 정렬

강한 결합 요소
위상 정렬과 강한 결합 요소
코사라주 알고리듬
코사라주 알고리듬의 이해

## 그래프의 너비 우선 탐색
그래프 BFS의 시간 복잡도
