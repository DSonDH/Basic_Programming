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
게임 AI를 직접 구현하고자 할 때, 현재 판을 보고 다음 액션을 결정하고자 함.  
이때 모든 경우으이 수를 보여주기 적합한 자료구조는  
트리임!!  

전략  
1. 상대방이 이길 수 있는 구성을 주지 않는다.
2. 그러나 내가 이길 수 있는 가능성을 열어둔다.
상대방의 최대 이득이 나는 경우를 최소화 한다.  
= 내 최대 손실이 나는 경우를 최소화 한다!  

손실에 대한 함수를 작성함.  
ex: 내가 이기면 +10점, 비기면 0점, 상대가 이기면 -10점  

최악의 경우 발생할 수 있는 손실을 최소화하려는 규칙  
게임이론, 결정이론, 통계학, 철학 등에서 널리 사용  
최초의 AI체스 월드 챔피언 Deep Blue가 사용한 알고리듬  
(현재 챔피언은 기계학습 알고리듬, 여전히 미니맥스기반 알고리듬도 상위권)  
제로섬 (zero-sum) 게임의 결정 알고리듬으로 적합  
n명이 참가하는 제로섬 게임이론에서 시작한 알고리듬  
여전히 어떤 제로섬 게임에도 적용하기 적합  

미니맥스 알고리듬의 가정  
상대방도 최적의 결정을 내림: 상대방도 이기는 게 목표, 랜덤하게 플레이하지 않음.  
게임이 순수히 전략적이어야 함: 운 요소 없어야 함. 운 까지 고려하는 변형 알고리듬도 있긴 함.  

## 틱택토 평가 함수
깊이 3에서,  결과에 따른 점수:  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/e651c4a2-25e3-4de7-901b-b7fc5823d4c8)  

깊이 2에서, 결과에 따른 점수:  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/48f9a873-a775-4b4e-82f1-51a231d6d239)  

깊이 1에서, 결과에 따른 점수:  
전략: 가운에 옵션 중에서, 상대가 이길 수 있는 경우가 있으므로 적절하지 않음.  
이러면 최소 점수를 취해오면 상대가 이길 수 있는 경우가 있다는 개념이 반영이 됨.  
즉 MIN을 취함  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/29d13b96-b097-43a6-bc5e-55754e3cf883)  

이 MIN 결과들 중에서 MAX를 취해서 그 경로를 내 전략으로 취한다.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c290f201-3d49-42cd-a183-6c70f51680db)  

!!!!!! 상대가 수를 놓는 상황은 MIN, 내가 수를 놓는 상황은 MAX를 취한다.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/9a62ef7e-7ce0-451e-8e8f-0e2e200deaae)  

## 깊이 제한 미니맥스
체스 같은 좀 복잡한 게임은 첫 수에서 연산을 가장 많이 필요로하게 됨.  
게임 트리를 전부 훑을 수 없는 경우  
특정 깊이까지만 게임 트리를 만듦.  
마지막 깊이에서 점수를 계산해야 함.  
평가함수(evaluation function)을 효율적이고 빠르게 구현할줄 아는게 핵심!  
: 확실히 승/패가 결정 안 난 상황이라 근사치를 구해야 함.  
"현재 보드 상태가 나에게 얼마나 유리한가 ??!!"  

## 미니맥스 알고리듬의 성능  
1. 점수 계산 함수가 얼마나 뛰어난가?  
상대가 못보는 점수 계산법이어야 함. 남들이 알면 나와 같은 전략이 되어버리므로.  
같은 깊이를 한계적으로 보더라도 좀 더 실제 정답에 가까워야 함.  
2. 얼마나 깊이 볼 수 있는가?  
최적화를 더 잘해서 더 깊이 볼 수 있는 것.  
지금 보는 노드가 이전에 본 것 보다 별로인 것 같으면 중단 (alpha-beta pruning)  

