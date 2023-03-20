___
# What is sorting? 
대소 관계에 따라 데이터 집합을 일정한 순서로 나열

* - 오름차순 : 작은 데이터가 앞
  - 내림차순

*  안정된 정렬 : 같은 값을 정렬해도 그 전의 순서가 유지되는 것

* - 내부정렬 : 데이터 개수가 상대적으로 적을 때
  - 외부정렬 : 데이터가 많아서 하나의 배열 이상 필요시

* 핵심 요소: 교환, 선택, 삽입

___
# 버블정렬 bubble sort 
(=단순 교환 정렬 straight exchange sort) 이웃한 두 요소의 대소 관계를 비교하고 필요에 대한 교환을 반복

* if 가장 작은 값을 앞으로 보내려고 한다면, 데이터 개수가 n개라면 n-1 번 비교 -> 가장 작은 값이 맨 앞에 정렬됨
* 비교하고 자리를 바꾸는 것을 pass
* 두 번째 자리에 원하는 값(두 번째로 작은 값을 넣는)을 넣기 위해선 n-2번 pass가 진행됨
* 그리고 모든 정렬이 끝나려면 n-1번의 pass가 진행되는데 마지막 값은 비교없이 마지막에 위치하니까

### 버블 정렬 프로그램 만들기
* 변수 i값을 0부터 n-2까지 1씩 증가시키며 패스를 n-1번 수행하는 프로그램

❗ n-2 왜냐면 배열은 0부터 시작하니까 n값을 넣으면 n-1 값까지만 비교하면 되는데 배열안의 숫자는 그것보다 -1 해야되므로

```java
for(int i =0; i<n-1;i++){

}
 📍 이렇게 무작위로 배열값을 나열하고 뒤에서 앞으로 비교& 자리를 바꾸는 코드를 작성한다.

'''java
class BubbleSort{
static void swap(int[] 1, int idx1, int idx2} {
int t = a[idx1]
a[idx1] = a[idx2];
a[idx2] = t;
} //비교한 두 값을 교환

static void bubbleSort(int[] a, int n){
for(int i =0; i<n-1; i++)
for(int j= n-1; j>i; j--)
if(a[[j-1] > a[j])
swap(a, j-1, j);
}
```

### 알고리즘 개선하기1

상황) 뒤에서부터 비교하다가 중간부터 교환이 필요없을 때 (이미 정렬이 된 상태), 정렬의 진행을 멈추기 위한 방법

❓p 207 어떤 패스에서 요소의 교환 횟수가 0번이면 더이상 정렬할 요소가 없다는 뜻

❓  
1. 변수 exchg 새롭게 추가  
2. 패스 전  exchg = 0; -> 요소 교환시 +1 즉, 패스 종료한(안쪽 for 반복이 완료시) 변수 exchg값은 해당 패스의 교환 횟수  
3. 패스 종료시 exchg =0 이면 정렬이 완료 -> 함수 종료  

❓ p 206 q2 출력 패스1 1,8은 교환 이루어지지 않는데 왜 멈추지 않고 진행

### 알고리즘 개선하기2  
last = 패스시 오른쪽 인덱스를 저장하는 변수 -> ❓last를 k에 대입하여 다음에 수행할 패스의 범위 제한  
❗마지막 교환이 일어난 인덱스는 제외하고 정렬하는 것
___
# 단순 선택 정렬(straight selection sort) 
* 가장 작은 요소를 맨 앞, 두 번째 작은 요소는 맨 앞에서 두 번째로 이동하는 작업을 반복
가장 작은 값을 선택 후 맨 앞에 넣기 -> 두 번째 작은 요소를 그 다음에 넣기

❓ 실습 6-4 swap전까지는 가장 작은 값을 찾는 메서드인가? 아직 정렬은 안하고? => Yes
___
# 단순 삽입 정렬(straight insertion sort) 
* 아직 정렬되지 않은 부분의 첫 번째 요소를 정렬한 부분의 알맞은 위치에 삽입

* 단순삽입 정렬은 두 번째 요소부터 선택하여 진행

* 알맞은 위치에 삽입? 이웃한 요소를 비교하면서 위치를 교환하여 원하는 곳에 삽입하는 것

