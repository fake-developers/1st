# 선택 정렬(Selection sort)

- 제자리 정렬 알고리즘의 하나
  - 제자리 정렬 : 입력 배열(정렬되지 않은 값들) 이외에 다른 추가 메모리를 요구하지 않는 정렬 방법
- 해당 순서에 넣을 위치는 이미 정해져 있고, 어떤 원소를 넣을지 선택하는 알고리즘
- [버블 정렬](./Bubble%20sort.md)과 비슷하지만 보다 개선된 정렬이다.

<br>

## 선택 정렬 과정(오름차순 정렬 기준)

- 선택 정렬은 첫 번째 자료를 두번째 자료부터 마지막 자료까지 차례대로 비교하여 가장 작은 값을 찾아 첫번째에 놓고, 정렬된 첫 번째를 제외하고 다시 두번째 자료부터 마지막 자료까지 앞의 과정을 반복하며 자료를 정렬한다.

- **한 번 전체 반복을 수행하고 나면 가장 작은 값의 자료가 맨 앞에 오게 된다.**

- 따라서, 1회전 반복을 수행할 때마다 정렬에서 제외되는 데이터가 하나씩 늘어간다.

- 정렬 예제

  <img src="https://media.vlpt.us/images/hwamoc/post/4adce14a-bb45-4c39-8253-ae5665991156/%EC%84%A0%ED%83%9D1.gif" height=300> 

  1. 수열을 선형 탐색해 최소값을 찾는다.
     - 가장 작은 값 : 1
  2. 최소값을 열의 왼쪽 끝에 있는 값과 교환하고 정렬을 완료한다.
     - 1과 6 교환
  3. 동일한 작업을 모든 값이 정렬을 마칠 때까지 반복한다.
     - 2와 8 교환
     - 3은 그대로
     - 4와 5 교환
     - 5와 9 교환
     - 6과 10 교환
     - 7,8,9,10은 그대로
  
- ex_) 코드 예제

  ~~~java
  void selectionSort(int[] arr) {
      int indexMin, temp; 
      for (int i = 0; i < arr.length-1; i++) { // 1. 
          indexMin = i; 
          for (int j = i + 1; j < arr.length; j++) { // 2. 
              if (arr[j] < arr[indexMin]) { // 3. 
                  indexMin = j; 
              } 
          } 
          // 4. swap(arr[indexMin], arr[i]) 
          temp = arr[indexMin]; 
          arr[indexMin] = arr[i]; 
          arr[i] = temp;
      } 
      System.out.println(Arrays.toString(arr)); 
  }
  ~~~

  

<br>

## 선택정렬의 특징

- **장점**
  - 자료 이동 횟수가 미리 결정된다.
- **단점**
  - **불안정 정렬(Unstable Sort)** 이다.
    - 값이 같은 레코드가 있는 경우에 상대적인 위치가 변경될 수 있다.

<BR>

## 선택정렬의 시간복잡도 & 공간복잡도

- #### 시간복잡도

  - **최선의 경우**
    - 자료가 이미 정렬되어 있는 경우
    - **O(n<sup>2</sup>)**
      - 비교횟수 : n(n-1)/2번
  - **최악의 경우**
    - 자료가 역순으로 정렬되어 있는 경우
    - **O(n<sup>2</sup>)**
      - 비교횟수 : n(n-1)/2번
  - 최선, 최악, 평균 모두 O(n<sup>2</sup>)로 동일하다.

- #### 공간복잡도
  - 주어진 배열 안에서 교환(swap)을 통해, 정렬이 수행되므로 **O(n)**

<BR>

:bulb: **정렬 알고리즘의 시간 복잡도 비교**

​	<img src="https://blog.kakaocdn.net/dn/TljF4/btqBYvpMt0m/KHsoZfoTPISLxNVZhsBWg1/img.png" height=250>

- **단순(구현 간단)하지만 비효율적인 방법 :** 삽입 정렬, **선택 정렬**, 버블 정렬
- **복잡하지만 효율적인 방법 :** 퀵 정렬, 힙 정렬, 합병 정렬, 기수 정렬

--------

**<참조>**

- [[알고리즘] 정렬 알고리즘-1 (버블 정렬, 선택 정렬, 삽입 정렬)](https://velog.io/@hwamoc/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EC%A0%95%EB%A0%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-1-%EB%B2%84%EB%B8%94-%EC%A0%95%EB%A0%AC-%EC%84%A0%ED%83%9D-%EC%A0%95%EB%A0%AC-%EC%82%BD%EC%9E%85-%EC%A0%95%EB%A0%AC)

- [[알고리즘] 선택 정렬(selection sort)이란](https://gmlwjd9405.github.io/2018/05/06/algorithm-selection-sort.html)

- [[정렬] 선택정렬(Selection Sort)의 개념/Java코드/시간복잡도/공간복잡도](https://devuna.tistory.com/28)




