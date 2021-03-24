# [DATA STRUCTURE] 선택정렬(Selection Sort)

:writing_hand: *Assembled by JiYoung-Kwon (2021-03-16)* 



## 1. 선택 정렬이란?

- **제자리 정렬(in-place sorting)** 알고리즘의 하나
  - 입력 배열(정렬되지 않은 값들) 이외에 다른 추가 메모리를 요구하지 않는 정렬 방법
- **해당 순서에 원소를 넣을 위치는 이미 정해져 있고, 어떤 원소를 넣을지 선택하는 알고리즘**
  1. 첫 번째 순서에는 첫 번째 위치에 가장 최솟값을 넣는다.
  2. 두 번째 순서에는 두 번째 위치에 남은 값 중에서의 최솟값을 넣는다.
  3. 이하 생략…
- 기본적으로 오름차순을 기준으로 정렬함

<br/>

## 2. 선택 정렬 과정

1. 주어진 배열 중에 최소값을 찾는다.
2. 그 값을 맨 앞에 위치한 값과 교체한다. (pass)
3. 맨 처음 위치를 뺀 나머지 배열을 같은 방법으로 교체한다.
4. 하나의 원소만 남을 때까지 위의 1~3 과정을 반복한다.
5. 정렬 완료

<br/>

#### 2-1. 예시

![img](https://blog.kakaocdn.net/dn/vVwkP/btqBYf8Bp5U/o7DFDqpjMmDolg3BkZIQr1/img.png)

***

1. 첫 번째 자료 9를 두 번째 자료부터 마지막 자료까지와 비교
   * 가장 작은 값을 첫 번째 위치에 옮겨 놓음
   * 이 과정에서 자료를 4번 비교함
2. 두 번째 자료 6을 세 번째 자료부터 마지막 자료까지와 비교
   * 가장 작은 값을 두 번째 위치에 옮겨 놓음
   * 이 과정에서 자료를 3번 비교함
3. 세 번째 자료 7을 네 번째 자료부터 마지막 자료까지와 비교
   * 가장 작은 값을 세 번째 위치에 옮겨 놓음
   * 이 과정에서 자료를 2번 비교함
4. 네 번째 자료 9와 마지막에 있는 7을 비교하여 서로 교환
5. 정렬 종료

***

* Gif로 보는 선택정렬

![img](https://blog.kakaocdn.net/dn/bekAxf/btqBWrh1Sjl/AAVyKUtExiy6pdwfbhgR3k/img.gif)

<br/>

## 3. 선택 정렬의 특징

* **장점**

  - 알고리즘이 단순함
  - 자료 이동 횟수가 미리 결정됨
  - 정렬을 위한 비교 횟수는 많지만, 실제 교환하는 횟수는 적음
    - 많은 교환이 일어나야 하는 자료상태에서 비교적 효율적
  - 제자리 정렬이므로, 다른 메모리 공간을 필요로 하지 않음

* **단점**

  - 시간복잡도가 O(n^2)로, 비효율적임

  - 안정성을 만족하지 않음 (불안정 정렬 - `Unstable Sort`)

    - 즉, 값이 같은 레코드가 있는 경우에 상대적인 위치가 변경될 수 있음

    - ```
      # Stable Sort(안정 정렬)
      
      - 동일한 정렬기준을 가진 것은 정렬하기 전의 순서와 정렬한 후의 순서가 동일함
      - 예시
      	7 4 3 4` 1 5 를 오름차순으로 정렬했을 때,
      	1 3 4 4` 5 7 이런식으로 4와 4` 간의 동일한 정렬기준을 가짐
      - 종류
        Bubble Sort, Insertion Sort, Merge Sort
      ```

    - ```
      # Unstable Sort(불안정 정렬)
      
      - 동일한 정렬기준을 가진 것의 정렬 전/후 순서가 다를 수 있음
      - 예시
      	5 3 1` 9 2 1 를 오름차순으로 정렬했을 때, 
      	정렬 전의 순서가 유지된다는 보장을 할수 없음
          1` 1 2 3 5 9 또는 1 1` 2 3 5 9, 이렇게 두 가지 결과가 나올 수 있음
      - 종류
      	Selection Sort, Quick Sort, Heap Sort
      ```


<br/>

## 4. 선택 정렬 구현

* 오름차순 조건 예시

* ```java
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
  ```

  1. 우선, 위치(index)를 **선택**
  2. i+1번째 원소부터 선택한 위치(index)의 값과 비교를 시작
  3. 오름차순이므로 현재 선택한 자리에 있는 값보다 순회하고 있는 값이 작다면, 위치(index)를 갱신해줌
  4. `// 2.`번 반복문이 끝난 뒤, indexMin에 `// 1.`번에서 선택한 위치(index)에 들어가야하는 값의 위치(index)를 갖고 있으므로 서로 교환(swap)해줌

<br/>

## 5. 선택 정렬의 복잡도

#### 5-1. 시간 복잡도

- 비교 횟수
  - 두 개의 for 루프의 실행 횟수
  - 외부 루프 : (n-1)번
  - 내부 루프(최소값 찾기) 
    - 1번째 회전 : n-1
    - 2번째 회전 : n-2
    - ...
    - n-2번째 회전 : n-(n-2)  = 2
    - n-1번째 회전 : n-(n-1) = 1
- T(n) = (n-1) + (n-2) + … + 2 + 1 = n(n-1)/2 = O(n^2)
- 최선, 평균, 최악의 경우 모두 O(n^2)로 동일함

#### 5-2. 공간 복잡도

* 교환 횟수
  * 외부 루프의 실행 횟수와 동일. 즉 상수 시간 작업
  * 한번 교환하기 위하여 3번의 이동(SWAP 함수의 작업)이 필요함 -> 3(n-1)번
* 주어진 배열 안에서 교환을 통해 정렬이 수행됨
  * O(n)



#### :pushpin: 추가 ) 정렬의 시간 복잡도

![img](https://blog.kakaocdn.net/dn/TljF4/btqBYvpMt0m/KHsoZfoTPISLxNVZhsBWg1/img.png)

- **단순(구현 간단)하지만 비효율적인 방법 :** 삽입 정렬, 선택 정렬, 버블 정렬
- **복잡하지만 효율적인 방법 :** 퀵 정렬, 힙 정렬, 합병 정렬, 기수 정렬

![img](https://t1.daumcdn.net/cfile/tistory/996A5E3B5AE4201F1F)



<br/>

## :page_with_curl: Reference

[[알고리즘] 선택 정렬(selection sort)이란](https://gmlwjd9405.github.io/2018/05/06/algorithm-selection-sort.html)

[[정렬] 선택정렬(Selection Sort)의 개념/Java코드/시간복잡도/공간복잡도](https://devuna.tistory.com/28)

[[Algorithm] 선택 정렬 (Selection Sort)](https://donis-note.medium.com/algorithm-%EC%84%A0%ED%83%9D-%EC%A0%95%EB%A0%AC-selection-sort-375351d5c1dc)

[자료구조 :: 선택정렬 Selection sort (c/c++ 구현)](https://hongku.tistory.com/146)