___
# 셸 정렬
**단순 삽입 정렬**의 장점을 살리고 단점을 보완하여 스피드 UP

 -단순 삽입 정렬 
 장점: 정렬되어 있거나 정렬 상태가 가까우면 속도가 빠르지만
 단점: 삽입할 곳이 멀리 있으면 pass 횟수가 많아진다.
 
 그럼 셸 정렬이란?
 
 정렬을 큰 2개의 그룹으로 나누고
 1번 그룹의 맨앞 vs 2번 그룹의 맨앞 pass
 
 그리고 정렬을 더 작은 큰 그룹으로 나누고
 1번 그룹의 맨앞 vs 2번 그룹의 맨앞 pass vs 3번 그룹의 맨앞 pass
 
 -> 조금이라도 더 '정렬된'상태에서 단순 삽입 정렬 사용
 
 ```dart
 // 
 class ShellSort {
     static void shellSort(int[] a, int n) { 📍배열 x = a와 배열 x의 길이값 nx = n를 shellSort 메소드로 실행
        for (int h = n / 2; h > 0; h /= 2)   📍h = 길이를 반으로 나누고, 만약 반으로 나눈 값이 0보다 크면
            for (int i = h; i < n; i++) {    📍 반으로 나눠진 값을 i에 넣고, i값이 n보다 작으면
                int j;                   
                int tmp = a[i];              📍tmp에 a배열의 나눠진 중간 배열의 값을 넣고
                
                for (j = i - h; j >= 0 && a[j] > tmp; j -= h)  ❓근데 왜 여기서 j값을 넣어주지? int j = i로 하면 안되나?  
                    a[j + h] = a[j];
                 a[j + h] = tmp;
            }
    }
    
  📢 이중 for문
  h = n/2 가 조건 h>0에 해당하면
  i = h에 넣고 조건 i<n에 해당하면
  j = i-h를 넣고 조건 j>=0&&(동시에) a[j]>tmp에 해당하면  a[j + h] = a[j]; a[j + h] = tmp; 실행하고
  j에 j-h값을 넣고 조건 j>=0&& a[j]>tmp에 해당하면.. 반복
  
  
    public static void main(String[] args) {
        Scanner stdIn = new Scanner(System.in);

        int nx = stdIn.nextInt();  📍배열 크기 정하기
        int[] x = new int[nx];     📍정한 크기의 배열 생성

        for (int i = 0; i < nx; i++) {  📍배열 개수만큼 값 for문 이용해서 자동으로 받아오기
            x[i] = stdIn.nextInt();
        }

        shellSort(x, nx);     📍배열 x와 배열 x의 길이값 nx를 shellSort 메소드로 실행      
        for (int i = 0; i < nx; i++)  📍실행된 값을 출력
            System.out.println("x[" + i + "]=" + x[i]);
    }
}

 
 ```
 ___
# 퀵 정렬 
the fastest

1. 피벗을 정해서 두 그룹으로 나누기
2. 왼쪽 끝에서 원하는 값과 오른쪽 끝에서 원하는 값의 위치를 바꾸기

```dart
class Partition {

    static void swap(int[] a, int idx1, int idx2) { 📍조건에 맞을 경우 값 교환 메서드
        int t = a[idx1]; 
        a[idx1] = a[idx2];  
        a[idx2] = t;
    }

    static void partition(int[] a, int n) {
        int pl = 0;        📍왼쪽 끝 인덱스
        int pr = n - 1;    📍오른쪽 끝 인덱스
        int x = a[n / 2];  📍피벗(여기서는 가운데 값)

        do {
            while (a[pl] < x) pl++;    📍피벗보다 작으면 +해서 오른쪽으로 이동
            while (a[pr] > x) pr--;    📍피벗보다 크면 -해서 왼쪽으로 이동
            if (pl <= pr)              📍위의 조건이 아닐 때 멈춰진 pl과 pr 인덱스 값을 비교해서 pl이 pr보다 작으면 값 pass
                swap(a, pl++, pr--);
        } while (pl <= pr);

      
        for (int i = 0; i <= pl - 1; i++)   ❓pl -1? 0 -1?          
                  
        if (pl > pr + 1) {for (int i = pr + 1; i <= pl - 1; i++)}  

        for (int i = pr + 1; i < n; i++)                  
           

    public static void main(String[] args) {
        Scanner stdIn = new Scanner(System.in);
       
        int nx = stdIn.nextInt();
        int[] x = new int[nx];

        for (int i = 0; i < nx; i++) {
           x[i] = stdIn.nextInt();
        }
        partition(x, nx);               
    }
}

```

