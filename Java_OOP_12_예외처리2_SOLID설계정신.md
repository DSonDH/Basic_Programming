# 잘못된 예외 처리 가이드를 조심하자! 

아직도 대부분의 프로그램은 모든 예외로부터 회복해야한다고 말하는 웹사이트가 많음.  
근래에는 실행중인 프로세스가 사라지면 다시 실행하도록 설정 가능함.  
그리고 각 프로그램 마다 별도의 가상 메모리가 제공되어  
프로그램 크래시가 기계 크래시로 이어지지 않음.  

근데, 이걸 무시하고 exceptionm safe 프로그래밍 시도하다가 오작동하면,  
좀비 프로그램 생김 ...  C++언매니지드 프로그래밍에서 배움.  

## 제어 흐름용으로 예외를 사용하지 말 것
goto와 개념이 같은데, 함수 범위에서 점프하는게 아니라 호출 스택 어디로도 점프 가능.  
더 고차원적인 스파게티코드 ...  
다음에 실행할 코드를 결정하는 용도로 쓰지 말 것 !!!!!!!!!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/cac237b3-8c12-4117-8ca6-da6aae90920d)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/d25c0e65-d155-4cff-9761-bb78d044d296)  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/17b81575-1889-41b6-9c34-0171f4870233)  

## 예외적인 상황에만 예외를 사용해야 하는 경우
예외는 오류상황이라는 전체하에 모든 툴이 개발되어 있으므로.  
프로그래머가 기억해야 할 교훈 한 가지 : 할 수 있다고 다 해야 하는 건 아니다.  
원래 방법이 가지는 혜택을 포기하고서 hack을 써야할 이유가 업음.  
예 : Intellij가 예외 발생하면 디버그 모드에서 예외 발생하면 중단점 자동으로 걸어주는데,  
예외 때문에 쓸모없는데에 자꾸 중단점 걸림.  

# 올바른 오류 처리 방법

## 오류 상황, 예외 상황
프로그램은 기본적으로 happy path를 따름.  
이 happy path가 아닌 경우가 생기기도 함.  
error condition(오류 상황), exceptional condition(예외 상황) 이라 함.  
근데 예외 상황이 프로그래밍 언어의 Exception을 의미하는 경우도 있음.  

오류 상황에 빠지면 프로그램을 어떻게 진행할까 ?  
그걸 결정하는게 오류 처리방법. 예외 던지고 처리하는 것도 그중 일부.  

* 오류 상황은 예측 가능한 상황을 의미함.  
* 프로그램 실행 중에 기본적으로 일어나지 않는 일  
* 하지만 여전히 일어날 수 있는 일.  
따라서 이런 상황을 처리하는 코드는 프로그램 기능의 일부임.  

그러나, 프로그래머가 미리 예측치 못했다면?  
처리 코드가 있을 수 없음. 이를 버그라 함!!  
버그 발결 후, 제대로 처리하는 코드를 추가 -> 다시 빌드  

## 4가지 오류 상황 처리법
1. 무시
2. 종료
문제를 일으킬 수 있는 상황이 있는지 검사하고, 그렇다면 프로그램 종료  
3. 수정
문제를 일으킬 수 있는 상황이 있는지 검사하고, 그렇다면 실수를 고친 뒤  
계속 프로그램을 실행되게 한다.  
4. 예외

1,2,3dms Java탄생 전 부터 많이 쓰던 방법.  
4는 OO언어가 나올 즈음부터 많이 사용하기 시작.  
4번은 어느 누구도 정립 못했음 ㄷㄷ  

훌륭한 프로그래머는, 문제 해결에 가장 적합한 방법을 뭐든간에 사용함.  
4가지 방법마다 다 적합한 상황이 있음.  

## 오류 상황을 피하는게 최고
처음부터 문제 없는 코드가 최고!  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/19260e6c-2f2c-49b2-ba4b-4606998c49f4)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/85a30873-f73e-4c0c-a8e5-b67dce783c9e)  

