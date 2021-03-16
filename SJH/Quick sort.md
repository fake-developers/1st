# 퀵 정렬(Quick sort)

- '찰스 앤터니 리처드 호어'가 개발한 정렬 알고리즘
- **분할 정복 알고리즘**의 하나로, 평균적으로 **매우 빠른 수행 속도**를 자랑하는 정렬
  - 합병 정렬과 달리 퀵 정렬은 리스트를 비균등하게 분할
  - 분할 정복 방법
    - 문제를 작은 2개의 문제로 분리하고 각각을 해결한 다음, 결과를 모아서 원래의 문제를 해결하는 전략
    - 분할 정복 방법은 대개 순환 호출을 이용하여 구현한다.
- **불안정 정렬**에 속하며, 다른 원소와의 비교만으로 정렬을 수행하는 **비교 정렬**이다.

<br>

## 퀵 정렬 과정(오름차순 정렬 기준)

- 하나의 리스트를 피벗(pivot)을 기준으로 두 개의 비균등한 크기로 분할하고 분할된 부분 리스트를 정렬한 다음, 두 개의 정렬된 부분 리스트를 합하여 전체가 정렬된 리스트가 되게 한다.

- 퀵 정렬의 과정의 핵심 단계

  - **분할(Divide)** : 입력 배열을 피벗을 기준으로 비균등하게 2개의 부분 배열 **(피벗을 중심으로 왼쪽 : 피벗보다 작은 요소들 / 오른쪽 : 피벗보다 큰 요소들)** 로 분할한다.
  - **정복(Conquer) **: 부분 배열을 정렬한다. 부분 배열의 크기가 충분히 작지 않으면 **순환 호출**을 이용하여 다시 분할 정복 방법을 적용한다.
  - **결합(Combine)** : 정렬된 부분 배열들을 하나의 배열에 합병한다.

  - 순환 호출이 한번 진행될 때마다 최소한 하나의 원소(피벗)는 최종적으로 위치가 정해지므로, 이 알고리즘은 반드시 끝난다는 것을 보장할 수 있다.

- 정렬 예제

  <img src="https://user-images.githubusercontent.com/58902042/111310023-ebdd4100-869f-11eb-8cae-0ec5dc60230b.png" height=600>

  1. 리스트 안에 있는 한 요소를 선택한다. 이렇게 고른 원소를 **피벗(pivot)** 이라고 한다.
     - 이 경우 입력리스트의 첫 번째 데이터로 한다.
  2. 피벗을 기준으로 피벗보다 작은 요소들은 모두 피벗의 왼쪽으로 옮겨지고 피벗보다 큰 요소들은 모두 피벗의 오른쪽으로 옮겨진다.
     - 피벗이 5인 경우,
     - low : 3, right : 7
     - low는 왼쪽에서 오른쪽으로 탐색하다가 피벗보다 큰 데이터(8)를 찾으면 멈춘다.
     - high는 오른쪽에서 왼쪽으로 탐색하다가 피벗보다 작은 데이터(2)를 찾으면 멈춘다.
     - 8과 2 교환
     - 이 탐색-교환 과정은 low와 high가 엇갈릴 때까지 반복한다.
     - 9와 1교환
     - low와 high가 엇갈렸으므로 stop하고 pivot을 가운데로 옮긴다.
  3. 피벗을 제외한 왼쪽 리스트와 오른쪽 리스트를 다시 정렬한다.
     - 피벗이 1인 경우,
     - 피벗이 9인 경우
  4. 부분 리스트들이 더 이상 분할이 불가능할 때까지 반복한다.

- git으로 보는 퀵 정렬

  <img src="https://github.com/GimunLee/tech-refrigerator/raw/master/Algorithm/resources/quick-sort-001.gif">

- ex_) 코드 예제

  ~~~java
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
  
  ~~~

<br>

## 큌 정렬의 특징

- **장점**
  - 속도가 빠르다.
    - 시간 복잡도가 O(nlog₂n)를 가지는 다른 정렬 알고리즘과 비교했을 때도 가장 빠르다.
    - 퀵 정렬이 불필요한 데이터의 이동을 줄이고 먼 거리의 데이터를 교환할 뿐만 아니라, 한 번 결정된 피벗들이 추후 연산에서 제외되는 특성 때문이다.
  - 제자리 정렬 중 하나로 추가 메모리 공간을 필요로 하지 않는다
    - 퀵 정렬은 O(log n)만큼의 메모리를 필요로 한다.
