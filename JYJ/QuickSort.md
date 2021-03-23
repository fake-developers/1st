# 퀵 정렬 (Quick Sort)

:writing_hand: *Assembled by Yunju Jang*

🤝*Contributors : JiYoung-Kwon, JeongHea Shin* 

<hr>


## 퀵 정렬 (Quick Sort)

- <b>퀵 정렬이란?</b>

  - 분할 정복 알고리즘의 하나로, 평균적으로 매우 빠른 수행 속도를 자랑하는 정렬 방법이다.

    - 합병 정렬과 달리, 리스트를 비균등하게 분할한다.

    > 분할 정복 방법
    >
    > - 문제를 작은 2개의 문제로 분리하고, 각각을 해결한 다음,  결과를 모아서 원래의 문제를 해결하는 전략이다.
    > - 분할 정복 방법은 대개 순환 호출을 이용하여 구현한다.

  - 불안정 정렬에 속하며, 다른 원소와의 비교만으로 정렬을 수행하는 비교 정렬이다.

  <br/>

  <br/>

- <b>퀵 정렬 과정 (오름차순 정렬 기준)</b>

  - 하나의 리스트를 피벗(pivot)을 기준으로 두 개의 비균등한 크기로 분할한다.
  - 분할된 부분 리스트를 정렬한다.
  - 두 개의 정렬된 부분 리스트를 합하여 전체가 정렬된 리스트가 되게 한다.

  <br/>

  <img src='resources/quick.gif' width='300px' align='center'>

  - 퀵 정렬 과정의 <b>핵심 단계</b>

    - 분할 (Divide) 

      - 입력 배열을 피벗을 기준으로 비균등하게 2개의 부분 배열로 분할한다.
      - 이때, 피벗을 중심으로 왼쪽에는 피벗보다 작은 요소들, 오른쪽에는 피벗보다 큰 요소들로 분할한다.

    - 정복 (Conquer)

      - 부분 배열을 정렬한다.

      - 부분 배열의 크기가 충분히 작지 않으면 순환 호출을 이용하여 다시 분할 정복 방법을 적용한다.

      - 실제로 정렬이 이루어지는 단계이다. 

        <small>\* cf. 병합 정렬은 결합에서 정렬이 이루어진다.</small>

    - 결합 (Combine)

      - 정렬된 부분 배열들을 하나의 배열에 합병한다.

    - 순환 호출이 한번 진행될 때마다 최소한 하나의 원소(피벗)은 최종적으로 위치가 정해지므로, 이 알고리즘은 반드시 끝난다는 것을 보장한다.

<br/>

<br/>

- <b>퀵 정렬 알고리즘 예제</b>

  - 배열에 [5, 3, 8, 4, 9, 1, 6, 2, 7] 가 저장되어 있다고 가정하고 오름차순으로 정렬한다.

    <img src='resources/QuickSort.png' width='400px' align='center'>

    <br/>

    <img src='resources/QuickSort2.png' width='900px' align='center'>

    <br/>

    - 리스트 안에 있는 한 요소(피벗)을 선택한다.
      
      - 이 경우 입력 리스트의 첫 번째 데이터로 한다.
      
    - 피벗을 기준으로 피벗보다 작은 요소들은 모두 피벗의 왼쪽으로 옮긴다.

    - 피벗을 기준으로 피벗보다 큰 요소들은 모두 피벗의 오른쪽으로 옮긴다.

      \* 피벗이 5인 경우, low : 3 / high : 7

      - low는 왼쪽에서 오른쪽으로 탐색하다가 피벗보다 큰 데이터 (8)을 찾으면 멈춘다.
      - high는 오른쪽에서 왼쪽으로 탐색하다가 피벗보다 작은 데이터 (2)를 찾으면 멈춘다.
      - 둘을 교환한다.
      - 이 과정을 low와 high가 엇갈릴 때까지 반복한다.
      - 9와 1교환
      - low와 high가 엇갈렸으므로 stop하고, pivot을 가운데로 옮긴다.

    - 피벗을 제외한 왼쪽 리스트와 오른쪽 리스트를 다시 정렬한다.

      \* 피벗이 1인 경우, 피벗이 9인 경우

    - 부분 리스트들이 더 이상 분할이 불가능할 때까지 반복한다.

<br/>

<br/>