남에게 문제를 알려주는 방법.  
1. boolean or null 반환.
2. 오류코드 (int or enum) 반환.
3. 예외를 던짐.

### '무시'와 '종료' 방법
무시한다.  
1. 곧바로 크래시
2. 일단은 작동하지만 언젠가는 크래시
3. 안정적이지 못한 상태로 계속 동작함

1번 2번이 블루스크린  
3번은 조금 위험함. 데이터가 망가지면 올바르지 않은 결과가 나올 수 있음.  

미리 검사 후 프로그램 종료
어떤 문제가 있었는지 사용자에게 팝업 창이나 log파일 보여주고 정상 종료.  
C#: Application.Exit()호출, Java: System.exit(int) 호출  
사용자는 '그런 문제가 있었군' 이라 생각하고 다시 프로그램을 실행.  

크래시에 비해 나은점 :  
제대로 시스템 상태를 정리하고 프로그램을 종료할 가능성이 높음.  
따라서 프로그램 종료 후 시스템이 좀 더 안정적일 가능성이 높음.  
무었보다, 작업하던 내용을 날리지 않고 저장해 줄 수 있음.  

### '수정'과 '예외' 방법
미리 검사 후 문제를 고친다  
UX 고려시 사용자에게 올바른 값을 입력하라고 다시 요청  
OO랑은 거리가 조금 멀어질 순 있으나, UX를 포기하면서까지 OO를 계승할 이유가 없음.  
또한, 예외는 다른 방법에 비해 성능이 가장 느림. (C로 구현하려 하면 .. 복잡복잡 ㄷㄷ)  
결론 : 설계와 필요한 성능 수준에 따라 OO에서도 충분히 좋은 방법.  
단점 :  
문제가 처음 발생한 곳 파악이 힘듦.  
문제가 발생한지도 모르고 시간이 오래 흐를 수 있음.  
예 : 파일 읽는 함수에서 파일을 못찾았는데 빈 문자열을 반환받으면,  
빈 파일 읽는 것과 다르지 않으므로 그 순간에는 올바른 방법 같지만,  
나중에 그 파일에 문자열을 덧붙이려고 하면 그건 불가능한 연산.  
프로그래머는 있던 파일이 사라졌다 생각할 수도 있음.  

예외를 던진다.  
이미 살펴봄.  
예외는 다음 두 가지를 지원.  
1. 문제가 발생했다는 사실을 알려줄 수 있음 (예외 던지기)  
2. 그 예외 처리 (예외를 catch 한 뒤 처리)
대부분의 OO언어는 예외를 지원

## 예외는 OO의 일부가 아니다.
예외 외에는 해결책이 없는 경우 : 생성자.  
이미 개체는 생성되었고, 반환형은 없으므로.  
문제가 발생했다는 사실을 알려주려면 예외가 유일한 방법.  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/6260d2aa-1c07-4d0b-ab70-a0828c47c72d)  
이것 또한 언어의 제약.  

## 잘못된 예외처리보다 크래시가 낫다
예외처리를 잘못하면 더 큰 문제가 생김.  
크래시가 안나고 프로그램이 계속 실행되면, 안정적이지 않게 계속 돔.  
크래시의 진정함 문제점은 작업물을 잃어버리는 것.  
근데 요즘은 자동 세이브가 잘 되어있음. 히스토리 무한 되돌리기도 되는걸?  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/47fc439f-5480-4560-948b-66611068ed28)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/c625e3a3-3861-441d-af48-6263fb1c1273)  
이에 반해,  
예외를 던지면 호출 스택 정보 (문자열), 메시지 (null인 경우가 빈번), 예외 형 이정도 정보 밖에 못얻음.  

## 프로그램 종료도 올바른 방법이다
좀비상태에 빠지는 것을 방지.  
크래시 보다도 좋음. 작업물 저장도 되고.  
요즘 사람들 그렇게 까탈스럽지 않더라 ..  

