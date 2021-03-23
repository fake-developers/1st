# 합병 정렬(Merge sort)

- '존 폰 노이만'이 제안한 정렬 방법
- **분할 정복 알고리즘** 의 하나로, 병합해놓은 리스트를 원본에 복사하는 과정 등이 필요하여 시간이 오래걸린다.
  - 분할 정복 방법
    - 문제를 작은 2개의 문제로 분리하고 각각을 해결한 다음, 결과를 모아서 원래의 문제를 해결하는 전략
    - 분할 정복 방법은 대개 순환 호출을 이용하여 구현한다
  - 2-way병합과 n-way 병합
    - 2-way : 2개의 정렬된 집합을 하나의 집합으로 만드는 병합 방법
    - n-way : n개의 정렬된 집합을 결합하여 하나의 집합으로 만드는 병합 방법
- 일반적인 방법으로 구현했을 때 **안정 정렬** 에 속한다

<br>

## 합병 정렬 과정 (오름차순 정렬 기준)

- 하나의 리스트를 두 개의 균등한 크기로 분할하고 분할된 부분 리스트를 정렬한 다음, 두 개의 정렬된 부분 리스트를 합하여 전체가 정렬된 리스트가 되게하는 방식이다.

- 추가적인 리스트가 필요하다.

- 합병 정렬의 과정의 핵심 단계

  - **분할(Divide)** : 정렬되지 않은 리스트를 절반으로 잘라 비슷한 크기의 두 부분 리스트로 만든다.

  - **정복(Conquer)**: 각 부분 리스트를 재귀적으로 합병 정렬을 이용해 정렬한다.

  - **결합(Combine)** : 두 부분 리스트를 다시 하나의 정렬된 리스트로 **합병**한다. 이 때 정렬 결과가 임시 배열에 저장된다.

    :bulb: 실제로 정렬이 이루어지는 단계(vs 퀵 정렬은 정복에서 정렬이 이루어진다.)

  - **복사(Copy)** : 임시 배열에 저장된 결과를 원래 배열에 복사한다.

- 정렬 예제

  <img src="https://gmlwjd9405.github.io/images/algorithm-merge-sort/merge-sort-concepts.png">

  1. 하나의 배열을 두개로 쪼갠다
     - `[21, 10, 12, 20]`  `[25, 13, 15, 22]`
  2. 두개의 배열을 네개로 쪼갠다.
     - `[21, 10]` `[12, 20]` `[25, 13]` `[15, 22]`
  3. 네 개의 배열을 여덟개로 쪼갠다.
     - `[21]` `[10]` `[12]` `[20]` `[25]` `[13]` `[15]` `[22]`
  4.  더 이상 배열을 쪼갤 수 없으므로, 두개씩 합치기 시작한다.
     - 오름차순 기준이므로 작은 숫자가 앞에 큰 숫자가 뒤에 위치한다.
     - `[10, 21]` `[12, 20]` `[13, 25]` `[15, 22]`
  5.  네개의 배열을 두개로 합친다.
     - 각 배열에서 작은 두개를 비교한 후, 다시 또 두 배열을 비교하여 작은 값이 앞에 오게 한다.
     - `[10, 12, 20, 21]`  `[13, 15, 22, 25]`

  <img src="https://gmlwjd9405.github.io/images/algorithm-merge-sort/merge-sort.png">

  6. 정렬된 두개의 배열을 하나로 합친다.	

     - 2개의 정렬된 리스트를 합병하는 과정
       - 2개의 리스트의 값들을 처음부터 하나씩 비교하여 두 개의 리스트의 값 중에서 더 작은 값을 새로운 리스트(sorted)로 옮긴다.
       - 둘 중에서 하나가 끝날 때까지 이 과정을 되풀이한다.
       - 만약 둘 중에서 하나의 리스트가 먼저 끝나게 되면 나머지 리스트의 값들을 전부 새로운 리스트(sorted)로 복사한다.
       - 모두 정렬된 새로운 리스트를 원래의 리스트로 옮긴다.
     - 위의 합병 과정은 합병하는 과정에 모두 적용된다.

     - `[10, 12, 13, 15, 20, 21, 22, 25]`

- gif 으로 보는 합병 정렬

  <img src="https://sweetlog.netlify.app/61dd53416b89ba128a162db51a62f582/220px-Merge-sort-example-300px.gif" height=200>