```dart
❓ p229 
* pr이 맨 앞보다 오른쪽에 있으면(left<pr) 왼쪽 그룹을 나눕니다.
* pl이 맨 뒤보다 왼쪽에 있으면(pl<right) 오른쪽 그룹을 나눕니다.

 static void quickSort(int[] a, int left, int right) {
        int pl = left;                  
        int pr = right;                 
        int x = a[(pl + pr) / 2];       
        do {
            while (a[pl] < x) pl++;
            while (a[pr] > x) pr--;
            if (pl <= pr)
                swap(a, pl++, pr--);
        } while (pl <= pr);

        if (left < pr)  quickSort(a, left, pr);  ❓ 여기서 pr값과 pl값 do-while 진행 후의 값? 
        if (pl < right) quickSort(a, pl, right);
    }
```

* 비재귀적인 퀵 정렬 구현하기

 ___
# 병합 정렬
배열을 앞부분과 뒷부분 둘로 나누어 각각 정렬한 다음 병합하는 작업 반복

```dart
class MergeArray {
    
    static void merge(int[] a, int na, int[] b, int nb, int[] c) { 📍a배열/a 길이/b배열/ b길이/ c배열
        int pa = 0;
        int pb = 0;
        int pc = 0;

        while (pa < na && pb < nb)      
            c[pc++] = (a[pa] <= b[pb]) ? a[pa++] : b[pb++];  📍a 배열와 b 배열을 오른쪽 앞부터 비교해서 작은 수를 c배열로 보낸뒤,

        while (pa < na)                   📍비교 후 마지막 인덱스 길이와 a 배열의 크기 or b배열의 크기를 비교해서 작은 a 또는 b 배열을 나머지를 c배열에 넣어준다
            c[pc++] = a[pa++];

        while (pb < nb)                  
            c[pc++] = b[pb++];
    }

    public static void main(String[] args) {
        Scanner stdIn = new Scanner(System.in);
        int[] a = {2, 4, 6, 8, 11, 13};
        int[] b = {1, 2, 3, 4, 9, 16, 21};
        int[] c = new int[13];

        System.out.println("두 개의 배열을 병합");

        merge(a, a.length, b, b.length, c);     

        System.out.println("배열 a와 b를 병합하여 배열 c에 저장했습니다.");
        System.out.println("배열 a: ");
        for (int i = 0; i < a.length; i++)
            System.out.println("a[" + i + "] = " + a[i]);

        System.out.println("배열 b: ");
        for (int i = 0; i < b.length; i++)
            System.out.println("b[" + i + "] = " + b[i]);

        System.out.println("배열 c: ");
        for (int i = 0; i < c.length; i++)
            System.out.println("c[" + i + "] = " + c[i]);
    }
}

```

* 병합 정렬 구현하기 
정렬을 마친 배열의 병합을 응요하여 **분할 정복법**에 따라 정렬하는 알고리즘

- 분할 정복법(Divide and Conquer)
크고 방대한 문제를 조금씩 나눠가면서 용이하게 풀 수 있는 문제 단위로 나눈 다음 그것들을 다시 합쳐서 해결하자는 개념

