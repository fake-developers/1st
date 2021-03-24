# 선택 정렬 (Selection Sort)

:writing_hand: *Assembled by Yunju Jang*

🤝*Contributors : JiYoung-Kwon, JeongHea Shin* 

<hr>


## 선택 정렬 (Selection Sort)

- <b>선택 정렬이란?</b>

  - 제자리 정렬 (in-place sorting) 알고리즘의 하나이다.
    - 제자리 정렬이란, 입력 배열 (정렬되지 않은 값들) 이외에 다른 추가 메모리를 요구하지 않는 정렬 방법을 말한다.
  - 해당 순서에 원소를 넣을 위치는 이미 정해져있고, 어떤 원소를 넣을지 선택하는 알고리즘이다.
    1. 첫 번째 순서에는 첫 번째 위치에 가장 최솟값을 넣는다.
    2. 두 번째 순서에는 두 번째 위치에 남은 값 중에서의 최솟값을 넣는다.
    3. 위 과정을 반복한다.

  <br/>

  <br/>

- <b>선택 정렬 과정 (오름차순 정렬 기준)</b>

  1. 주어진 배열 중에 최소값을 찾는다.
  2. 그 값을 맨 앞에 위치한 값과 교체한다. (pass)
  3. 맨 처음 위치를 뺀 나머지 배열을 같은 방법으로 교체한다.
  4. 하나의 원소만 남을 때까지 위의 과정을 반복한다.

  <img src='resources/selection.gif' width='500px' align='center'>

<br/>

<br/>

- <b>선택 정렬 알고리즘 예제</b>

  - 배열에 [9, 6, 7, 3, 5] 가 저장되어 있다고 가정하고 오름차순으로 정렬한다.

    <img src='resources/SelectionSort.png' width='900px' align='center'>

    <br/>

    - <b>1회전 -</b> 첫 번째 자료 9와 두 번째 자료부터 마지막 자료까지 비교한다.
      - 가장 작은 값을 첫 번째 위치에 옮겨 놓는다.
      - 이 과정에서 자료를 4번 비교한다.
    - <b>2회전 -</b> 두 번째 자료 6과 세 번째 자료부터 마지막 자료까지 비교한다.
      - 가장 작은 값을 두 번째 위치에 옮겨 놓는다.
      - 이 과정에서 자료를 3번 비교한다.
    - <b>3회전 -</b> 세 번째 자료 7과 네 번째 자료부터 마지막 자료까지 비교한다.
      - 가장 작은 값을 세 번째 위치에 옮겨 놓는다.
      - 이 과정에서 자료를 2번 비교한다.
    - <b>4회전</b> - 네 번째 자료 9와 마지막에 있는 자료 7일 비교하여 서로 교환한다.

<br/>

<br/>

- <b>선택 정렬 예제 코드</b>

  ``` java
  void selectionSort(int[] arr) {
      int indexMin, temp; 
      for (int i = 0; i < arr.length-1; i++) { // 1.위치(index) 선택
          indexMin = i; 
          for (int j = i + 1; j < arr.length; j++) { // 2. i+1번째 원소부터 선택한 위치(index)의 값과 비교 시작
              if (arr[j] < arr[indexMin]) { // 3.오름차순이므로, 현재 선택한 자리에 있는 값보다 순회하고 있는 값이 작다면, 
                  indexMin = j; // 위치(index)를 갱신한다.
              }
          } 
          // 4. swap(arr[indexMin], arr[i]) 
          temp = arr[indexMin]; 
          arr[indexMin] = arr[i]; 
          arr[i] = temp; 
      } 
      System.out.println(Arrays.toString(arr)); 
  }
  ```

  

  <br/>

  <br/>

- <b>선택 정렬의 특징</b>
  
    - 장점
      
        - 자료 이동 횟수가 미리 결정된다.
        
        <br/>
    - 단점
      - 불안정 정렬이다.
        - 값이 같은 레코드가 있는 경우, 상대적인 위치가 변경될 수 있다.

<br/>

<br/>

- <b>선택 정렬 시간 복잡도</b>
    - 비교 횟수
        - 두 개의 for 루프의 실행 횟수
      - 외부 루프 : (n-1)번
        - 내부 루프 (최소값 찾기)
          - 1회전 : n-1
          - 2회전 : n-2
          - ...
          - n-2회전 : n-(n-2) = 2
          - n-1회전 : n-(n-1) = 1
      - 따라서, T(n) = (n-1) + (n-2) + ... + 2 + 1 = n(n-1)/2 = O(n^2)
      - 최선, 평균, 최악의 경우 모두 O(n^2)로 동일하다.

<br/>

<br/>

- <b>선택 정렬 공간 복잡도</b>
  - 교환 횟수
    - 외부 루프의 실행 횟수와 동일하다. (즉, 상수 시간 작업)
    - 한번 교환하기 위하여 3번의 이동 (SWAP 함수의 작업)이 필요하다.
      - 3(n-1)번
  - 주어진 배열 안에서 교환을 통해 정렬이 수행된다.
    - O(n)


<br/>

<br/>

## 예상질문❔

Q1) 선택 정렬이란 무엇인가?

A1) 해당 순서에 넣을 위치는 이미 정해져 있고, 어떤 원소를 넣을지 선택하는 정렬 알고리즘이다.

<br/>

<br/>

### Reference📖

- https://github.com/fake-developers/1st/blob/main/KJY/%5BDATA%20STRUCTURE%5D%20%EC%84%A0%ED%83%9D%EC%A0%95%EB%A0%AC(Selection%20Sort).md
- https://github.com/fake-developers/1st/blob/main/SJH/Selection%20sort.md
