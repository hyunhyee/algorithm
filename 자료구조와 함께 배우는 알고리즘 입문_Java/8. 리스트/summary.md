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

    private Node<E> head;      📍연결리스트 클래스가 갖는 데이터는 실질적으로 머리 포인터 head뿐  
    private Node<E> crnt;       

    public LinkedList() {
        head = crnt = null;    📍Node<E>형의 변수 head가 머리 노드에 대한 참조이지 머리 노드 그 자체가 아님
    }

     public E search(E obj, Comparator<? super E> c) { 
// https://www.google.com/search?q=Comparator%3C%3F+super&oq=Comparator%3C%3F+super&aqs=chrome..69i57.493j0j7&sourceid=chrome&ie=UTF-8

        Node<E> ptr = head;                          // 현재 스캔 중인 노드

        while (ptr != null) {
            if (c.compare(obj, ptr.data) == 0) {    
                crnt = ptr;
                return ptr.data;
            }
            ptr = ptr.next;                                
        }
        return null;                                      
    }

     public void addFirst(E obj) {
        Node<E> ptr = head;                       📍ptr = 머리노드A를 가리키는 머리 포인터 
        head = crnt = new Node<E>(obj, ptr);      📍삽입할 노드를 생성해서(데이터는 obj 포인트 가리키는 곳은 ptr(삽입 전 머리노드A) -> 생성한노드 참조 위해 head 업데이트
                                                    + 선택 포인터 crnt도 새로 만드는 노드를 가리키도록 업데이트
    }
    
     public void addLast(E obj) {
        if (head == null)                📍리스트가 비어 있으면 head에 노드 삽입
            addFirst(obj);               
        else {
            Node<E> ptr = head;
            while (ptr.next != null)
                ptr = ptr.next;
            ptr.next = crnt = new Node<E>(obj, null);
        }
    }

    public void removeFirst() {
        if (head != null)                        
            head = crnt = head.next;
    }

    public void removeLast() {
        if (head != null) {
            if (head.next == null)            
                removeFirst();                
            else {
                Node<E> ptr = head;            
                Node<E> pre = head;           

                while (ptr.next != null) {     ❓
                    pre = ptr;
                    ptr = ptr.next;
                }
                pre.next = null;               
                crnt = pre;
            }
        }
    }

    public void remove(Node p) {
        if (head != null) {
            if (p == head)                
                removeFirst();           
            else {
                Node<E> ptr = head;        ❓

                while (ptr.next != p) {
                    ptr = ptr.next;
                    if (ptr == null) return;    
                }
                ptr.next = p.next;
                crnt = ptr;
            }
        }
    }

    public void removeCurrentNode() {
        remove(crnt);
    }

     public void clear() {
        while (head != null)        
            removeFirst();         
        crnt = null;
    }

    //--- 선택 노드를 하나 뒤쪽으로 진행 ---//
    public boolean next() {
        if (crnt == null || crnt.next == null)
            return false;           // 나아갈 수 없음
        crnt = crnt.next;
        return true;
    }
}
```
## 포인터로 연결 리스트를 사용하는 프로그램 만들기

___
# 배열 커서로 연결 리스트 만들기
- 다음 노드를 가리키는 뒤쪽 포인터는 다음 노드에 대한 포인터 X, 다음 노드가 들어 있는 배열 요소의 인덱스 and 인덱스 포인터 = 커서(cursor)


```java
// 연결 리스트 클래스(배열 커서 버전）

import java.util.Comparator;

public class ArrayLinkedList<E> {

    //--- 노드 ---//
    class Node<E> {
        private E data;          // 데이터
        private int next;        // 리스트의 뒤쪽포인터
        private int dnext;       // 프리 리스트의 뒤쪽포인터

        //--- data와 next를 설정 ---//
        void set(E data, int next) {
            this.data = data;
            this.next = next;
        }
    }

    private Node<E>[] n;        // 리스트 본체
    private int size;           // 리스트 크기(최대 데이터 개수)
    private int max;            // 사용 중인 꼬리 record
    private int head;           // 머리노드
    private int crnt;           // 선택 노드
    private int deleted;        // 프리 리스트의 머리노드
    private static final int NULL = -1;    // 뒤쪽노드가 없음 / 리스트가 가득 참

    //--- 생성자(constructor) ---//
    public ArrayLinkedList(int capacity) {
        head = crnt = max = deleted = NULL;
        try {
            n = new Node[capacity];
            for (int i = 0; i < capacity; i++)
                n[i] = new Node<E>();
            size = capacity;
        }
        catch (OutOfMemoryError e) {        // 배열 생성에 실패
            size = 0;
        }
    }

