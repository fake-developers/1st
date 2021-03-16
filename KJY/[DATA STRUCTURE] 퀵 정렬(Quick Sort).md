# [DATA STRUCTURE] 퀵 정렬(Quick Sort)

:writing_hand: *Assembled by JiYoung-Kwon (2021-03-16)* 



## 1. 퀵 정렬이란?

- ‘찰스 앤터니 리처드 호어(Charles Antony Richard Hoare)’가 개발한 정렬 알고리즘
- 퀵 정렬은 **불안정 정렬** 에 속하며, 다른 원소와의 비교만으로 정렬을 수행하는 **비교 정렬** 에 속함
- **분할 정복** 알고리즘의 하나로, 평균적으로 **매우 빠른 수행 속도를** 자랑하는 정렬 방법
  - 분할 정복(divide and conquer) 방법
    - 문제를 작은 2개의 문제로 분리하고 각각을 해결한 다음, 결과를 모아서 원래의 문제를 해결하는 전략
    - 분할 정복 방법은 대개 순환 호출을 이용하여 구현함
- 합병 정렬(merge sort)과 달리 퀵 정렬은 리스트를 **비균등하게** 분할
- 재귀 알고리즘
- 기본적으로 오름차순을 기준으로 정렬함

<br/>

## 2. 퀵 정렬 과정

* 퀵 정렬은 다음의 단계들로 이루어짐
  * **분할(Divide)**
    * 입력 배열을 피벗을 기준으로 비균등하게 2개의 부분 배열로 분할
      * (피벗을 중심으로 왼쪽: 피벗보다 작은 요소들, 오른쪽: 피벗보다 큰 요소들)
  * **정복(Conquer)**
    * 부분 배열을 정렬함
      * 부분 배열의 크기가 충분히 작지 않으면 **순환 호출** 을 이용하여 다시 분할 정복 방법을 적용
  * **결합(Combine)**
    * 정렬된 부분 배열들을 하나의 배열에 합병

* 순환 호출이 한 번 진행될 때마다 최소한 하나의 원소(피벗)는 최종적으로 위치가 정해지므로, 이 알고리즘은 반드시 끝난다는 것을 보장할 수 있음

<br/>

#### 2-1. 전체 흐름