## 4가지 처리법의 순위
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/f68ed38c-3e8a-44b1-8a97-8b7d0c9e85ce)  
수정 : 호출자가 수정을 원치 않거나, 내가 잘못 고칠 수도 있어서 위험.  

![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/578e3b42-780e-42f8-b575-7c3b7fdcf04c)  
무시 : 대부분 크래시가 나기에 명백함. 단, 크래시가 안나면 예외보다 나쁨!  

## 예측 가능한 상황의 처리법
오류 상황을 예측했으면 오류 처리 코드가 있음 (기능)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/353fdf86-88f6-4a90-b21a-80651d3c3a85)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/cfc8c8ea-2f84-4a17-8e77-c24f46bab8b3)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/bb7cce56-0806-4b81-a561-17a93cc29fbf)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/0dd062a7-f454-4d79-b20c-d5f531c011ba)  
로그보다는 메모리 덤프가 낫다...  

## 예측 불가한 상황의 처리법
오류 상황을 예측 못했으면 오류 처리 코드가 없음 (버그)  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/aecd8228-19a8-440a-832a-f5f41a1a4c95)  

* 실행 중에 문제를 고치려 한다고 프로그램의 안정성이 높아지는 건 아니다. 좀비가 되면 그게 더 큰 문제!

# SOLID 설계 정신 (참고용. 중요하진 않음)
소프트웨어 설계를 이해하기 쉽고, 유연하고, 유지보수 쉽게하기 위한 방향성.  
알아주면 좋은 주관적인 내용일 뿐임.  
좀 극단적인 주장을 한 것도 있음.  
정확히 어느 경우에 어떻게 적용하는지 설명하지 않음.  
모든걸 SOLID에 맞게 설계하면 오히려 유지관리가 힘든 코드가 될 것임.  
유연해지기는 함. 대규모 프로젝트여서 디커플링이 중요할 때.  

따라서, 처음에는 직접적/구체적인 설계를 하다가, 규모가 커지면서  
유연성이 필요해지면 그때 바꿔갈 때 도움이 될 정신임.  
요즘 트렌드는 필요성이 마딱드리면 그제서야 대규모/유연한 설계를 수행하는 것.  
회사 내부 자체 개발팀이 있어서, 최대한 빠르게 첫 버전 만들고,  
필요에 따라 요구사항 고치고 종종 기능도 바꿈.  
툭하면 요구사항이 바껴서 재사용성 높은 설계가 힘듦.  

## Single-responsibility principle (단일 책임)  
* 클래스는 오직 한 가지 일만 해야 한다.  
* 클래스를 바꿀 상황이 생긴다면 바꾸려는 이유가 하나여야 한다.  

한 가지 일? 하나의 이유가 명확하지 않아서 비판 많이 받음.  
극단적 진영 : 클래스에 있는 함수가 4개를 넘으면 안된다. (4개는 주관적 내용임)  
- 사람이 한 번에 쉽게 이해할 수 있는 정보의 크기를 의미함.
- POCU제안 : 이 코드를 보는 대부분의 사람이 이해할 수 있는 크기로 클래스를 만들자!
- 주관적인 문제라, 팀 안에서 적당히 합의 봐야 함.
- 클래스 이름에 And가 들어가면 이 원칙이 깨짐을 나름 객관적으로 볼 수 있음.
- 메서드 이름도 마찬가지.

그럼, 두번째 내용인, 클래스 바꿀 단 하나의 이유에 대해 생각해보면 ...   
클래스를 바꿀 이유는 예측할 수 없으므로 개소리임.  
다만, 궂이 교훈을 끌어내보면, 각 클래스의 책임을 분명하게 정의하자는 뜻임.  
그러면 어떤 오류 상황이 있을 때 대응이 쉬움.  
그 오류를 검사하고 처리해야 하는 곳이 명확함.  

