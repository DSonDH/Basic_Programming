# OO에서 재사용성을 주요시하는 이유
* Don't reinvent the wheel
이미 동작과 상태가 명확하고 설계구현테스팅까지 모두 마친 물체를 다시 만들지 말고,  
그냥 가져다 쓰자 !!  

클래스를 재사용하면 좋은 점
1. 설계와 코딩에 드는 시간 절약
근데 재사용하기 어려운 건데도, 재사용해버리는 경우가 있긴 함.  
미래에 어떻게 변할지 완전히 예측 불가한데 미리 만든다고 가독성, 유지보수성 떨어뜨릴 수 있음.  
즉 주관적인 동료간에 상식의 밸런스를 맞춰야 함.  

2. 테스트에 걸리는 시간 절약
이미 테스트까지 끝낸 클래스를 다시 테스트할 필요가 없음.  
하지만, 새로운 버그를 찾을 지도 모름.  
자식클래스 추가하다 보니, 부모 클래스를 변경하는 경우도 생길 수 있음.  
그래도 부모 클래스 테스트 좀 했으면, 나중에 조금 덜 테스트해도 될것임.  

3. 관리 비용 절약
코드 중복이 없고, 관련 코드가 모두 한 파일 안에 있음.  
재사용성 vs 유지관리 밸런스가 중요함.  

## OO모델링 실력 높이는 법  
많은 연습 해보면 됨.  
다른 사람의 코드를 많이 사용해보고, 코드리뷰 주고받아야 함.  

# 상속 vs 컴포지션 선택 시 4가지 기준

상속, 컴포지션 모두 재사용성이 목적임.  
대부분의 경우에는 둘 다 가능함.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/3f4e7ff0-7353-4652-9e3f-4c9a6d9b973a)  
속이 빈 다이아몬드는 집합(aggregation)을 표현할 때 사용합니다. 컴포지션은 속이 찬 다이아몬드가 맞습니다.  

둘 중 하나를 고를 원칙은 ?  
4가지가 있음 !!  

## 1. 기계상의 차이 때문에 하나를 골라야 할 때
메모리 문제. 용량의 문제는 아님.  
개체 생성 시, 메모리가 하나의 덩어리임.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/bba94f59-c88e-4b2c-8440-bbded8df2423)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/1bbc7dec-ba60-45de-80b0-057206df137f)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/8eac39f6-7429-4f5c-bd52-0118540f8906)  

실행 성능에 영향을 미치게 됨.  
프로그램 실행 중 첫 번째 병목점  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/16a06b72-26bf-47af-97e8-6134dc3adb2f)  

두 번째 병목점  
새로운 메모리 할당(new)와 해제(delete, release)  
프로그래밍 언어 따라 이 둘중에 특히 느린 것이 있음.  
상속은 메모리 할당과 해제가 딱 한번씩.  
컴포지션은 한번 + 부품 수 만큼씩.  

## 2. 용도 때문에 상속을 고를 수밖에 없을 때 (다형성)
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/82c16a8c-185b-44bb-b599-29f1ae59dc99)  
다형성 구현 할려면 상속이 필수임.  

## 3. 관리의 효율성을 고려할 때
1. 상속이 더 나은 이유  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/0a7c91f5-c249-4b51-919c-4aae0050d1c7)  

2. 컴포지션이 더 나은 이유
깊은 상속할 때, 상위 클래스 하나 바꾸면 아래 모든 subclass들 테스트 추가로 해야함.  
즉 상속은 변화에 자유롭지 못한 단점이 있음 !  
컴포지션도 비슷한 문제가 있으나 상속보다는 덜함.  
나중에 인터페이스나 다형성이 이런 문제를 조금 완화!!  

## 그 외 일반적인 상황
상식적으로 생각할 것.  
has-a, is-a 관계에 충실해야 함.  
데스크톱 구현을 예로 들면,  
모니터와 본체가 분리 : 컴포지션.  
노트북처럼 모니터와 본체가 하나면 상속임.  

