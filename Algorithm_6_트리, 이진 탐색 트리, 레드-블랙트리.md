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
트리의 특수한 특수한 것. 보통은 이 이진 탐색 트리를 말함.  
자식이 최대 둘. 계층적, 재귀적으로 이분해 나갈 때 적합함.  
그 무언가를 이분하는 기준을 만들면, 그 기준에 따라 특화된 이진 트리를 만들 수 있음.  
그에 따라 보다 효율적인 알고리듬 고안 가능 (예: binary search tree)  

이진 탐색 트리, binary search tree (BST)  
이진 트리에 이분하는 규칙을 추가:  
왼쪽 자식은 언제나 부모보다 작음.  
오른쪽 자식은 언제나 부모 이상.  

순서대로 BST 읽기: 재귀적으로 읽는 순서만 지키면 오름차순으로 읽을 수 있음.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/098209f6-9fed-4fa3-86fb-62a663befadd)  
지금 읽은 방법은 중위 순회법 (in-order traversal)임.  
이는 정렬된 트리(=정렬된 자료구조)이므로, 정렬된 자료구조에 특화된 알고리즘 사용에 유리함.  
예: 이진 탐색 알고리듬  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/02450c08-2698-421a-bb4b-f1c567029c4a)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d4b28e2c-828d-4edc-8b8f-473b3f802130)  

### BST 탐색
기본적으로 이진 탐색과 동일 (분할정복, 재귀적)  
단, 각 노드마다 두 하위 트리로 이분됨.  
하위 트리로 내려갈 때마다 검색 공간이 절반씩 줄어듦.  
O(logN) 최악은 O(N) 연결리스트와 같이 한쪽에 모두 쏠렸을 때.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d6021bad-1d6d-4834-b827-eace2196b258)  

### BST 삽입
전략: 
1. 새로운 노드를 받아줄 수 있는 부모 노드를 찾음.
- 트리를 내려가는 방법은 탐색과 같음.
- 새로운 노드를 받아줄 수 있는 부모란? 내려가야하는 방향에 자식이 없는 부모.
2. 그 후, 거기에 자식으로 추가. 

1번 은 O(logN), 2번은 O(1) 시간복잡도가 걸림.  

이미 자라있는 부분은 유지됨. 기존 노드 위치를 하나도 안바꿈.  
새로운 가지를 뻗어나갈 뿐! 새로 추가되는 값은 언제나 리프노드!  

코드보기 : BST 삽입  
``` java
package academy.pocu.comp3500samples.w06.insert;

public class Node {
    private final int data;
    private Node left;
    private Node right;

    public Node(final int data) {
        this.data = data;
    }

    public int getData() {
        return this.data;
    }

    public Node getLeft() {
        return this.left;
    }

    public Node getRight() {
        return this.right;
    }

    public static Node insertRecursive(final Node node, int data) {
        if (node == null) {
            return new Node(data);
        }

        if (data < node.data) {
            node.left = insertRecursive(node.left,
                    data);
        } else {
            node.right = insertRecursive(node.right, data);
        }

        return node;
    }
}
```

### BST 삭제
트리에서 뭔가를 지울 때 언!제!나! 리프를 지움.  
노드를 삭제한 뒤에도 올바른 BST를 유지하려면, 정렬된 배열에서 값을 삭제하듯이 해야함.  
10을 지우고, 앞에있는 아이들을 뒤로 땡기던지, 뒤에있는 아이들을 앞으로 땡기던지!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/11c8a4a6-45b6-497c-8206-fd9512116aed)  

뒤에 12를 한칸씩 앞땡기기?  
오른쪽 하위 트리에서 최솟값(제인 왼쪽 리프). 이를 in-oder successor라고 부르고,  
얘를 땡겨온다.  

앞에 아이들을 뒤로 땡기기?  
왼쪽 하위 트리에서 최댓값(제일 오른쪽 리프)  
이를 in-oder predecessor라고 부른다.  

삭제 전략 정리  
1. 지울 값을 가지고 있는 노드를 찾음. 없으면 return false
2. 그 바로 전 값을 가진 노드를 찾음 (왼쪽 하위 트리의 제일 오른쪽 리프)
3. 두 값을 교환
4. 리프 노드를 삭제
또는, 3, 4번 합쳐서, in-order successor로 찾을 값 을 대체한다.  

BST 삭제 시간 복잡도?  
1, 2번 과정이 O(logN). 3, 4번 과정이 O(1)  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e4340c83-c681-45f6-aa19-3140f7203460)  
이거 삭제할 때 실제 지워지는 노드는 83 노드란다 ... ??  
그냥 트리 재정렬하고 마지막이랑 맨 처음 상태랑 차이가 나는 노드가 거기라서 그런듯.  

