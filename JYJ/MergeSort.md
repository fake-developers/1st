# 합병 정렬 (Merge Sort)

:writing_hand: *Assembled by Yunju Jang*

🤝*Contributors : JiYe Bae*

<hr>


## 합병 정렬 (Merge Sort)

- <b>합병 정렬 (병합 정렬) 이란?</b>

  - 하나의 리스트를 두 개의 균등한 크기로 분할하고, 분할된 부분 리스트를 정렬한 다음 두 개의 정렬된 부분 리스트를 합하여 전체가 정렬된 리스트가되게 하는 방법이다.
    
  - 분할 정복 알고리즘의 하나이다.

    > 분할 정복 방법
    >
    > - 문제를 작은 2개의 문제로 분리하고 각각 해결한 다음, 결과를 모아서 원래의 문제를 해결하는 전략이다.
    > - 분할 정복 방법은 대개 순환 호출을 이용하여 구현한다.

  - 다음의 단계들로 이루어진다.

    - 분할 : 입력 배열을 같은 크기의 2개의 부분 배열로 분할한다.
    - 정복 : 부분 배열을 정렬한다. 
      - 부분 배열의 크기가 충분히 작지 않으면 <b>순환 호출</b>을 이용하여 다시 분할 정복 방법을 적용한다.
    - 결합 : 정렬된 부분 배열들을 하나의 배열에 합병한다.

  <br/>

  <br/>

- <b>합병 정렬 과정</b>

  - 리스트의 길이가 1이 될때까지 반으로 잘게 나눈다. (분할)
  
    <img src='resources/merge1.png' width='400px' align='center'>
  
  - 다 나누어졌다면, 데이터를 정렬하면서 합친다. (병합)
  
    - 원소가 2개 -> 작은건 앞에, 큰건 뒤에
  
      <img src='resources/merge2.png' width='300px' align='center'>
  
    - 원소가 4개 -> 첫번째 요소끼리 비교하여 가장 작은 숫자를 새로운 그룹의 제일 앞에 둔다. 
  
      <img src='resources/merge3.png' width='300px' align='center'>
  
      <img src='resources/merge4.png' width='300px' align='center'>
  
      - 그 그룹 안에 있던 나머지 수와, 다른 그룹의 첫번째 요소를 비교하여 새로운 그룹에 정렬한다.
  
        <img src='resources/merge5.png' width='300px' align='center'>
  
        <img src='resources/merge6.png' width='300px' align='center'>
  
      - 이런 식으로 새 그룹에 계속해서 정렬하며 합쳐준다.
  
        <img src='resources/merge8.png' width='300px' align='center'>
  
        <img src='resources/merge9.png' width='300px' align='center'>
  
      
  
      
  
  <img src='resources/merge.gif' width='500px' align='center'>

<br/>

<br/>

- <b>병합 정렬 예제 코드</b>

  ``` java
  public class MergeSort {
      public static int[] src;
      public static int[] tmp;
  
      public static void main(String[] args) {
          src = new int[]{1, 9, 8, 5, 4, 2, 3, 7, 6};
          tmp = new int[src.length];
          printArray(src);
          mergeSort(0, src.length - 1);
          printArray(src);
      }
  
      public static void mergeSort(int start, int end) {
          if (start < end) {
              int mid = (start + end) / 2;
              mergeSort(start, mid);
              mergeSort(mid + 1, end);
              int p = start;
              int q = mid + 1;
              int idx = p;
              while (p <= mid || q <= end) {
                  if (q > end || (p <= mid && src[p] < src[q])) {
                      tmp[idx++] = src[p++];
                  } else {
                      tmp[idx++] = src[q++];
                  }
              }
              for (int i = start; i <= end; i++) {
                  src[i] = tmp[i];
              }
          }
      }
  
      public static void printArray(int[] a) {
          for (int i = 0; i < a.length; i++)
              System.out.print(a[i] + " ");
          System.out.println();
      }
  }
  
  // 실행결과
  // 1 9 8 5 4 2 3 7 6  --> 정렬 전
  // 1 2 3 4 5 6 7 8 9  --> 정렬 후
  ```

  <br/>

  <br/>

- <b>합병 정렬의 특징</b>
  
    - 장점
      
        - 안정적인 정렬 방법이다.
          - 데이터의 분포에 영향을 덜 받는다. 즉, 입력 데이터가 무엇이든 간에 정렬되는 시간은 동일하다. (O(nlog<small>2</small>n)으로 동일)
        
        <br/>
    - 단점
      - 만약 레코드를 배열로 구성하면, 임시 배열이 필요하다.
      
        - 제자리 정렬 (in-place sorting)이 아니다.
      
          \* 제자리 정렬 : 주어진 공간 외에 추가적인 공간을 사용하지 않는 정렬
      
          
      
      - 레코드들의 크기가 큰 경우에는 이동 횟수가 많으므로 매우 큰 시간적 낭비를 초래한다.


<br/>

<br/>

## 예상질문❔

Q1) 합병 정렬이란 무엇인가?

A1) 하나의 리스트를 두 개의 균등한 크기로 분할하고, 분할된 부분 리스트를 정렬한 다음 두 개의 정렬된 부분 리스트를 합하여 전체가 정렬된 리스트가되게 하는 방법이다.

<br/>

<br/>

### Reference📖

- https://gmlwjd9405.github.io/2018/05/08/algorithm-merge-sort.html
- https://reakwon.tistory.com/38
- https://yunmap.tistory.com/entry/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-Java%EB%A1%9C-%EA%B5%AC%ED%98%84%ED%95%98%EB%8A%94-%EC%89%AC%EC%9A%B4-Merge-Sort-%EB%B3%91%ED%95%A9-%EC%A0%95%EB%A0%AC-%ED%95%A9%EB%B3%91-%EC%A0%95%EB%A0%AC