- ex_) 코드 예제

  ~~~java
  public class MergeSort { 
  	static int[] sorted = new int[8]; 
  	public static void merge(int a[], int m, int middle, int n) { 
          int i = m; // 첫 번째 부분집합의 시작 위치 설정 
          int j = middle+1; // 두 번째 부분집합의 시작 위치 설정
          int k = m; // 배열 sorted에 정렬된 원소를 저장할 위치 설정 
  
          while(i<=middle && j<=n) { 
              if(a[i]<=a[j]) { 
                  sorted[k] = a[i]; 
                  i++;
              }else { 
                  sorted[k] = a[j];
                  j++; 
              }
              k++; 
          } 
          if(i>middle) { 
              for(int t=j;t<=n;t++,k++) { 
                  sorted[k] = a[t]; 
              }
          }
          else {
              for(int t=i;t<=middle;t++,k++) { 
                  sorted[k] = a[t];
              } 
          } 
          for(int t=m;t<=n;t++) { 
              a[t] = sorted[t];
          } 
      System.out.println("병합 정렬 후: "+Arrays.toString(a)); 
  	} 
      public static void mergeSort(int a[], int m, int n) { 
          int middle;
          if(m<n) { 
              middle = (m+n)/2; 
              mergeSort(a, m, middle); // 앞 부분에 대한 분할 작업 수행
              mergeSort(a, middle+1, n); // 뒷 부분에 대한 분할 작업 수행 
              merge(a, m, middle, n); // 부분집합에 대하여 정렬과 병합 작업 수행 
          } 
      } 
      public static void main(String[] args) { 
          int[] list = {58,8,28,3,18,6,33,20}; 
          int size = list.length; 
          System.out.println("정렬 수행 전: "+Arrays.toString(list));
          System.out.println("-----------------병합 정렬 수행 시작------------------"); 
          mergeSort(list, 0, size-1);
      } 
  }
  ~~~

<br>

## 합병 정렬의 특징

- **장점**
  - 안정적인 정렬 방법
    - 데이터의 분포에 영향을 덜 받는다. 즉, 입력 데이터가 무엇이든 간에 정렬되는 시간은 동일하다. (O(nlog₂n)로 동일)
  - 만약 레코드를 **연결 리스트(Linked List)** 로 구성하면, 링크 인덱스만 변경되므로 데이터의 이동은 무시할 수 있을 정도로 작아진다.
    - 제자리 정렬(in-place sorting)로 구현할 수 있다.
  - 크기가 큰 배열을 정렬할 경우 연결리스트를 사용한다면, 합병정렬은 어떤 정렬보다도 효율적이다.
- **단점**
  - 레코드가 **배열(Array)** 로 구성될 경우, 임시 배열이 필요하다.
    - 제자리 정렬이 아니다.
  - 레크드들의 크기가 큰 경우에는 이동 횟수가 많으므로 매우 큰 시간적 낭비를 초래한다.

<br>

## 합병 정렬의 시간 복잡도 & 공간 복잡도

- #### 시간 복잡도

  - 최선, 최악, 평균 모두 **O(nlog₂n)** 번

  - 분할단계 

    - 비교 연산과 이동 연산이 수행되지 않는다.

  - 합병 단계

    - 비교횟수 : nlog₂n 번

    <img src="https://gmlwjd9405.github.io/images/algorithm-quick-sort/sort-time-complexity-etc1.png" height=250> 

    - 순환 호출의 깊이: log₂n
      - 레코드의 개수 n이 2의 거듭제곱이라고 가정(n=2^k)했을 때, n=2^3의 경우, 2^3 -> 2^2 -> 2^1 -> 2^0 순으로 줄어들어 순환 호출의 깊이가 3임을 알 수 있다. 이것을 일반화하면 n=2^k의 경우, **k(k=log₂n)** 임을 알 수 있다.
    - 각 합병 단계의 비교 연산 : n
      - 각 정렬된 배열들을 병합할 때 모든 값을 비교해야하므로 최대 **n** 번 
    - 따라서,  **순환 호출의 깊이 * 각 합병 단계의 비교 연산 = nlog₂n** 

  - 이동 횟수

    - 순환 호출의 깊이 : log₂n
    - 각 합병 단계의 이동연산 : 2n
      - 임시 배열에 복사했다가 다시 가져와야 되므로 이동 연산은 총 부분 배열에 들어 있는 요소의 개수가 n인 경우, 레코드의 이동이 2n번 발생
    - 따라서,  **순환 호출의 깊이 * 각 합병 단계의 이동 연산 = 2nlog₂n** 

  - 따라서 시간복잡도는 **nlog₂n+ 2nlog₂n =  3nlog₂n = O(nlog₂n)**

- #### 공간복잡도

  - 두 개의 배열을 병합할 때 병합 결과를 담아 놓을 배열이 추가로 필요하다. 따라서 공간 복잡도는 **O(n)**

<br>

:bulb: **정렬 알고리즘의 시간 복잡도 비교**

​	<img src="https://gmlwjd9405.github.io/images/algorithm-merge-sort/sort-time-complexity.png" height=250>

- **단순(구현 간단)하지만 비효율적인 방법 :** 삽입 정렬 , 선택 정렬, 버블 정렬
- **복잡하지만 효율적인 방법 :** 퀵 정렬, 힙 정렬, **합병 정렬** , 기수 정렬

--------

**<참조>**

- [[알고리즘] 합병 정렬(merge sort)이란](https://gmlwjd9405.github.io/2018/05/08/algorithm-merge-sort.html)
- [합병 정렬(merge sort)에 대해 알아보자](https://sweetlog.netlify.app/algorithm/merge_sort/)

- [[자료구조] 병합정렬(MergeSort) with JAVA](https://heekim0719.tistory.com/289 )