```java
// Graphic.java
package academy.pocu.comp2500samples.w07.graphics;

public class Graphic {
    protected String label;

    public Graphic(String label) {
        this.label = label;
    }

    public String getLabel() {
        return this.label;
    }

    public void setLabel(String label) {
        this.label = label;
    }
}

// Point.java
package academy.pocu.comp2500samples.w07.graphics;

public class Point extends Graphic {
    private int x;
    private int y;

    public Point(String label, int x, int y) {
        super(label);
        this.x = x;
        this.y = y;
    }

    public int getX() {
        return this.x;
    }

    public int getY() {
        return this.y;
    }

    public void draw() {
        System.out.printf("Draw point '%s'%s",
                this.label,
                System.lineSeparator());
    }
}

// Line.java
package academy.pocu.comp2500samples.w07.graphics;

public class Line extends Graphic {
    private Point p1;
    private Point p2;

    public Line(String label,
                Point p1,
                Point p2) {
        super(label);
        this.p1 = p1;
        this.p2 = p2;
    }

    public double getLength() {
        int xDiff = this.p1.getX() - this.p2.getX();
        int yDiff = this.p1.getY() - this.p2.getY();

        return Math.sqrt(xDiff * xDiff + yDiff * yDiff);
    }

    public void draw() {
        System.out.printf("Draw line '%s'%s",
                this.label,
                System.lineSeparator());
    }
}

// Circle.java
package academy.pocu.comp2500samples.w07.graphics;

public class Circle extends Graphic {
    private Point center;
    private int radius;

    public Circle(String label,
                  Point center,
                  int radius) {
        super(label);
        this.center = center;
        this.radius = radius;
    }

    public double getCircumference() {
        return 2 * radius * Math.PI;
    }

    public double getArea() {
        return Math.PI * radius * radius;
    }

    public void draw() {
        System.out.printf("Draw circle '%s'%s",
                this.label,
                System.lineSeparator());
    }
}

// Picture.java
// Graphic개체를 상속받기도 하고, 컴포지션으로 가지기도 함 ! 
package academy.pocu.comp2500samples.w07.graphics;

import java.util.ArrayList;

public class Picture extends Graphic {
    private ArrayList<Graphic> graphics;

    public Picture(String label) {
        super(label);
        
        this.graphics = new ArrayList<>();
    }

    public void add(Graphic graphic) {
        this.graphics.add(graphic);
    }

    public void draw() {
        int count = this.graphics.size();

        if (count <= 0) {
            return;
        }

        System.out.printf("Draw picture '%s'%s",
                this.label,
                System.lineSeparator());

        for (int i = 0; i < count; ++i) {
            Graphic g = this.graphics.get(i);
            Class c = g.getClass();
            String className = c.getSimpleName();

            switch (className) {
                case "Circle":
                    ((Circle) g).draw();
                    break;

                case "Point":
                    ((Point) g).draw();
                    break;

                case "Line":
                    ((Line) g).draw();
                    break;

                case "Picture":
                    ((Picture) g).draw();
                    break;

                default:
                    String message = String.format("Unknown graphic type %s", className);
                    throw new IllegalArgumentException(message);
            }
        }
    }
}

// Program.java
package academy.pocu.comp2500samples.w07.graphics;

public class Program {
    public static void main(String[] args) {
        Point p1 = new Point("Point 1", 2, 7);
        Point p2 = new Point("Point 2", 1, 8);

        p1.draw();
        p2.draw();

        System.out.println("----------------------------");

        Line l1 = new Line("Line 1", p1, p2);

        l1.draw();

        System.out.println("----------------------------");

        Circle c1 = new Circle("Circle 1", p1, 5);
        Circle c2 = new Circle("Circle 2", p2, 10);

        c1.draw();
        c2.draw();

        System.out.println("----------------------------");

        Picture pic1 = new Picture("Picture with a line and a circle");

        pic1.add(c1);
        pic1.add(l1);

        pic1.draw();

        System.out.println("----------------------------");

        Picture pic2 = new Picture("More complicated pic");

        pic2.add(pic1);
        pic2.add(c2);

        pic2.draw();

        System.out.println("----------------------------");

        Picture pic3 = new Picture("Even more complicated pic");

        pic3.add(pic1);
        pic3.add(pic2);

        pic3.draw();
    }
}
```

## 상속과 잦은 클래스 변경할 때
* 엔티티 컴포넌트 시스템 (Entity Component System, ECS)  
프로그래머가 컴포지션을 선호하는 또 다른 예.  
코드 변경 없이 자유롭게 개체를 만들 수 있도록 하는게 목적.  
아키텍처 패턴 중 하나 (디자인 패턴과 비슷하지만 다른것)  
게임 업계에서 많이 씀 (Unity3D 의 게임 오브젝트 등)  

현실적으로 이것 저것 조합해서 구현해서 어떤게 가장 나은지 실제로 경험해봐야 함.  
-> 재컴파일 없이 게임 기획자가 원하는 대로 개체를 조랍하고싶음 !!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/7b8d69c1-55fb-41ef-875b-dac0f07fe577)  
1..* : 못해도 하나의 컴포넌트를 추가한다.  
컴포넌트 조합에 따라서 NPC냐 플레이어냐 조합이 됨.  
Component::update() 메서드는 각 클래스들이 다른 동작으로 바꿈. 이게 바로 다형성임!!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/2244cad4-4b02-44c7-93da-96edf2db254a)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/8a2ff933-59d7-4d52-aadb-85e893e79b7e)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/47e5862b-a9dc-4a21-b174-0ea6880b4787)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/046a73d1-00b0-4781-ba4b-12e3f17a3ec2)  

