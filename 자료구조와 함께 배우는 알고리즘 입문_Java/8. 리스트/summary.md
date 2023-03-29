___
# 리스트
- 순서를 갖도록 데이터를 나열
- 스택과 큐도 리스트 구조

#### 선형 리스트(linear list)
데이터가 배열처럼 연속하는(linear) 메모리 공간에 저장되어 순서를 갖게 됨

#### 연결 리스트(linked list)
데이터가 메모리 공간에 연속적으로 저장되어 있지 않더라고 각각의 데이터 안에 다음 데이터에 대한 정보를 갖고 있어 서로 연결(linked)됨  
- from 머리노드 to 꼬리노드  
* 앞쪽노드(predecessor node) <- (노드) -> 다음 노드(successor node)

- 리스트에 있는 개별 요소 : 노드(node) having 1. 데이터 2. 다음 노드를 가리키는 포인터  

## 배열로 선형 리스트 만들기
삽입한 위치 이후의 모든 요소를 한 칸씩 뒤로 옮김
- 다음 노드 꺼내기 : 1만큼 큰 인덱스를 갖는 요소에 접근
- For 노드의 삽입과 삭제, check 쌓이는 데이터의 최대 크기 because 삽입 요소 이후의 모든 요소를 한 칸씩 뒤로 밀거나 + 삭제한 요소 이후의 모든 요소를 앞으로 당기니까 

___
# 포인터로 연결 리스트 만들기
- 다음 노드를 가리키는 포인터를 각 노드에 포함시키는 **연결리스트**
- 데이터를 삽입할 때 노드용 객체 생성, 삭제할 때 노드용 객체를 삭제 

- 구현 노드
```java
class Node<E>{
E data; // 데이터용 필드(data)의 자료형(E)이 참조형이므로 -> ❓클래스형 변수 data가 나타내는 것이 데이터 그 자체가 아니라, 데이터를 넣어 두는 인스턴스에 대한 '참조'
Node<E> next;
}
```
- [about class](https://www.techopedia.com/definition/3214/class-java#:~:text=A%20class%20in%20Java%20is,of%20the%20%E2%80%9Ccats%E2%80%9D%20class.)
- [제네릭](https://nimesha-wijepala.medium.com/java-generics-for-beginners-d8c561377f4d)

[노드의 자료형이 클래스 Node<E>형인 연결리스트를 클래스 Linked List<E>로 구현]
```java
// 연결 리스트 클래스

import java.util.Comparator;

public class LinkedList<E> {
       class Node<E> {
        private E data;             
        private Node<E> next;       

       Node(E data, Node<E> next) { 📍매개변수 data, next에 전달받은 값을 해당 필드에 대입
            this.data = data;
            this.next = next;
        }
    }

    private Node<E> head;        
    private Node<E> crnt;       

    //--- 생성자(constructor) ---//
    public LinkedList() {
        head = crnt = null;
    }

    //--- 노드 검색 ---//
    public E search(E obj, Comparator<? super E> c) {
        Node<E> ptr = head;                          // 현재 스캔 중인 노드

        while (ptr != null) {
            if (c.compare(obj, ptr.data) == 0) {    // 검색 성공
                crnt = ptr;
                return ptr.data;
            }
            ptr = ptr.next;                                // 뒤쪽 노드에 주목
        }
        return null;                                       // 검색 실패
    }

    //--- 머리 노드 삽입 ---//
    public void addFirst(E obj) {
        Node<E> ptr = head;                       // 삽입 전의 머리 노드
        head = crnt = new Node<E>(obj, ptr);
    }
    
    //--- 꼬리 노드 삽입 ---//
    public void addLast(E obj) {
        if (head == null)                // 리스트가 비어있으면
            addFirst(obj);               // 머리에 삽입
        else {
            Node<E> ptr = head;
            while (ptr.next != null)
                ptr = ptr.next;
            ptr.next = crnt = new Node<E>(obj, null);
        }
    }

    //--- 머리노드 삭제 ---//
    public void removeFirst() {
        if (head != null)                        // 리스트가 비어있지 않으면
            head = crnt = head.next;
    }

    //--- 꼬리노드 삭제 ---//
    public void removeLast() {
        if (head != null) {
            if (head.next == null)             // 노드가 하나만 있으면
                removeFirst();                 // 머리노드 삭제
            else {
                Node<E> ptr = head;            // 스캔 중인 노드
                Node<E> pre = head;            // 스캔 중인 노드의 앞쪽 노드

                while (ptr.next != null) {
                    pre = ptr;
                    ptr = ptr.next;
                }
                pre.next = null;                // pre는 삭제 뒤의 꼬리 노드
                crnt = pre;
            }
        }
    }

    //--- 노드p 삭제 ---//
    public void remove(Node p) {
        if (head != null) {
            if (p == head)                // p가 머리 노드이면
                removeFirst();            // 머리 노드 삭제
            else {
                Node<E> ptr = head;

                while (ptr.next != p) {
                    ptr = ptr.next;
                    if (ptr == null) return;    // p가 리스트에 없음
                }
                ptr.next = p.next;
                crnt = ptr;
            }
        }
    }

    //--- 선택 노드 삭제 ---//
    public void removeCurrentNode() {
        remove(crnt);
    }

    //--- 전체노드 삭제 ---//
    public void clear() {
        while (head != null)        // 비게 될 때까지
            removeFirst();          // 머리 노드 삭제
        crnt = null;
    }

    //--- 선택 노드를 하나 뒤쪽으로 진행 ---//
    public boolean next() {
        if (crnt == null || crnt.next == null)
            return false;           // 나아갈 수 없음
        crnt = crnt.next;
        return true;
    }

    //--- 선택 노드 표시 ---//
    public void printCurrentNode() {
        if (crnt == null)
            System.out.println("주목노드가 없습니다.");
        else
            System.out.println(crnt.data);
    }

    //--- 전체 노드 표시 ---//
    public void dump() {
        Node<E> ptr = head;

        while (ptr != null) {
            System.out.println(ptr.data);
            ptr = ptr.next;
        }
    }
}
```




___
# 배열 커서로 연결 리스트 만들기

___
# 원형 이중 연결 리스트 만들기