```dart
class MergeSort {
    static int[] buff;    // 작업용 배열

  
    static void __mergeSort(int[] a, int left, int right) {
        if (left < right) {
            int i;
            int center = (left + right) / 2;
            int p = 0;
            int j = 0;
            int k = left;

            __mergeSort(a, left, center);         
            __mergeSort(a, center + 1, right);   

            for (i = left; i <= center; i++)
                buff[p++] = a[i];

            while (i <= right && j < p)
                a[k++] = (buff[j] <= a[i]) ? buff[j++] : a[i++];

            while (j < p)
                a[k++] = buff[j++];
        }
    }

  📍이게 꼭 있어야하나? 🚩 여기서 두 개로 나눌 수 있게 보내주고 __mergeSort에서 앞뒷부분을 각자 정렬 후에 새로운 buff 배열로 정렬된 두 개 배열을 병합!  
    static void mergeSort(int[] a, int n) {
        buff = new int[n];                  

        __mergeSort(a, 0, n - 1);           

        buff = null;                        
    }

    public static void main(String[] args) {
        Scanner stdIn = new Scanner(System.in);

        int nx = stdIn.nextInt();
        int[] x = new int[nx];

        for (int i = 0; i < nx; i++) {
            System.out.print("x[" + i + "]: ");
            x[i] = stdIn.nextInt();
        }

        mergeSort(x, nx);        

       for (int i = 0; i < nx; i++)
            System.out.println("x[" + i + "]=" + x[i]);
    }
}
```

*Arrays.sort로 퀵 정렬과 병합 정렬하기

 ___
# 힙 정렬
**선택 정렬** 응용 알고리즘 

- 선택 정렬(selection sort)  
주어진 리스트 중에 최소값을 찾는다-> 그 값을 맨 앞에 위치한 값과 교체한다(pass)-> 맨 처음 위치를 뺀 나머지 리스트를 같은 방법으로 교체

*힙(heap)
 '부못값이 자식값보다 항상 크다'라는 조건을 만족하는 **완전 이진 트리**
 
 -완전 이진 트리  
 부모는 자식을 왼쪽부터 추가하는 모양을 유지 + 부모가 가질 수 이쓴 자식의 최대 개수는 2
 
* 힙에서 부모 자식 사이의 대소 관계는 일정 but 형제 사이의 대소 관계는 일정 X (=부분 순서 트리 partial ordered tree)  

* 힙에서 가장 큰 값인 루트를 꺼낸다 -> 루트 이외의 부분을 힙으로 만든다 -> **그리고 남은 요소에서 다시 가장 큰 값을 구한다**

-트리를 힙으로 만드는 과정  
1. 루트를 꺼낸다 -> 마지막 요소를 루트로 옮긴다 -> 자기보다 큰 값을 갖는 자식 요소와 자리를 자꾸며 아래쪽으로 내려가는 작업 반복


! 하지만 초기 상태의 배열이 힙이 아니라면, 힙정렬 전에 배열을 힙 상태로 만들어야 한다.

```dart
  static void downHeap(int[] a, int left, int right) {
        int temp = a[left];        
        int child;                
        int parent;             

        for (parent = left; parent < (right + 1) / 2; parent = child) {
            int cl = parent * 2 + 1;        
            int cr = cl + 1;              
            child = (cr <= right && a[cr] > a[cl]) ? cr : cl;   
            if (temp >= a[child]) ❓
                break;
            a[parent] = a[child];
        }
        a[parent] = temp;
    }
```

  ___
# 도수 정렬(counting sort)  
요소의 대소 관계를 판단하지 않고 빠르게 정렬

*분포도수?
표본의 다양한 산출 분포를 보여주는 목록, 표, 그래프. 표에 들어가는 각 항목은 특정 그룹이나 주기 안에 값이 발생한 빈도나 횟수를 포함하고 있으며 이러한 방식으로 표는 표본 값의 분포를 요약

1. 도수분포표 만들기
- 배열안의 값들 중 같은 값은 분포 개수 정리
2. 누적도수분포표 만들기
- 각각의 값이하의 요소가 모두 몇 개인가 
3. 목표 배열 만들기  
<https://github.com/Lugriz/typescript-algorithms/blob/master/src/algorithms/sorting/counting-sort/README.md>     
4.배열 복사하기
```dart
class CountingSort {
    static void countingSort(int[] a, int n, int max) {
        int[] f = new int[max + 1];       📍만약 최댓값이 120면 121번 인덱스를 만들고 그 중간에 값이 없으면 0?
        int[] b = new int[n];             

        for (int i = 0;     i < n;    i++) f[a[i]]++;                  // [Step 1]
        for (int i = 1;     i <= max; i++) f[i] += f[i - 1];           // [Step 2]
        for (int i = n - 1; i >= 0;   i--) b[--f[a[i]]] = a[i];        // [Step 3]
        for (int i = 0;     i < n;    i++) a[i] = b[i];                // [Step 4]
    }
```

