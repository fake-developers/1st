# [DATA STRUCTURE] DFS / BFS

:writing_hand: *Assembled by JiYoung-Kwon (2021-05-31)* 



#### :pushpin: 그래프​

* 정점(node)과 그 정점을 연결하는 간선(edge)으로 이루어진 자료구조의 일종
* G = (V, E)
* **그래프 탐색**
  * 하나의 정점으로부터 시작하여 차례대로 모든 정점들을 한 번씩 방문하는 것
  * ex1) 특정 도시에서 다른 도시로 갈 수 있는지 없는지
  * ex2) 전자 회로에서 특정 단자와 단자가 서로 연결되어 있는지
  * 크게 **깊이 우선 탐색(DFS)과 너비 우선 탐색(BFS)이** 있음

<br/>

## 1. 깊이 우선 탐색 (DFS)

- Depth-First Search
- 최대한 깊이 내려간 뒤, 더이상 깊이 갈 곳이 없을 경우 옆으로 이동
- ![img](https://blog.kakaocdn.net/dn/xC9Vq/btqB8n5A25K/GyOf4iwqu8euOyhwtFuyj1/img.gif)

#### 1-1. 개념

* 루트 노드(혹은 다른 임의의 노드)에서 시작해서 다음 분기(branch)로 넘어가기 전에 **해당 분기를 완벽하게 탐색**하는 방식
* ex) 미로찾기를 할 때, 최대한 한 방향으로 갈 수 있을 때까지 쭉 가다가 더 이상 갈 수 없게 되면 다시 가장 가까운 갈림길로 돌아와서 그 갈림길부터 다시 다른 방향으로 탐색을 진행하는 것

* 넓게(wide) 탐색하기 전에, 깊게(deep) 탐색함
* 모든 노드를 방문하고자 하는 경우에 이 방법을 선택함
* 깊이 우선 탐색(DFS)이 너비 우선 탐색(BFS)보다 **좀 더 간단함**
* 검색 속도 자체는 너비 우선 탐색(BFS)에 비해서 **느림**

<br/>

#### 1-2. 특징

* 자기 자신을 호출하는 순환 알고리즘의 형태
* 이 알고리즘을 구현할 때 가장 큰 차이점
  * 그래프 탐색의 경우 **어떤 노드를 방문했었는지 여부를 반드시 검사** 해야 한다는 것 
  * 이를 검사하지 않을 경우 무한루프에 빠질 위험이 있음

<br/>

#### 1-3. 과정

