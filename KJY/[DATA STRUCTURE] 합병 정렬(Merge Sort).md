# [DATA STRUCTURE] 합병 정렬(Merge Sort)

:writing_hand: *Assembled by JiYoung-Kwon (2021-03-22)* 



## 1. 합병 정렬이란?

- 병합정렬이라고도 함
- 하나의 리스트를 두 개의 균등한 크기로 분할하고, 분할된 부분 리스트를 정렬한 다음 두 개의 정렬된 부분 리스트를 합하여 전체가 정렬된 리스트가되게 하는 방법
- **분할 정복 알고리즘의 하나**
  * 분할 정복 방법
    * 문제를 작은 2개의 문제로 분리하고 각각 해결한 다음, 결과를 모아서 원래의 문제를 해결하는 전략
    * 분할 정복 방법은 대개 순환 호출을 이용하여 구현함
- **재귀 알고리즘 이용**
- 다음의 단계들로 이루어짐
  - **분할**
    - 입력 배열을 같은 크기의 2개의 부분 배열로 분할함
  - **정복**
    - 부분 배열을 정렬함
    - 부분 배열의 크기가 충분히 작지 않으면, **순환 호출**을 이용하여 다시 분할 정복 방법을 적용함
  - **결합**
    - 정렬된 부분 배열들을 하나의 배열에 합병함
- 2-way 병합 : 2개의 정렬된 자료 집합을 병합하는 경우
- n-way 병합 : n개의 정렬된 자료 집합을 병합하는 경우

<br/>

## 2. 합병 정렬 과정

#### 2-1. 예시 및 과정

1. 리스트의 길이가 1이 될때까지 반으로 잘게 나누기 (분할)
   * ![](https://github.com/fake-developers/1st/raw/JYJ-08/JYJ/resources/merge1.png)
2. 다 나누어졌다면, 데이터를 정렬하면서 합침 (병합)
   - 원소가 2개 -> 작은건 앞에, 큰건 뒤에
     - ![img](https://github.com/fake-developers/1st/raw/JYJ-08/JYJ/resources/merge2.png)
   - 원소가 4개 -> 첫번째 요소끼리 비교하여, 가장 작은 숫자를 새로운 그룹의 제일 앞에 둠
     - ![img](https://github.com/fake-developers/1st/raw/JYJ-08/JYJ/resources/merge4.png)
   - 그 그룹 안에 있던 나머지 수와, 다른 그룹의 첫번째 요소를 비교하여 새로운 그룹에 정렬함
     - ![img](https://github.com/fake-developers/1st/raw/JYJ-08/JYJ/resources/merge5.png)
   - 이런 식으로 새 그룹에 계속해서 정렬하며 합쳐줌
     - ![img](https://github.com/fake-developers/1st/raw/JYJ-08/JYJ/resources/merge9.png)

***

* Gif로 보는 합병정렬

  * ![img](https://github.com/fake-developers/1st/raw/JYJ-08/JYJ/resources/merge.gif)

    ***

  * ![merge_sort](https://user-images.githubusercontent.com/61674527/111326074-99a41c00-86af-11eb-9f32-af3d639ada40.gif)

<br/>

## 3. 합병 정렬의 특징

* **장점**

  - **안정적인 정렬** 방법
    - 데이터의 분포에 영향을 덜 받음
    - 즉, 입력 데이터가 무엇이든 간에 정렬되는 시간은 동일함. O(nlog2n)

* **단점**

  - 만약 레코드를 배열로 구성하면, 임시 배열이 필요함

    - **제자리 정렬 (in-place sorting)이 아님**

      \* 제자리 정렬 : 주어진 공간 외에 추가적인 공간을 사용하지 않는 정렬

  - 레코드들의 크기가 큰 경우에는 이동 횟수가 많으므로 매우 큰 시간적 낭비를 초래함

<br/>

## 4. 합병 정렬 구현

* 오름차순 조건 예시

* ```java
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

## 5. 합병 정렬의 복잡도

#### 5-1. 시간 복잡도

- 전반적인 반복의 수는 점점 절반으로 줄어들기 때문에 **O(log₂N)** 시간이 필요함
- 각 패스에서 병합할 때 모든 값들을 비교해야 하므로 **O(N)** 시간이 소모됨
- 따라서, 총 시간 복잡도는 **O(Nlog₂N)**

<br/>

#### 5-2. 공간 복잡도

- 두 개의 배열을 병합할 때 병합 결과를 담아 놓을 배열이 추가로 필요함

- 따라서, 공간 복잡도는 **O(N)**

<br/>

#### :pushpin: 추가 ) 정렬의 시간 복잡도

* [선택정렬 게시물 마지막 부분 참고](./%5BDATA%20STRUCTURE%5D%20선택정렬(Selection%20Sort).md)

<br/>

## :page_with_curl: Reference

- https://gmlwjd9405.github.io/2018/05/08/algorithm-merge-sort.html
- https://reakwon.tistory.com/38
- [https://yunmap.tistory.com/entry/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-Java%EB%A1%9C-%EA%B5%AC%ED%98%84%ED%95%98%EB%8A%94-%EC%89%AC%EC%9A%B4-Merge-Sort-%EB%B3%91%ED%95%A9-%EC%A0%95%EB%A0%AC-%ED%95%A9%EB%B3%91-%EC%A0%95%EB%A0%AC](https://yunmap.tistory.com/entry/알고리즘-Java로-구현하는-쉬운-Merge-Sort-병합-정렬-합병-정렬)
- [병합정렬(1)](https://www.daleseo.com/sort-merge/)
- [병합정렬(2)](https://yunmap.tistory.com/entry/알고리즘-Java로-구현하는-쉬운-Merge-Sort-병합-정렬-합병-정렬)
- [병합정렬(3)](https://gmlwjd9405.github.io/2018/05/08/algorithm-merge-sort.html)
- [병합정렬(4)](https://velog.io/@rachell_lee/알고리즘정렬-합병-정렬)
- [병합정렬(위키피디아)](https://dpdpwl.tistory.com/18)
- [copyOfRange(4)](https://m.blog.naver.com/PostView.nhn?blogId=rain483&logNo=220589477455&proxyReferer=https:%2F%2Fwww.google.com%2F)