# Heap

### Heap이란?

- **우선순위 큐**를 위해 만들어진 자료구조이다.

   <details>
      <summary> 우선순위 큐 </summary>

     * 우선순위의 개념에 큐를 도입한 자료구조

     * 데이터들이 우선순위를 가지고 있고, 우선순위가 높은 데이터가 먼저 나간다.

          <img src="https://user-images.githubusercontent.com/58902042/106144929-3f5f0280-61b8-11eb-9260-d1ae4531a6f7.PNG" height =80>

     * 우선순위 큐는 배열, 연결리스트 힙으로 구현 가능하다.

        <img src="https://user-images.githubusercontent.com/58902042/106145199-9664d780-61b8-11eb-86d9-8d09b7ad25dc.PNG" height=130>

     * **힙으로 구현하는 것이 가장 효율적**이다.
   </details>

- 힙은 **완전 이진 트리**의 일종으로, 최댓값과 최솟값을 빠르게 찾아내는 연산을 위해 고안 되었다.
- 힙은 일종의 **반정렬 상태(느슨한 정렬 상태 유지)** 를 유지한다.
  - 큰 값이 상위 레벨에 있고, 작은 값이 하위 레벨에 있다는 정도
  - 부모 노드의 키 값이 자식 노드의 키 값보다 항상 큰(작은) 이진 트리를 말한다.
  - 힙 트리에서는 **중복된 값을 허용** 한다.
    - 이진 탐색 트리에서는 허용하지 않는다.

<br>

### Heap의 종류

<img src="https://user-images.githubusercontent.com/58902042/106146322-e3957900-61b9-11eb-9fc2-bdfb53b31249.PNG" height=200>

- 최대 힙(Max Heap)
  - 부모 노드의 키 값이 자식 노드의 키 값보다 크거나 같은 완전 이진 트리
  - key(부모 노드 값) >= key(자식 노드 값)
  - 최대값은 이진트리의 Root 부분에 항상 존재한다.

- 최소 힙(Min Heap)
  - 부모 노드의 키 값이 자식 노드의 키 값보다 작거나 같은 완전 이진 트리
  - key(부모 노드 값) <= key(자식 노드 값)
  - 최솟값은 이진트리의 root 부분에 항상 존재한다.

<br>

### Heap의 구현

- 힙을 저장하는 표준적인 자료구조는 배열이다.

- 구현을 쉽게 하기 위해 배열의 첫 번째 인덱스인 0은 사용되지 않는다.

- 특정 위치의 노드 번호는 새로운 노드가 추가되어도 변하지 않는다.

  - ex_) 예를 들어, 루트 노드의 오른쪽 노드의 번호는 항상 3이다.

    <img src="https://user-images.githubusercontent.com/58902042/106147632-6f5bd500-61bb-11eb-8f67-44cc8d1dfd52.PNG" height=350>

- 힙에서의 부모 노드와 자식 노드의 관계
  - 왼쪽 자식의 Index = (부모 Index) * 2
  - 오른쪽 자식의 Index = (부모 Index) * 2 + 1
  - 부모의 Index = (자식의 Index) / 2

<br>

### Heap의 삽입

1. 힙에 새로운 요소가 들어오면, 일단 새로운 노드를 힙의 마지막 노드에 이어서 삽입한다.

2. 새로운 노드를 부모 노드들과 교환해서 힙의 성질을 만족시킨다.

   - ex_)

      <img src="https://user-images.githubusercontent.com/58902042/106148927-feb5b800-61bc-11eb-929a-b5456fbea417.PNG" height=700>


<br>

### Heap의 삭제

1. 최대 힙에서 최댓값은 루트 노드이므로 루트 노드가 삭제된다.

   - 최대 힙에서 삭제 연산은 최댓값을 가진 요소를 삭제하는 것

2. 삭제된 루트 노드에는 힙의 마지막 노드를 가져온다.

3. 힙을 재구성한다.

   - ex_)

   <img src="https://user-images.githubusercontent.com/58902042/106350158-17d27c00-6317-11eb-9c87-53fba924ece4.PNG" height=700>





-------------

**<참조>**

- https://github.com/fake-developers/1st/blob/JYJ-04/JYJ/Heap.md