![img](https://t1.daumcdn.net/cfile/tistory/9983A7335BD0156910)



<br/>

## 2. 너비 우선 탐색 (BFS)

* Breadth-First Search

* **최대한 넓게 이동한 다음, 더 이상 갈 수 없을 때 아래로 이동**

* ![img](https://blog.kakaocdn.net/dn/c305k7/btqB5E2hI4r/ea7vFo08tkDYo4c8wkfVok/img.gif)

#### 2-1. 개념

* 루트 노드(혹은 다른 임의의 노드)에서 시작해서 **인접한 노드를 먼저** **탐색**하는 방법
* 시작 정점으로부터 가까운 정점을 먼저 방문하고 멀리 떨어져 있는 정점을 나중에 방문하는 순회 방법
* 깊게(deep) 탐색하기 전에, 넓게(wide) 탐색하는 것
* 주로 두 노드 사이의 **최단 경로**를 찾고 싶을 때 이 방법을 선택
* ex) 지구 상에 존재하는 모든 친구 관계를 그래프로 표현한 후 Sam과 Eddie 사이에 존재하는 경로를 찾는 경우
  * 깊이 우선 탐색의 경우 - 모든 친구 관계를 다 살펴봐야 할지도 모름
  * 너비 우선 탐색의 경우 - Sam과 가까운 관계부터 탐색

<br/>

#### 2-2. 특징

* 재귀적으로 동작하지 않음
* 방문한 노드를 차례대로 저장한 후, 꺼낼 수 있는 자료구조인 큐(Queue)를 사용
* 즉, 선입선출(FIFO) 원칙으로 탐색

<br/>

#### 2-3. 과정

* ![img](https://t1.daumcdn.net/cfile/tistory/99960F405BD01A8D18)
* 깊이가 1인 모든 노드 방문 -> 깊이가 2인 모든 노드 -> 깊이가 3인 모든 노드를 방문하는 식

<br/>



## 3. DFS VS BFS

* ![img](https://blog.kakaocdn.net/dn/cQYkI8/btqB8oDsMGe/EEYm0cKGYhxTR0kJhGiJPK/img.gif)

* |                 DFS(깊이우선탐색)                 |            BFS(너비우선탐색)            |
  | :-----------------------------------------------: | :-------------------------------------: |
  | 현재 정점에서 갈 수 있는 점들까지 들어가면서 탐색 | 현재 정점에 연결된 가까운 점들부터 탐색 |
  |             스택 또는 재귀함수로 구현             |           큐를 이용해서 구현            |



#### 3-1. 시간복잡도

* 두 방식 모두 조건 내의 모든 노드를 검색한다는 점에서 시간 복잡도는 동일

* DFS와 BFS 둘 다, 다음 노드가 방문하였는지를 확인하는 시간과 각 노드를 방문하는 시간을 합하면 됨

* N은 노드, E는 간선일 때

  > 인접 리스트 : O(N+E)
  > 인접 행렬 : O(N²)

  * 일반적으로 E(간선)의 크기가 N²에 비해 상대적으로 적기 때문에 **인접 리스트 방식이 효율적**

  * **인접 리스트**
    * 존재하는 간선의 정보만 저장되어 있으므로, 인접 행렬에서 사용한 2중 for문이 필요하지 않음
    
    * 다음 노드가 방문하였는지 확인할 때, 간선의 개수인 E의 두 배만큼의 시간이 걸림
      * 1번에서 2, 6번이 방문하였는지를 확인하고, 2번에서 1,3,6번을 방문하였는지 확인
      * 이때 1번과 2번의 간선 하나에 두 번의 확인을 하기 때문에 두 배만큼 시간이 걸림
      
    * 각 노드를 방문할 때 정점의 개수인 N만큼 시간 소요
    
    * => O(N+2*E) = **O(N+E)** (시간 복잡도에서 *계수는 삭제*.)
    
    * ```java
      void dfs(vector<int> *graph, bool *check, int x) 
      {
      
          check[x] = true;
          
          for(int i = 0; i < graph[x].size(); i++)
          {
          	int next = graph[x][i];
              if(!check[next])
              	dfs(next);
          }
      }
      
      void BFS(vector<int> *graph,int V, int start)
      {
          queue<int> q;
          bool check[V+1] = {false};
          
          check[start] = true;
          q.push(start);
          
          while(!q.empty())
          {
          	int now = q.front();
              q.pop();
              
              for(int i = 0; i < graph[now].size(); i++)
              {
                  int next = graph[now][i];
                  if(!check[next])
                  {
                  	check[next] = true;
                      q.push(next);
                  }
              }
          }
      }
  * **인접 행렬**
    * 정점의 개수 N만큼 도는 이중 for문을 돌려 두 정점 간에 **간선이 존재하는지를 확인해야 함**
    
    * 이때 N의 제곱만큼 돌게 됨 => **O(N²)**의 시간 복잡도
    
    * ```java
      void dfs(int x)
      {
          check[x] = true;
          
          for(int i = 1; i <= V ; i++)
          {
          	if(graph[x][i] == 1 && !check[i])
              	dfs(i);
          }
      }
      
      void BFS(int V, int start)
      {
          queue<int> q;
          bool check[V+1] = {false};
          
          check[start] = true;
          q.push(start);
          
          while(!q.empty())
          {
          	int now = q.front();
              q.pop();
              
              for(int i = 1; i <= V; i++)
              {
              	if(graph[now][i] == 1 && !check[i])
                  {
                  	check[i] = true;
                      q.push(i);
                  }
              }
          }
      }
      ```
    
    * 

<br/>

## 4. DFS와 BFS를 활용한 문제 유형/응용


* DFS, BFS은 특징에 따라 사용에 더 적합한 문제 유형들이 있음

1. 그래프의 **모든 정점을 방문**하는 것이 주요한 문제
   * DFS, BFS 두 가지 방법 중 어느 것을 사용해도 상관없음
   * 둘 중 편한 것을 사용
2. **경로의 특징**을 저장해둬야 하는 문제

   * ex) 각 정점에 숫자가 적혀있고, a부터 b까지 가는 경로를 구하는데 경로에 같은 숫자가 있으면 안 된다는 문제
   * 각각의 경로마다 특징을 저장해둬야 할 때는 **DFS를 사용** 
   * BFS는 경로의 특징을 가지지 못함   

3. **최단거리를** 구해야 하는 문제
   * ex) 미로 찾기
   * **BFS가 유리**
   * 깊이 우선 탐색 : 처음으로 발견되는 해답이 최단거리가 아닐 수 있
   * 너비 우선 탐색 : 경로를 탐색 시 먼저 찾아지는 해답이 곧 최단거리
     * 현재 노드에서 가까운 곳부터 찾기 때문

- 검색 대상 그래프가 **정말 크다면 DFS를 고려**
- 검색대상의 **규모가 크지 않고,** 검색 시작 지점으로부터 원하는 **대상이 별로 멀지 않다면 BFS**

<br/>

## 5. DFS와 BFS을 사용한 JAVA코드

#### 5-1. DFS 알고리즘

1. 스택 이용

2. 재귀함수 이용

   * 가장 보편적이고 짧은 코드를 작성할 수 있음

   > 재귀함수
   >
   > * 함수 내부에서 함수가 자기 자신을 또다시 호출하는 함수를 의미
   > * 재귀 호출은 자기가 자신을 계속해서 호출하므로, 끝없이 반복됨
   >   * 함수 내에 **재귀 호출을 중단하도록 조건이 변경될 명령문을 반드시 포함해야 함**

```java
/* 인접 리스트 이용 */ 
class Graph { 
    private int V; 
    private LinkedList<Integer> adj[];
    
    Graph(int v) {
        V = v; 
        adj = new LinkedList[v]; 
        // 인접 리스트 초기화 
        for (int i=0; i<v; ++i) 
            adj[i] = new LinkedList(); 
    } 
    
    void addEdge(int v, int w) { adj[v].add(w); } 
    
/* DFS */ 
    void DFS(int v) { 
        boolean visited[] = new boolean[V]; 
        
        // v를 시작 노드로 DFSUtil 재귀 호출 
        DFSUtil(v, visited); 
    } 
    
/* DFS에 의해 사용되는 함수 */ 
    void DFSUtil(int v, boolean visited[]) { 
        // 현재 노드를 방문한 것으로 표시하고 값을 출력 
        visited[v] = true; 
        System.out.print(v + " "); 
        
        // 방문한 노드와 인접한 모든 노드를 가져온다. 
        Iterator<Integer> it = adj[v].listIterator(); 
        while (it.hasNext()) {
            int n = it.next(); 
            // 방문하지 않은 노드면 해당 노드를 시작 노드로 다시 DFSUtil 호출
            if (!visited[n]) 
                DFSUtil(n, visited); 
        } 
    } 
}
```



#### 5-2. BFS 알고리즘

* 큐(Queue)를 사용

```java
class Graph { 
    private int V; 
    private LinkedList<Integer> adj[]; 
    
    Graph(int v) { 
        V = v; 
        adj = new LinkedList[v]; 
        for (int i=0; i<v; ++i) 
            adj[i] = new LinkedList(); 
    } 
    
    void addEdge(int v, int w) { adj[v].add(w); } 

/* BFS */ 
    void BFS(int s) { 
        boolean visited[] = new boolean[V]; //방문여부 확인용 변수 
        LinkedList<Integer> queue = new LinkedList<Integer>(); //연결리스트 생성 
        
        visited[s] = true; 
        queue.add(s); 
        
        while (queue.size() != 0) { 
            // 방문한 노드를 큐에서 추출(dequeue)하고 값을 출력 
            s = queue.poll();
            System.out.print(s + " "); 
            
            // 방문한 노드와 인접한 모든 노드를 가져온다. 
            Iterator<Integer> i = adj[s].listIterator(); 
            while (i.hasNext()) { 
                nt n = i.next(); 
                
                // 방문하지 않은 노드면 방문한 것으로 표시하고 큐에 삽입(enqueue) 
                if (!visited[n]) { 
                    visited[n] = true; 
                    queue.add(n); 
                } 
            } 
        } 
    } 
}
```



<br/>

## :page_with_curl: Reference

[[알고리즘] 깊이 우선 탐색(DFS) 과 너비 우선 탐색(BFS)](https://devuna.tistory.com/32)

[[알고리즘] 깊이 우선 탐색(DFS) 과 너비 우선 탐색(BFS)](https://yunyoung1819.tistory.com/86)

[[그래프] BFS와 DFS](https://velog.io/@kjh107704/%EA%B7%B8%EB%9E%98%ED%94%84-BFS%EC%99%80-DFS)

[[알고리즘] DFS / BFS](https://velog.io/@gouz7514/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-DFS-BFS)