코드보기: 틱택토
``` java
// Move.java
package academy.pocu.comp3500samples.w09.tictactoe;

public class Move {
    private int index;
    private int score;

    public Move(final int index, final int score) {
        this.index = index;
        this.score = score;
    }

    public int getIndex() {
        return this.index;
    }

    public int getScore() {
        return this.score;
    }
}

// Player.java
package academy.pocu.comp3500samples.w09.tictactoe;

public enum Player {
    X,
    O
}

// TicTacToe.java
package academy.pocu.comp3500samples.w09.tictactoe;

import java.util.ArrayList;

public class TicTacToe {
    public static final int BOARD_SIZE = 9;

    private TicTacToe() {
    }

    public static int getBestMoveIndex(final Player[] board, final Player player) {
        assert (board.length == BOARD_SIZE);

        Player opponent = player == Player.O
                ? Player.X : Player.O;

        Move move = getBestMoveRecursive(board,
                player,
                opponent,
                player);

        return move.getIndex();
    }

    private static Move getBestMoveRecursive(final Player[] board, final Player player, final Player opponent, final Player turn) {
        assert (board.length == BOARD_SIZE);

        if (hasWon(board, opponent)) {
            return new Move(-1, -10);
        }

        if (hasWon(board, player)) {
            return new Move(-1, 10);
        }

        ArrayList<Integer> availableIndexes = getEmptyIndexes(board);
        if (availableIndexes.isEmpty()) {
            return new Move(-1, 0);
        }

        ArrayList<Move> moves = new ArrayList<>();

        for (int i = 0; i < availableIndexes.size(); ++i) {
            int index = availableIndexes.get(i);

            Player[] newBoard = copyBoard(board);

            newBoard[index] = turn;

            Player nextPlayer = turn == player
                    ? opponent : player;

            int score = getBestMoveRecursive(newBoard,
                    player,
                    opponent,
                    nextPlayer)
                    .getScore();

            Move move = new Move(index, score);
            moves.add(move);
        }

        if (turn == player) {
            return getMaxScoreMove(moves);
        }

        return getMinScoreMove(moves);
    }

    private static Move getMaxScoreMove(final ArrayList<Move> moves) {
        assert (!moves.isEmpty());

        Move bestMove = moves.get(0);
        for (int i = 1; i < moves.size(); ++i) {
            if (moves.get(i).getScore() > bestMove.getScore()) {
                bestMove = moves.get(i);
            }
        }

        return bestMove;
    }

    private static Move getMinScoreMove(final ArrayList<Move> moves) {
        assert (!moves.isEmpty());

        Move bestMove = moves.get(0);
        for (int i = 0; i < moves.size(); ++i) {
            if (moves.get(i).getScore() < bestMove.getScore()) {
                bestMove = moves.get(i);
            }
        }

        return bestMove;
    }

    private static Player[] copyBoard(final Player[] board) {
        assert (board.length == BOARD_SIZE);

        Player[] newBoard = new Player[board.length];

        for (int i = 0; i < board.length; ++i) {
            newBoard[i] = board[i];
        }

        return newBoard;
    }

    private static ArrayList<Integer> getEmptyIndexes(final Player[] board) {
        assert (board.length == BOARD_SIZE);

        ArrayList<Integer> indexes = new ArrayList<>();

        for (int i = 0; i < board.length; ++i) {
            if (board[i] == null) {
                indexes.add(i);
            }
        }

        return indexes;
    }

    private static boolean hasWon(final Player[] board, final Player player) {
        assert (board.length == BOARD_SIZE);

        return (board[0] == player && board[1] == player && board[2] == player)
                || (board[3] == player && board[4] == player && board[5] == player)
                || (board[6] == player && board[7] == player && board[8] == player)
                || (board[0] == player && board[3] == player && board[6] == player)
                || (board[1] == player && board[4] == player && board[7] == player)
                || (board[2] == player && board[5] == player && board[8] == player)
                || (board[0] == player && board[4] == player && board[8] == player)
                || (board[2] == player && board[4] == player && board[6] == player);
    }
}

// Program.java
package academy.pocu.comp3500samples.w09.tictactoe;

public class Program {
    public static void main(String[] args) {
        {
            Player[] board = new Player[TicTacToe.BOARD_SIZE];

            int index = TicTacToe
                    .getBestMoveIndex(board,
                            Player.X);

            System.out.println(String.format("best move index: %d", index));
        }

        {
            Player[] board = new Player[]{
                    null, Player.O, Player.X,
                    Player.X, Player.O, Player.O,
                    null, null, Player.X};

            int index = TicTacToe
                    .getBestMoveIndex(board,
                            Player.X);

            System.out.println(String.format("best move index: %d", index));
        }

        {
            Player[] board = new Player[]{
                    Player.O, null, Player.X,
                    Player.X, null, Player.X,
                    null, Player.O, Player.O};

            int index = TicTacToe
                    .getBestMoveIndex(board,
                            Player.X);

            System.out.println(String.format("best move index: %d", index));
        }
    }
}
```
