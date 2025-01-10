# 트라이, 공간분할 트리

* 단어 확인과 자동완성
단어들을 엄청 많이 담은 사전에서 내가 찾고자 하는 단어를 찾으려면?  
모든 단어들을 일이히 string compare할 수는 없다.  
모든 단어들을 hashmap으로 비교하기에는 해시충돌 문제도 있다.  
또한, 몇 글자만 쳐도 단어를 보여주는/자동완성 해주는 기능도 추가할 수 없다.  
이를 해결할 수 있는게 트라이.  

사전식 순서  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/58cea490-8959-4c19-a03e-6e5aa153fd6a)  
트리구조를 활용하면 된다!  

## 트라이 (trie)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/719ac249-267b-49c6-8f6f-f225473ecfe5)  
어쩐 집한 안에서 특정 키를 찾을 때 사용.  
키는 보통 문자열임.  
노드 사이의 견결이 한 글자로 결정됨. 키 전부가 아님!  
노드 위치 자체가 키를 정의함. 노드가 키 전체를 저장하지 않음! char 하나 저장함!  

사전데이터를 저장할 때 쓰임. 용량을 더 차지하지만, 탐색 속도는 향상됨.  
해시테이블 대신 사용가능!  
출돌이 없고, 해시 테이블보다 최악의 경우에 더 빠름 O(k)  
평균 O(1)이 아님. 표현하기 어려운 데이터형도 있음: float같은것  

## 공간분할 트리
지금까지 본 트리는 1차원 공간을 표현함. 즉 실체는 1차원 배열꼴이었음.  
2D나 3D를 다루는 트리가 공간분할 트리.  
영상처리, 게임, 영화, 설계 프로그램, 가상현실, 증강현실 등에서 주로 사용함.  

많은 물체 처리 문제
처리할 개체들은 차원이 높아질수록 기하급수적으로 늘어남.  
그래서 모든 공간을 처리하지 말고, 꼭 필요한 일부 공간만 처리하도록  
서브 공간을 정의해서 처리하면 효율적임.  

화면에 확실히 안 나올 물체들은 추려버림: 경계 상자, 경계 구 등 이용.  
안 추려진 물체들만 그래픽 카드에 요청.  

### 쿼드 트리(quad tree)  
깊이0: 전체 공간  
깊이1: 전체를 1/4로 나눈 공간  
깊이2: 전체를 1/16로 나눈 공간  
...
현재 내 화면이 나오는 최대 깊이와 해당 리프공간을 찾아서 그 영역에서만 연산 수행  

즉 쿼드 트리는 사분 트리라고도 하고,  
재귀적으로 2D공간을 분할함.  
각 노드가 4개의 자식을가짐.  

* 옥 트리(octree)와 기타 공간 분할 트리  
재귀적으로 3D공간을 분할.  
각 노드가 8개의 자식을 가짐. 3D프로그램에 종종 사용

*binary space partitioning, R tree, k-d tree, etc 도 있음.   