이제, 기획자는 GUI같은걸로 원하는 옵션 선택해서 테스트하면 됨 !  

``` java
// GameObject.java
package academy.pocu.comp2500samples.w07.entitycomponentsystem;

import java.util.ArrayList;

public class GameObject {
    private String name;
    private ArrayList<Component> components = new ArrayList<Component>();

    public GameObject(String name) {
        this.name = name;
    }

    public void addComponent(Component component) {
        components.add(component);
    }

    public void update() {
        System.out.printf("Update GameObject '%s'%s",
                this.name,
                System.lineSeparator());

        for (Component component : this.components) {
            component.update();
        }

        System.out.printf("Updating '%s' complete%s",
                this.name,
                System.lineSeparator());
    }
}

// Component.java
package academy.pocu.comp2500samples.w07.entitycomponentsystem;

public class Component {
    public void update() {
    }
}

// AiComponent.java
package academy.pocu.comp2500samples.w07.entitycomponentsystem;

public class AiComponent extends Component {
    public void update() {
        System.out.println("Updating AiComponent");
    }
}

// PhysicsComponent.java
package academy.pocu.comp2500samples.w07.entitycomponentsystem;

public class PhysicsComponent extends Component {
    public void update() {
        System.out.println("Updating PhysicsComponent");
    }
}

// EntityComponent.java
package academy.pocu.comp2500samples.w07.entitycomponentsystem;

public class EntityComponent extends Component {
    public void update() {
        System.out.println("Updating EntityComponent");
    }
}

// ControllableComponent.java
package academy.pocu.comp2500samples.w07.entitycomponentsystem;

public class ControllableComponent extends Component {
    public void update() {
        System.out.println("Updating ControllableComponent");
    }
}

// ComponentType.java
package academy.pocu.comp2500samples.w07.entitycomponentsystem;

public enum ComponentType {
    AI,
    PHYSICS,
    ENTITY,
    CONTROLLABLE
}


//개체 txt 파일을 Component로 역직렬화
// Batman.txt
Entity,Physics,Controllable

// ScaryVampire.txt
Entity,Physics,Ai

// Tree.txt
Entity

// Program.java
package academy.pocu.comp2500samples.w07.entitycomponentsystem;

import java.io.File;
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.List;

public class Program {
    public static void main(String[] args) {
        GameObject batman = loadGameObjectOrNull("Batman");
        batman.update();

        System.out.println();

        GameObject tree = loadGameObjectOrNull("Tree");
        tree.update();

        System.out.println();

        GameObject scaryVampire = loadGameObjectOrNull("ScaryVampire");
        scaryVampire.update();
    }

    private static GameObject loadGameObjectOrNull(String name) {
        String directory = getClassPath();
        String filename = String.format("%s.txt", name);
        Path filepath = Paths.get(directory, filename);
        File playerFile = new File(filepath.toString());

        if (!playerFile.isFile()) {
            return null;
        }

        List<String> lines;

        try {
            lines = Files.readAllLines(filepath,
                    StandardCharsets.UTF_8);
        } catch (IOException e) {
            e.printStackTrace();
            return null;
        }

        assert (lines.size() == 1) : "Player setting file is not in correct format!";

        String[] components = lines.get(0)
                .split(",", -1);

        GameObject obj = new GameObject(name);

        for (String c : components) {
            ComponentType type;

            try {
                type = ComponentType.valueOf(c.toUpperCase());
            } catch (IllegalArgumentException e) {
                e.printStackTrace();
                return null;
            }

            switch (type) {
                case AI:
                    obj.addComponent(new AiComponent());
                    break;

                case CONTROLLABLE:
                    obj.addComponent(new ControllableComponent());
                    break;

                case PHYSICS:
                    obj.addComponent(new PhysicsComponent());
                    break;

                case ENTITY:
                    obj.addComponent(new EntityComponent());
                    break;

                default:
                    return null;
            }
        }

        return obj;
    }

    private static String getClassPath() {
        File file = new File(Program.class.getProtectionDomain().getCodeSource().getLocation().getPath());
        String packageName = Program.class.getPackageName();
        packageName = packageName.replace('.', '/');

        Path path = Paths.get(file.getPath(), packageName);

        return path.toAbsolutePath().normalize().toString();
    }
}
```