- <b>퀵 정렬 예제 코드</b>

  ``` java
  public class QuickSort { 
      static int partition(int[] array,int start, int end) {
          int pivot = array[(start+end)/2]; //여기서는 중간값을 피벗으로 설정
          while(start<=end) { 
              while(array[start]<pivot)
                  start++; 
              while(array[end]>pivot) 
                  end--; 
              if(start<=end) { 
                  int tmp = array[start]; 
                  array[start]=array[end]; 
                  array[end]=tmp; 
                  start++;
                  end--;
              }
          }
          return start;
      } 
      
      static int[] quickSort(int[] array,int start, int end) {
          int p = partition(array, start, end); //분할
          if(start<p-1) 
              quickSort(array,start,p-1); //정복
          if(p<end)
              quickSort(array,p,end); //정복
          return array;
      } 
      public static void main(String[] args) { 
          int[] array = {4,2,3,5,9};
          array = quickSort(array,0,array.length-1); 
          System.out.println(Arrays.toString(array));
      } 
  }
  ```

  

  <br/>

  <br/>

- <b>퀵 정렬의 특징</b>

    - 장점
      
        - 속도가 빠르다.
          - 시간 복잡도가 O(nlog₂n)을 가지는 다른 정렬 알고리즘과 비교했을 때도 가장 빠르다.
          - 불필요한 데이터의 이동을 줄이고 먼 거리의 데이터를 교환한다.
          - 한 번 결정된 피벗들이 추후 연산에서 제외된다. (캐시 효율)
        - 제자리 정렬 중 하나로 추가 메모리 공간을 필요로 하지 않는다.
          - 퀵 정렬은 O(log n)만큼의 메모리를 필요로 한다.
        
        <br/>
    - 단점
      - 불안정 정렬(Unstable Sort)이다.
      - 정렬된 리스트에 대해서는 퀵 정렬의 불균형 분할에 의해 오히려 수행시간이 더 많이 걸린다.
        - 피벗 값이 최소나 최대값으로 지정되어 파티션이 나누어지지 않았을 때)
        - O(n^2)
        - 퀵 정렬의 불균형 분할을 방지하기 위하여 피벗을 선택할 때 더욱 리스트를 균등하게 분할할 수 있는 데이터를 선택한다. 

<br/>

<br/>

- <b>퀵 정렬 시간 복잡도</b>
    - 최선의 경우
        
      - O(nlog₂n)
      
        - 비교횟수 : nlog₂n 번
      
        <img src='resources/QuickO.png' width='6500px' align='center'>
      
        - 순환 호출의 깊이 : log₂n
      
          - 레코드의 개수 n이 2의 거듭 제곱이라고 가정 (n=2^k) 했을 때,  n = 2^3의 경우, 2^3 -> 2^2 -> 2^1 -> 2^0 순으로 줄어들어, 순환 호출의 깊이가 3임을 알 수 있다.
          - 이를 일반화하면 n=2^k의 경우, k(k=log₂n) 임을 알 수 있다.
      
        - 각 순환 호출 단계의 비교 연산 : n
      
          - 각 순환 호출에서는 전체 리스트의 대부분의 레코드를 비교해야 하므로 평균 n번 정도의 비교가 이루어진다.
      
          - 따라서, 최선의 경우 순환 호출의 깊이 * 각 순환 호출 단계의 비교 연산 = nlog₂n임을 알 수 있다.
          - 이동 횟수는 비교 횟수보다 적으므로 무시가 가능하다.

    <br/>

    <br/>

    - 최악의 경우

      - 리스트가 계속 불균형하게 나누어지는 경우

        - 특히, 이미 정렬된 리스트에 대하여 퀵 정렬을 해야하는 경우

      - 비교 횟수

        <img src='resources/QuickO2.png' width='400px' align='center'>

        - 순환 호출의 깊이
          - 레코드의 개수 n이 2의 거듭제곱이라고 가정 (n = 2^k) 했을 때
            - 순환 호출의 깊이는 <b>n</b> 임을 알 수 있다.
        - 각 순환 호출 단계의 비교 연산
          - 전체 리스트의 대부분의 레코드를 비교해야한다.
          - 따라서, <b>평균 n번</b> 정도의 비교가 이루어진다.
        - 순환 호출의 깊이 * 각 순환 호출 단계의 비교 연산 = <b>n^2</b>

        <br/>

      - 이동 횟수

        - 비교 횟수보다 적으므로 무시 가능

      - 따라서, 최악의 경우는 T(n) = O(n^2)

    <br/>

    <br/>

    - 평균 : T(n) = O(nlog₂n)

<br/>

<br/>

## 예상질문❔

Q1) 퀵 정렬이란 무엇인가?

A1) 배열을 피벗을 기준으로 비균등한 2개의 부분 배열로 분할한 후, 각 부분 배열을 정렬한 후 다시 정렬된 원래의 리스트로 정렬하는 알고리즘이다.

<br/>

<br/>

### Reference📖

- https://github.com/fake-developers/1st/blob/main/SJH/Quick%20sort.md
- https://github.com/fake-developers/1st/blob/main/KJY/%5BDATA%20STRUCTURE%5D%20%ED%80%B5%20%EC%A0%95%EB%A0%AC(Quick%20Sort).md