코드보기: 쿼드 트리  
``` java
// BoundingRect.java
package academy.pocu.comp3500samples.w07.quadtree;

public final class BoundingRect {
    private final Point topLeft;
    private final Point bottomRight;

    public BoundingRect(final Point topLeft, final int width, final int height) {
        assert (width >= 0);
        assert (height >= 0);

        this.topLeft = topLeft;
        this.bottomRight = new Point(
                topLeft.getX() + width, topLeft.getY() + height);
    }

    public int getWidth() {
        final int x1 = this.topLeft.getX();
        final int x2 = this.bottomRight.getX();

        return Math.abs(x1 - x2);
    }

    public int getHeight() {
        final int y1 = this.topLeft.getY();
        final int y2 = this.bottomRight.getY();

        return Math.abs(y1 - y2);
    }

    public Point getTopLeft() {
        return this.topLeft;
    }

    public Point getBottomRight() {
        return this.bottomRight;
    }

    public boolean contains(final Point point) {
        final int pX = point.getX();
        final int pY = point.getY();

        return pX >= this.topLeft.getX()
                && pX <= this.bottomRight.getX()
                && pY >= this.topLeft.getY()
                && pY <= this.bottomRight.getY();
    }

    public boolean contains(final BoundingRect other) {
        final int x1 = this.topLeft.getX();
        final int x2 = this.bottomRight.getX();
        final int y1 = this.topLeft.getY();
        final int y2 = this.bottomRight.getY();

        final int otherX1 = other.topLeft.getX();
        final int otherX2 = other.bottomRight.getX();
        final int otherY1 = other.topLeft.getY();
        final int otherY2 = other.bottomRight.getY();

        return x1 <= otherX1
                && x2 >= otherX2
                && y1 <= otherY1
                && y2 >= otherY2;
    }
}

// GameObject.java
package academy.pocu.comp3500samples.w07.quadtree;

public class GameObject {
    private final Point position;
    private final int data;

    public GameObject(final Point position, int data) {
        this.position = position;
        this.data = data;
    }

    public int getData() {
        return this.data;
    }

    public Point getPosition() {
        return this.position;
    }
}

// Point.java
package academy.pocu.comp3500samples.w07.quadtree;

public final class Point {
    private int x;
    private int y;

    public Point(final int x, final int y) {
        assert (x >= 0);
        assert (y >= 0);

        this.x = x;
        this.y = y;
    }

    public Point(Point other) {
        this.x = other.x;
        this.y = other.y;
    }

    public int getX() {
        return this.x;
    }

    public int getY() {
        return this.y;
    }
}

// Quadrant.java
package academy.pocu.comp3500samples.w07.quadtree;

import java.util.ArrayList;

public final class Quadrant {
    private static final int MIN_QUAD_DIMENSION = 2;

    private final BoundingRect boundingRect;

    private Quadrant topLeft;
    private Quadrant topRight;
    private Quadrant bottomLeft;
    private Quadrant bottomRight;

    private ArrayList<GameObject> gameObjects = new ArrayList<>();

    public Quadrant(final BoundingRect boundingRect) {
        this.boundingRect = boundingRect;

        createChildren();
    }

    public boolean insert(final GameObject gameObject) {
        final Point position = gameObject.getPosition();

        if (!this.boundingRect.contains(position)) {
            return false;
        }

        this.gameObjects.add(gameObject);

        if (this.topLeft != null) {
            this.topLeft.insert(gameObject);
            this.topRight.insert(gameObject);
            this.bottomLeft.insert(gameObject);
            this.bottomRight.insert(gameObject);
        }

        return true;
    }

    public ArrayList<GameObject> getGameObjects(final BoundingRect rect) {
        if (!this.boundingRect.contains(rect)) {
            return new ArrayList<>();
        }

        if (this.topLeft == null) {
            return this.gameObjects;
        }

        if (this.topLeft.boundingRect.contains(rect)) {
            return this.topLeft.getGameObjects(rect);
        }

        if (this.topRight.boundingRect.contains(rect)) {
            return this.topRight.getGameObjects(rect);
        }

        if (this.bottomRight.boundingRect.contains(rect)) {
            return this.bottomRight.getGameObjects(rect);
        }

        if (this.bottomLeft.boundingRect.contains(rect)) {
            return this.bottomLeft.getGameObjects(rect);
        }

        return this.gameObjects;
    }

    private void createChildren() {
        final int width = this.boundingRect.getWidth();
        final int height = this.boundingRect.getHeight();

        if (width < 2 * MIN_QUAD_DIMENSION
            || height < 2 * MIN_QUAD_DIMENSION) {
            return;
        }

        int x1 = this.boundingRect
                .getTopLeft()
                .getX();
        int y1 = this.boundingRect
                .getTopLeft()
                .getY();
        int x2 = this.boundingRect
                .getBottomRight()
                .getX();
        int y2 = this.boundingRect
                .getBottomRight()
                .getY();

        int midX = (x1 + x2) / 2;
        int midY = (y1 + y2) / 2;

        Point p1 = new Point(x1, y1);
        Point p2 = new Point(midX, midY);

        BoundingRect rect = new BoundingRect(p1,
                p2.getX() - p1.getX(),
                p2.getY() - p1.getY());

        this.topLeft = new Quadrant(rect);

        p1 = new Point(midX, y1);
        p2 = new Point(x2, midY);
        rect = new BoundingRect(p1,
                p2.getX() - p1.getX(),
                p2.getY() - p1.getY());

        this.topRight = new Quadrant(rect);

        p1 = new Point(x1, midY);
        p2 = new Point(midX, y2);
        rect = new BoundingRect(p1,
                p2.getX() - p1.getX(),
                p2.getY() - p1.getY());

        this.bottomLeft = new Quadrant(rect);

        p1 = new Point(midX, midY);
        p2 = new Point(x2, y2);
        rect = new BoundingRect(p1,
                p2.getX() - p1.getX(),
                p2.getY() - p1.getY());

        this.bottomRight = new Quadrant(rect);
    }
}

// Program.java
package academy.pocu.comp3500samples.w07.quadtree;

import java.util.ArrayList;

public class Program {
    public static void main(String[] args) {
        final Point p1 = new Point(1, 4);
        final GameObject gameObject1 = new GameObject(p1, 1);

        final Point p2 = new Point(7, 9);
        final GameObject gameObject2 = new GameObject(p2, 2);

        final Point p3 = new Point(5, 5);
        final GameObject gameObject3 = new GameObject(p3, 3);

        final Point p4 = new Point(3, 4);
        final GameObject gameObject4 = new GameObject(p4, 4);

        final Point p5 = new Point(2, 7);
        final GameObject gameObject5 = new GameObject(p5, 5);

        final Point p6 = new Point(9, 3);
        final GameObject gameObject6 = new GameObject(p6, 6);

        Point topLeft = new Point(0, 0);

        BoundingRect rect = new BoundingRect(topLeft, 10, 10);
        final Quadrant root = new Quadrant(rect);

        root.insert(gameObject1);
        root.insert(gameObject2);
        root.insert(gameObject3);
        root.insert(gameObject4);
        root.insert(gameObject5);
        root.insert(gameObject6);

        topLeft = new Point(0, 1);
        rect = new BoundingRect(topLeft, 4, 3);

        ArrayList<GameObject> gameObjects = root.getGameObjects(rect);

        print(gameObjects);

        topLeft = new Point(5, 8);
        rect = new BoundingRect(topLeft, 1, 1);

        gameObjects = root.getGameObjects(rect);

        print(gameObjects);

        topLeft = new Point(6, 3);
        rect = new BoundingRect(topLeft, 3, 1);

        gameObjects = root.getGameObjects(rect);

        print(gameObjects);
    }

    private static void print(ArrayList<GameObject> gameObjects) {
        System.out.println("--------------------");
        for (int i = 0; i < gameObjects.size(); ++i) {
            GameObject obj = gameObjects.get(i);
            System.out.println(String.format("%d. [%d] (%d, %d)",
                    i + 1,
                    obj.getData(),
                    obj.getPosition().getX(),
                    obj.getPosition().getY()));
        }

        System.out.println(String.format("Count: %d", gameObjects.size()));

        System.out.println("--------------------");
    }
}
```
