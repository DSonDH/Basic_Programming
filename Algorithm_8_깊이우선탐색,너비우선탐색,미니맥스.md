# 깊이 우선 탐색 (Depth First Search)  
내 자식들 중 한 쪽으로 리프까지 확인  
중위 순회와 매우 비슷: 재귀 함수로 쉽게 작성 가능.  
스택 자료구조로 비 재귀적으로도 구현 가능!  
간단한 미로 탈출하기 전략.  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/8f12f553-7c57-4755-9d9d-a728319edc8e)  

# 너비 우선 탐색 (Bredth First Search) 
여러 우물을 동시에 같은 깊이로!  
현재 깊이의 이웃 노드들을 먼저 방문.  
어느 한 가지부터 깊게 보지 않음.  
현재 노드보다 얕은 노드는 모두 방문했음!  
최단 경로 찾기에 적합함 (각종 경로들을 트리로 구현해서 BFS)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/a5c3d17f-0d23-4b47-a197-1a30f0529226)  

깊이우선 vs 너비우선  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/0256d401-9e93-460c-9827-afb5e4ebae97)  

그래프와 깊이/너비 우선 탐색  
그래프: 서로 연관 있는 노드의 집합.  
연관 있는 노드끼리 edge로 연결.  
부모/자식 관계를 요하지 않음.  
탐색을 수행할 때, 인접행렬에 방문했던 노드를 기억함.  

코드보기: 디렉터리 트리 출력하기
``` java
package academy.pocu.comp3500samples.w09.directorytree;

import java.io.File;

public class Program {
    private static final int INDENT_LENGTH = 2;

    public static void main(String[] args) {
        if (args.length != 1) {
            System.err.println(String.format("Wrong number of arguments: %d", args.length));
            System.exit(1);
        }

        String path = args[0];
        File file = new File(path);

        printDirectoryTreeRecursive(file, 0);
    }

    private static void printDirectoryTreeRecursive(File file, int depth) {
        String filename = file.getName();

        String message = String.format("- %s",
                filename);
        message = padLeft(INDENT_LENGTH * depth,
                message);

        System.out.println(message);

        if (file.isDirectory()) {
            File[] children = file.listFiles();

            for (File child : children) {
                printDirectoryTreeRecursive(child,
                        depth + 1);
            }
        }
    }

    private static String padLeft(int padLength, String message) {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < padLength; i++) {
            sb.append(' ');
        }

        sb.append(message);

        return sb.toString();
    }
}
```

# mini-max
