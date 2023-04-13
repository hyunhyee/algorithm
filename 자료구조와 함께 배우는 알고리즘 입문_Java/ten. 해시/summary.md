___
# 해시법
hashing 데이터를 저장할 위치(인덱스)를 간단한 연산으로 구하여 검색, 추가, 삭제를 효율적으로 수행
- 인덱스: 데이터를 저장할 위치
- 배열의 키값: 각 요소의 값
- 해시값(hash value): 배열의 키값을 배열의 요솟수로 나눈 나머지를 정리한 값 (데이터 접근 시 사용)
- 해시 테이블: 해시값을 인덱스로 하여 원래의 키값을 저장한 배열
- 버킷(bucket): 해시테이블의 각 요소

![hashig table](https://media.geeksforgeeks.org/wp-content/uploads/20220701080941/ComponentsofHashing-660x342.png)


Ex {“ab”, “cd”, “efg”}
1. 해시 함수로 저장할 주소값 만들기
2. "a” = 1, “b”=2, .. 
3. "ab” = 1 + 2 = 3, “cd” = 3 + 4 = 7 , “efg” = 5 + 6 + 7 = 18  
4. 사이즈가 7인 데이블로 각 값을 나누면, “ab” = 3, “cd” = 0, “efg” = 4


### 충돌
collision 저장할 버킷이 중복되는 현상

###  체인법
chaining chain 모양의 연결 리스트로 연결하는 방법 = open hashing

##### 생성자 ChainHash
비어있는 테이블 생성

##### 메서드 hashValue
- 해시값을 구하는 메서드
= key의 해시값을 size로 나눈다

###  오픈 주소법
open addressing 충불 발생시 rehashing 하여 비어있는 버킷을 찾아내는 방벙 = closed hashing