    //--- 다음에 삽입하는 record의 인덱스를 구함 ---//
    private int getInsertIndex() {
        if (deleted == NULL) {                    // 삭제 record가 존재하지 않음
            if (max < size)
                return ++max;                     // 새 record를 사용
            else
                return NULL;                      // 크기 넘침(over)
        } else {
            int rec = deleted;                    // 프리 리스트에서
            deleted = n[rec].dnext;               // 머리 rec을 꺼냄
            return rec;
        }
    }

    //--- record idx를 프리 리스트에 등록 ---//
    private void deleteIndex(int idx) {
        if (deleted == NULL) {                    // 삭제 record가 존재하지 않음
            deleted = idx;                        // idx를 프리 리스트의
            n[idx].dnext = NULL;                  // 머리에 등록
        } else {
            int rec = deleted;                    // idx를 프리 리스트의
            deleted = idx;                        // 머리에 삽입
            n[rec].dnext = rec;
        }
    }

    //--- 노드를 검색 ---//
    public E search(E obj, Comparator<? super E> c) {
        int ptr = head;                                    // 현재 스캔 중인 노드

        while (ptr != NULL) {
            if (c.compare(obj, n[ptr].data) == 0) {
                crnt = ptr;
                return n[ptr].data;                   // 검색 성공
            }
            ptr = n[ptr].next;                        // 뒤쪽 노드 선택
        }
        return null;                                  // 검색 실패
    }

    //--- 머리노드 삽입 ---//
    public void addFirst(E obj) {
        int ptr = head;                                // 삽입 전의 머리노드
        int rec = getInsertIndex();
        if (rec != NULL) {
            head = crnt = rec;                         // 제 rec 번째 레코드에 삽입
            n[head].set(obj, ptr);
        }
    }

    //--- 꼬리노드 삽입 ---//
    public void addLast(E obj) {
        if (head == NULL)                                // 리스트가 비어있으면
            addFirst(obj);                               // 머리에 삽입
        else {
            int ptr = head;
            while (n[ptr].next != NULL)
                ptr = n[ptr].next;
            int rec = getInsertIndex();
            if (rec != NULL) {                        // 제 rec 번째 레코드에 삽입
                n[ptr].next = crnt = rec;
                n[rec].set(obj, NULL);
            }
        }
    }

    //--- 머리노드 삭제 ---//
    public void removeFirst() {
        if (head != NULL) {                            // 리스트가 비어있지 않으면
            int ptr = n[head].next;
            deleteIndex(head);
            head = crnt = ptr;
        }
    }

    //--- 꼬리노드 삭제 ---//
    public void removeLast() {
        if (head != NULL) {
            if (n[head].next == NULL)            // 노드가 하나만 있으면
                removeFirst();                   // 머리노드 삭제
            else {
                int ptr = head;                  // 스캔 중인 노드
                int pre = head;                  // 스캔 중인 노드의 앞쪽노드

                while (n[ptr].next != NULL) {
                    pre = ptr;
                    ptr = n[ptr].next;
                }
                n[pre].next = NULL;                    // pre는 삭제 뒤의 꼬리 노드
                deleteIndex(pre);
                crnt = pre;
            }
        }
    }

    //--- 레코드 p를 삭제 ---//
    public void remove(int p) {
        if (head != NULL) {
            if (p == head)                                // p가 머리 노드이면
                removeFirst();                            // 머리노드 삭제
            else {
                int ptr = head;

                while (n[ptr].next != p) {
                    ptr = n[ptr].next;
                    if (ptr == NULL) return;    // p가 리스트에 없음
                }
                n[ptr].next = NULL;
                deleteIndex(ptr);
                n[ptr].next = n[p].next;
                crnt = ptr;
            }
        }
    }

    //--- 선택 노드 삭제 ---//
    public void removeCurrentNode() {
        remove(crnt);
    }

    //--- 전체 노드 삭제 ---//
    public void clear() {
        while (head != NULL)                        // 비게 될 때까지
            removeFirst();                          // 머리 노드 삭제
        crnt = NULL;
    }

    //--- 선택 노드를 하나 뒤쪽으로 진행 ---//
    public boolean next() {
        if (crnt == NULL || n[crnt].next == NULL)
            return false;                                    // 나아갈 수 없음
        crnt = n[crnt].next;
        return true;
    }

    //--- 선택 노드 표시 ---//
    public void printCurrentNode() {
        if (crnt == NULL)
            System.out.println("선택 노드가 없습니다.");
        else
            System.out.println(n[crnt].data);
    }

    //--- 전체 노드 표시 ---//
    public void dump() {
        int ptr = head;

        while (ptr != NULL) {
            System.out.println(n[ptr].data);
            ptr = n[ptr].next;
        }
    }
}
```

## 배열의 비어 있는 요소 처리

## 프리 리스트


___
# 원형 리스트(circular list)
- 꼬리 노드가 머리 노드를 가리키는 연결 리스트

## 이중 연결 리스트(doubly linked list)

## 원형 이중 연결 리스트 만들기
```java
// 원형 이중 연결 리스트 클래스