## Open-closed principle (개방-폐쇄)
확장은 가능하게, 그러나 수정은 불가능하게.  
* 클래스 내부 수정 없이 동작을 확장할 수 있어야 한다는 의미.
이 정신을 지키려면 상속, 다형성을 잘 써야함.
단일 책임 정신도 동시에 만족시킬 가능성이 높다.  

다만, 융통성 없이 따르면 노답인게,  
한번 만든 클래스는 절대로 바꾸면 안된다고 생각하면,  
![image](https://github.com/DSonDH/Basic_Programming/assets/15919242/eef4a90a-48db-4414-95bc-9f5987f3dc15)  

또 다른 경우 : 스펙이 바뀌는 경우.  
더이상 안쓰는 A를 고쳐? 아님 A를 두고 AA를 새로 만들어?  
보통은 A가 정상임.  

모든 문제를 프로그래밍으로 풀지 말것.  
외부 도구로 해결할 일을 자꾸 내 코드로 해결하려고 하면 일이 꼬임.  

## Liskov substitution principle (리스코프 치환)
부모 클래스의 개체를 사용하는 코드 A가 있음.  
나중에 자식 클래스의 개체를 거기에 대신 사용함 (치환)  
이때 A가 아무 문제없이 작동해야 한다.  

즉 부모가 할 수 있는 일은 자식도 다 할 수 있어야 함.  
상속을 깊게 하면, 이런 정신 지켜주면 실수는 좀 막을 수 있음.  
하지만, 100% 이렇게 되지는 않음.  

```Java
// is-a 관계일때만 상속을 구현하는게 올바르다는 것을 말하면서
// 리스코프 치환 개념에 위배되는 사례
// stack이 arraylist를 상속받아 만드는게 올바른 방법이 아닌 것임.

package academy.pocu.comp2500samples.w13.stack;

import java.util.ArrayList;

public final class Stack<E> extends ArrayList<E> {
    @Override
    public void add(int index, E element) {
        super.add(element);
    }

    @Override
    public E remove(int index) {
        assert this.size() > 0;

        int lastIndex = size() - 1;
        E element = get(lastIndex);

        super.remove(lastIndex);

        return element;
    }

    @Override
    public boolean remove(Object o) {
        if (this.size() == 0) {
            return false;
        }

        remove(0);

        return true;
    }
}

package academy.pocu.comp2500samples.w13.stack;

import java.util.ArrayList;

public class Program {
    public static void main(String[] args) {
        Stack<Integer> stack = new Stack();

        stack.add(1);
        stack.add(2);
        stack.add(3);
        stack.add(4);
        stack.add(5);

        while (!stack.isEmpty()) {
            int num = stack.remove(0);
            System.out.println(num);
        }

        System.out.println("-----------------");

        ArrayList<Integer> list = new ArrayList<>();

        addInOrder(list, 10);
        addInOrder(list, 2);
        addInOrder(list, 5);

        for (int num : list) {
            System.out.println(num);
        }

        System.out.println("-----------------");

        list = new Stack<>();

        addInOrder(list, 10);
        addInOrder(list, 2);
        addInOrder(list, 5);

        for (int num : list) {
            System.out.println(num);
        }
    }

    private static void addInOrder(ArrayList<Integer> list, int num) {
        int i;

        for (i = 0; i < list.size(); ++i) {
            if (list.get(i) > num) {
                break;
            }
        }

        list.add(i, num);
    }
}
```

## Interface segregation principle (인터페이스 분리)
큰 인터페이스 몇 개 있는 것보단 작은 인터페이스가 많이 있는 게 좋다.  

이것도 이해할 수 있는 코드 크기에 대한 얘기임.  
1메서드당 1인터페이스 할건지, 인터페이스 없게 할건지,  
내 그룹의 평균치를 내서 원칙으로 삼기.  

## Dependency inversion principle (의존 역전)
개체끼리 통신할 때 구체적인 것 말고 추상적인 것에 의존하란 이야기.  
- POCU가 제안하는 인터페이스를 어디에 사용해야 하는지에 대한 가이드를 따르면 됨.  