- **단점**
  - **불안정 정렬(Unstable Sort)** 이다.
  - 정렬된 리스트에 대해서는 퀵 정렬의 불균형 분할에 의해 오히려 수행시간이 더 많이 걸린다.(**피벗 값이 최소나 최대값으로 지정되어 파티션이 나누어지지 않았을 때**)
    - O(n<sup>2</sup>)
    - 퀵 정렬의 불균형 분할을 방지하기 위하여 피벗을 선택할 때 더욱 리스트를 균등하게 분할할 수 있는 데이터를 선택한다.

<br>

## 퀵정렬의 시간복잡도 & 공간복잡도

- #### 시간복잡도

  - **최선의 경우**

    - **O(nlog₂n)**

      - 비교횟수 : nlog₂n 번

      <img src="https://gmlwjd9405.github.io/images/algorithm-quick-sort/sort-time-complexity-etc1.png" height=250> 

      - 순환 호출의 깊이): log₂n
        - 레코드의 개수 n이 2의 거듭제곱이라고 가정(n=2^k)했을 때, n=2^3의 경우, 2^3 -> 2^2 -> 2^1 -> 2^0 순으로 줄어들어 순환 호출의 깊이가 3임을 알 수 있다. 이것을 일반화하면 n=2^k의 경우, **k(k=log₂n)**임을 알 수 있다.
      - 각 순환 호출 단계의 비교 연산 : n
        - 각 순환 호출에서는 전체 리스트의 대부분의 레코드를 비교해야 하므로 **평균 n번** 정도의 비교가 이루어진다
      - 따라서, 최선의 경우 **순환 호출의 깊이 * 각 순환 호출 단계의 비교 연산 = nlog₂n** 임을 알 수 있다. 이동 횟수는 비교 횟수보다 적으므로 무시 가능하다.

  - **최악의 경우**

    - 리스트가 계속 불균형하게 나누어지는 경우

      - 특히, 이미 정렬된 리스트에 대해 실행되는 경우

    - **O(n<sup>2</sup>)**

      - 비교 횟수 : n<sup>2</sup> 번

      <img src="https://gmlwjd9405.github.io/images/algorithm-quick-sort/sort-time-complexity-etc2.png" height=280> 

      - 순환 호출의 깊이
        - 레코드의 개수 n이 2의 거듭제곱이라고 가정(n=2^k)했을 때, 순환 호출의 깊이는 **n** 임을 알 수 있다.
      - 각 순환 호출 단계의 비교 연산
        - 각 순환 호출에서는 전체 리스트의 대부분의 레코드를 비교해야 하므로 **평균 n번** 정도의 비교가 이루어진다.
      - 따라서, 최악의 경우 **순환 호출의 깊이 * 각 순환 호출 단계의 비교 연산 = n<sup>2</sup>** 임을 알 수 있다. 이동 횟수는 비교 횟수보다 적으므로 무시 가능하다.

  - **평균**

    - **O(nlog₂n)**

- #### 공간복잡도

  - 주어진 배열 안에서 교환(swap)을 통해, 정렬이 수행되므로 **O(n)**

<br>

:bulb: **정렬 알고리즘의 시간 복잡도 비교**

​	<img src="https://gmlwjd9405.github.io/images/algorithm-quick-sort/sort-time-complexity.png" height=250>

- **단순(구현 간단)하지만 비효율적인 방법 :** 삽입 정렬, 선택 정렬, 버블 정렬
- **복잡하지만 효율적인 방법 :** **퀵 정렬**, 힙 정렬, 합병 정렬, 기수 정렬

--------

**<참조>**

- [[알고리즘] 퀵 정렬(quick sort)이란](https://gmlwjd9405.github.io/2018/05/10/algorithm-quick-sort.html)
- [[자료구조] 퀵 정렬(Quick Sort) with JAVA](https://heekim0719.tistory.com/282 )
- [ 퀵 정렬(Quick Sort)](https://gyoogle.dev/blog/algorithm/Quick%20Sort.html)