### 트리 순회
1. 중위 순회 (in-order)
왼쪽 하위 트리 -> 현재노드 -> 오른쪽 하위 트리  
``` java
public static void traverseInorder(Node node) {
    if (node == null) {
        return;
    }

    traverseInorder(node.left);
    System.out.println(node.data);
    traverseInorder(node.right);
}
```
2. 전위 순회 (pre-order)
현재노드 -> 왼쪽 하위 트리 -> 오른쪽 하위 트리  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/3660c072-07c9-4d7d-95ae-4e443a29f02d)  

용도1 : 트리 복사  
부모가 있어야 자식도 추가할 수 있음.  
따라서 전위 순회가 적합함 (부모 먼저 나열하니까)  
다른 순회로도 복사는 가능하지만, 직관적이진 않다.  

용도2 : 수식의 전위 표기법  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/5808154b-4773-4330-8c58-6dcacfc5dcdd)  

3. 후위 순회 (post-order)
왼쪽 하위 트리 -> 오른쪽 하위 트리 -> 현재 노드  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/234b257d-ee98-440e-a986-8cacf406aa79)  

앞에서 본 예 외에도 알고리듬에 따라 셋 중 하나는 사용!  

가이드!  
리프보다 루트를 먼저 봐야하면 전위 순회  
리프본 다음 다른 노드 봐야하면 후위 순회  
순서대로 봐야하면 중위 순회  

하위 트리와 비교했을 때 현재 노드의 방문 순서임.  

코드보기 : 전위 순회, 깊은 트리 복사  

## 레드-블랙 트리
각 노드가 레드 혹은 블랙. 노드에 저장하는 데이터가 아님.  
그냥 1비트짜리 추가 정보 (굳이 빨/검이 아니어도 됨)  

스스로 균형을 잡는 트리 (self-balancing tree)  
그걸로 트리 높이를 최소로 보장.  
균형을 잡는 시점은 사입과 삭제시.  
그 외 연산은 BST와 동일함 (단, 탐색 속도가 BST보다 빠를 것임)  

* 레드-블랙 트리의 특성  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/345b9443-f6ff-4ed0-aef9-35ef8067fac3)  
리프 노드는 데이터를 담지 않음(NIL)  
블랙 깊이(black depth): 루트와 어떤 노드 사이에 있는 블랙 노드 수  
블랙 높이(black height): 어떤 노드와 리프 사이에 있는 블랙 수  
가장 큰 리프 깊이가 가장 작은 것의 2배를 넘지 않음 !!  
-> 이진 트리 연산 최악의 경우를 방지하여 O(logN)을 보장  
  C++의 std::map의 구현으로 일반적으로 사용되는 자료구조임.  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/98a344ae-bda4-4f3a-a21a-d7d7721d9820)  


레드-블랙 트리의 특성을 유지하려면 어떤 연산을 해야하는지가 중요함.  
탐색: 이진 탐색 트리와 같음. 단, O(logN) 보장됨  
삽입: 일단 무작정 삽입 혹은 삭제 (특성이 망가질 수 있음)  
그 후, 망가진 특성을 고치려 트리의 구조를 재배치(회전) 혹은 노드 색 바꿈.  
완벽하진 않지만, 탐색 시간 O(logN)을 보장할 정도의 균형!  
모두 O(longN). 트리 회전, 색바꾸기: O(1)  

삽입, 삭제 원리를 정확히 아는건 힘든 일이므로, 최소한의 감을 잡도록 함.  
몇 가지 문제를 해결하며 패턴을 정리해볼것임.  

### 레드-블랙 트리의 삽입 방법
1. BTS와 똑같이 삽입
단, 새로 삽입하는 노드는 언제나 레드.  
언제나 리프에 추가되니 아래 연산이 간단해짐.  

2. 레드-블랙 트리 조건을 만족하도록 재귀적으로 고침
재귀 방향: 리프로부터 위로 올라가면서.  
고칠때 tree rotation이나 색깔 바꾸기 두 가지 기법을 사용함.  
총 4가지 상황(패턴)에 따라 트리 회전, 색깔 바꾸기 기법을 다르게 적용함.  
전략 4가지는 외울 필요는 없고, 필요할 때 마다 찾아서 쓰면 됨.  

### 레드-블랙 트리의 삭제 방법
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/a809d704-2ba2-4bd4-b3f9-49bba72d48b7)  




