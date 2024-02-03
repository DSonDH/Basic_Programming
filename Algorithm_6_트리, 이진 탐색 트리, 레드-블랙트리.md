# 트리
실무에서 사용할 일 많은 구조.  
tree의 계층적 구조를 표현  
노드(node) : 실제로 저장하는 데이터  
루트(root) 노드: 최상위에 위치한 데이터. 시작 노드.  
리프(leaf) 노드: 마지막에 위치한 데이터들. 더이상 가지를 치지 않음.  
부모-자식: 연결된 노드들 간의 상대적 관계. 부모는 언제나 하나  
조부모, 삼촌(uncle), 형제자매(sibling)도 있음.  
깊이(depth): 노드부터 루트까지 경로의 길이.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d43447be-541b-450b-9f46-d417c5f9c5ea)  
높이(height): 노드부터 리프경로들 중 최대 길이  
하위 트리(subtree): 어떤 노드 아래의 모든 것을 포함하는 트리  
!! 재귀적: 하위 트리 그 자체가 트리임!  

* 트리의 저장법 및 용도
트리 속성  
1. 부모와 자식 모두 노드
2. 부모 한명 뿐, 자식은 다수 가능
3. 자식은 언제나 부모로부터 가지를 침
따라서 부모가 자식을 참조하는 방식이 가장 직관적  
``` java
public class Node {
    public int data;
    public ArrayList<Node> children;
}

public class BinaryNode {
    public int data;
    public Node left;
    public Node right;
}
```
자식이 2개니 이진 트리라 함.  
자식이 하나 뿐이면 그냥 배열/링크드리스트 임.  

!! 트리의 용도 !!  
계층적 데이터를 표현  
- HTML이나 XML의 문서 개체 모델(DOM)을 표현  
- Json이나 YAML처리 시 계층 관계를 표현  
- 프로그래밍 언어를 표현하는 추상 구문 트리(abstract syntax tree)  
- 인간 언어를 표현하는 파싱 트리(parsing tree)  

검색 트리를 통해 효율적인 검색 알고리듬 구현 가능  
그 외 다수의 용도가 있음!  

## 이진 탐색 트리 (Binary Search Tree, BST)

### BST 탐색

### BST 삽입

### BST 삭제


중위 순회
전위 순회, 후위 순회

## 레드-블랙 트리
레드-블랙 트리의 특성

### 레드-블랙 트리의 삽입 방법

### 레드-블랙 트리의 삭제 방법