* ![img](https://gmlwjd9405.github.io/images/algorithm-quick-sort/quick-sort.png)

1. 리스트 안에 있는 한 요소를 선택 
   * 이렇게 고른 원소를 **피벗(pivot)** 이라고 함
2. 피벗을 기준으로 피벗보다 **작은** 요소들은 모두 피벗의 **왼쪽으로** 옮겨지고 피벗보다 **큰** 요소들은 모두 피벗의 **오른쪽으로** 옮겨짐
   * 피벗을 중심으로 왼쪽 : 피벗보다 작은 요소들
   * 피벗을 중심으로 오른쪽 : 피벗보다 큰 요소들
3. **피벗을 제외한** **왼쪽** 리스트와 **오른쪽** 리스트를 **다시 정렬함**
   * 분할된 부분 리스트에 대하여 **순환 호출** 을 이용하여 정렬을 반복
   * 부분 리스트에서도 다시 피벗을 정하고 피벗을 기준으로 2개의 부분 리스트로 나누는 과정을 반복함
4. 부분 리스트들이 **더 이상 분할이 불가능할 때까지** 반복
   * 리스트의 크기가 0이나 1이 될 때까지
5. 정렬된 부분 리스트를 합하여 전체가 정렬된 리스트가 되게 함

<br/>

#### 2-2. 예시

* **세부 흐름**
  * ![img](https://gmlwjd9405.github.io/images/algorithm-quick-sort/quick-sort2.png)

***

1. 배열에 5, 3, 8, 4, 9, 1, 6, 2, 7이 저장되어 있음 (오름차순으로 정렬)

2. 퀵 정렬에서 피벗을 기준으로 두 개의 리스트로 나누기

   1. 피벗 값을 입력 리스트의 첫 번째 데이터로 설정 (다른 임의의 값이어도 상관없음)
   2. 2개의 인덱스 변수(low, high)를 이용해서 리스트를 두 개의 부분 리스트로 나눔

   ***

   * 1회전 (피벗이 5인 경우)
     1. low : 왼쪽 -> 오른쪽으로 탐색해가다가, 피벗보다 큰 데이터(8)을 찾으면 멈춤
     2. high : 오른쪽 -> 왼쪽으로 탐색해가다가, 피벗보다 작은 데이터(2)를 찾으면 멈춤
     3. low와 high가 가리키는 두 데이터를 서로 교환
     4. 이 탐색-교환 과정은 low와 high가 엇갈릴 때까지 반복

   ***

3. 부분 리스트들이 더 이상 분할이 불가능할 때까지 반복

   ***

   * 2회전 (피벗이 1인 경우)
     * 피벗 : 1회전의 왼쪽 부분리스트의 첫 번째 데이터
     * 위와 동일한 방법으로 반복
   * 3회전 (피벗이 9인 경우)
     * 피벗 : 1회전의 오른쪽 부분리스트의 첫 번째 데이터
     * 위와 동일한 방법으로 반복

<br/>

* **Gif로 보는 퀵 정렬**

![img](https://t1.daumcdn.net/cfile/tistory/996DAB335ACC1BDF16)

<br/>

## 3. 퀵 정렬의 특징

* **장점**

  - 속도가 빠름
    - 시간 복잡도가 O(nlog₂n)를 가지는 다른 정렬 알고리즘과 비교했을 때도 **가장 빠름**
      - 불필요한 데이터의 이동을 줄이고 먼 거리의 데이터를 교환
      - 한 번 결정된 피벗들이 추후 연산에서 제외됨 (캐시 효율)
  - 추가 메모리 공간을 필요로 하지 않음
    - 퀵 정렬은 O(log n)만큼의 메모리를 필요로 함
  
* **단점**
  - 정렬된 리스트에 대해서는 퀵 정렬의 불균형 분할에 의해 오히려 수행시간이 더 많이 걸림
    - 퀵 정렬의 불균형 분할을 방지하기 위하여, 피벗을 선택할 때 더욱 리스트를 균등하게 분할할 수 있는 데이터를 선택해야 함
    - ex) 리스트 내의 몇 개의 데이터 중에서 크기순으로 중간 값(medium)을 피벗으로 선택

<br/>

## 4. 퀵 정렬 구현

* 오름차순 조건 예시

* ```java
  public class Quick {
      
      public void sort(int[] data, int l, int r){
          int left = l;
          int right = r;
          int pivot = data[(l+r)/2];
          
          do{
              while(data[left] < pivot) left++;
              while(data[right] > pivot) right--;
              if(left <= right){    
                  int temp = data[left];
                  data[left] = data[right];
                  data[right] = temp;
                  left++;
                  right--;
              }
          }while (left <= right);
          
          if(l < right) sort(data, l, right);
          if(r > left) sort(data, left, r);
      }
      
      public static void main(String[] args) {
          
          int data[] = {66, 10, 1, 34, 5, -10};
          
          Quick quick = new Quick();
          quick.sort(data, 0, data.length - 1);
          for(int i=0; i<data.length; i++){
              System.out.println("data["+i+"] : "+data[i]);
          }
      }
  }
  ```

  1. left = 1, right = r 로 초기화
  2. 피벗을 기준으로 좌/우 리스트 나누기
     * data[1] ~ data[left] / pivot / data[right] ~ data[data.length -1] 로 나누기
  3. 나눠진 리스트 별로 다시 위 과정 반복 (재귀)
     * if(l < right) sort(data, l, right);
     * if(r > left) sort(data, left, r);

<br/>

## 5. 퀵 정렬의 복잡도

* 최선의 경우
  * 비교 횟수
    * ![img](https://gmlwjd9405.github.io/images/algorithm-quick-sort/sort-time-complexity-etc1.png)
  * 순환 호출의 깊이
    * 레코드의 개수 n이 2의 거듭제곱이라고 가정(n=2^k)했을 때
      * n=2^3의 경우, 2^3 -> 2^2 -> 2^1 -> 2^0 순으로 줄어들어 순환 호출의 깊이가 3임을 알 수 있음
      * 이것을 일반화하면 n=2^k의 경우, k임을 알 수 있음
    * **k = log₂n**
  * 각 순환 호출 단계의 비교 연산
    * 각 순환 호출에서는 전체 리스트의 대부분의 레코드를 비교해야 함
      * 따라서 평균 n번 정도의 비교가 이루어짐
    * **평균 n번**
  * 순환 호출의 깊이 * 각 순환 호출 단계의 비교 연산 = **nlog₂n**
  * 이동 횟수
    * 비교 횟수보다 적으므로 무시할 수 있음
  * 따라서 최선의 경우 T(n) = **O(nlog₂n)**
* 최악의 경우
  * 리스트가 계속 불균형하게 나누어지는 경우
    * 특히, 이미 정렬된 리스트에 대하여 퀵 정렬을 실행하는 경우
      * ex) [1 2 3 4 5 6 7 8 9 10] 을 오름차순으로 정렬하는 프로그램
  * 비교 횟수
    * ![img](https://gmlwjd9405.github.io/images/algorithm-quick-sort/sort-time-complexity-etc2.png)
  * 순환 호출의 깊이
    * 레코드의 개수 n이 2의 거듭제곱이라고 가정(n=2^k)했을 때
      * 순환 호출의 깊이는 n임을 알 수 있음
    * **n**
  * 각 순환 호출 단계의 비교 연산
    * 각 순환 호출에서는 전체 리스트의 대부분의 레코드를 비교해야 함
      * 따라서 평균 n번 정도의 비교가 이루어짐
    * **평균 n번**
  * 순환 호출의 깊이 * 각 순환 호출 단계의 비교 연산 = **n^2**
  * 이동 횟수
    * 비교 횟수보다 적으므로 무시할 수 있음
  * 따라서 최악의 경우 T(n) = **O(n^2)**
* 평균

  * 평균 T(n) = **O(nlog₂n)**

<br/>

#### :pushpin: 추가 ) 정렬의 시간 복잡도

- [선택정렬 게시물 마지막 부분 참고](./%5BDATA%20STRUCTURE%5D%20선택정렬(Selection%20Sort).md)

<br/>

## :page_with_curl: Reference

[퀵 정렬(Quick Sort)](https://hahahoho5915.tistory.com/9)

[[알고리즘] 퀵 정렬(quick sort)이란](https://gmlwjd9405.github.io/2018/05/10/algorithm-quick-sort.html)

[5. 퀵 정렬(Quick Sort)](https://blog.naver.com/ndb796/221226813382)

[퀵소트 알고리즘 :: 마이구미](https://mygumi.tistory.com/308)