import java.util.Comparator;

public class DoubleLinkedList<E> {
    //--- 노드 ---//
    class Node<E> {
        private E data;              // 데이터
        private Node<E> prev;        // 앞쪽포인터(앞쪽 노드에 대한 참조)
        private Node<E> next;        // 뒤쪽포인터(뒤쪽 노드에 대한 참조)

        //--- 생성자(constructor) ---//
        Node() {
            data = null;
            prev = next = this;
        }

        //--- 생성자(constructor) ---//
        Node(E obj, Node<E> prev, Node<E> next) {
            data = obj;
            this.prev = prev;
            this.next = next;
        }
    }

    private Node<E> head;        // 머리 포인터(참조하는 곳은 더미노드)
    private Node<E> crnt;        // 선택 포인터

    //--- 생성자(constructor) ---//
    public DoubleLinkedList() {
        head = crnt = new Node<E>();        // 더미 노드를 생성
    }

    //--- 리스트가 비어있는가? ---//
    public boolean isEmpty() {
        return head.next == head;
    }

    //--- 노드를 검색 ---//
    public E search(E obj, Comparator<? super E> c) {
        Node<E> ptr = head.next;                // 현재 스캔 중인 노드

        while (ptr != head) {
            if (c.compare(obj, ptr.data) == 0) {
                crnt = ptr;
                return ptr.data;                        // 검색 성공
            }
            ptr = ptr.next;                             // 뒤쪽 노드에 주목
        }
        return null;                                    // 검색 실패
    }

    //--- 선택 노드 표시 ---//
    public void printCurrentNode() {
        if (isEmpty())
            System.out.println("선택 노드가 없습니다.");
        else
            System.out.println(crnt.data);
    }

    //--- 전체 노드 표시 ---//
    public void dump() {
        Node<E> ptr = head.next;                // 더미 노드의 뒤쪽 노드

        while (ptr != head) {
            System.out.println(ptr.data);
            ptr = ptr.next;
        }
    }

    //--- 전체 노드 역순 표시 ---//
    public void dumpReverse() {
        Node<E> ptr = head.prev;                // 더미 노드의 앞쪽 노드

        while (ptr != head) {
            System.out.println(ptr.data);
            ptr = ptr.prev;
        }
    }

    //--- 선택 노드를 하나 뒤쪽으로 진행 ---//
    public boolean next() {
        if (isEmpty() || crnt.next == head)
            return false;                                    // 나아갈 수 없음
        crnt = crnt.next;
        return true;
    }

    //--- 선택 노드를 하나 앞쪽으로 진행 ---//
    public boolean prev() {
        if (isEmpty() || crnt.prev == head)
            return false;                                    // 나아갈 수 없음
        crnt = crnt.prev;
        return true;
    }

    //--- 선택 노드 바로 뒤에 노드 삽입 ---//
    public void add(E obj) {
        Node<E> node = new Node<E>(obj, crnt, crnt.next);
        crnt.next = crnt.next.prev = node;
        crnt = node;
    }

    //--- 머리 노드 삽입 ---//
    public void addFirst(E obj) {
        crnt = head;                                     // 더미 노드 head의 바로 뒤에 삽입
        add(obj);
    }

    //--- 꼬리 노드 삽입 ---//
    public void addLast(E obj) {
        crnt = head.prev;                                // 꼬리 노드head.prev 바로 뒤에 삽입
        add(obj);
    }

    //--- 선택 노드 삭제 ---//
    public void removeCurrentNode() {
        if (!isEmpty()) {
            crnt.prev.next = crnt.next;
            crnt.next.prev = crnt.prev;
            crnt = crnt.prev;
            if (crnt == head) crnt = head.next;
        }
    }

    //--- 노드p 삭제 ---//
    public void remove(Node p) {
        Node<E> ptr = head.next;

        while (ptr != head) {
            if (ptr == p) {                                // p를 찾았음
                crnt = p;
                removeCurrentNode();
                break;
            }
            ptr = ptr.next;
        }
    }

    //--- 머리 노드 삭제 ---//
    public void removeFirst() {
        crnt = head.next;                                // 머리 노드 head.next를 삭제
        removeCurrentNode();
    }

    //--- 꼬리 노드 삭제 ---//
    public void removeLast() {
        crnt = head.prev;                                // 꼬리 노드 head.prev를 삭제
        removeCurrentNode();
    }

    //--- 전체 노드 삭제 ---//
    public void clear() {
        while (!isEmpty())                            // 비게 될 때까지
            removeFirst();                            // 머리노드 삭제
    }
}
```
