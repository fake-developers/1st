# DFS&BFS

- 깊이 우선 탐색(DFS) / 너비 우선 탐색(BFS)

- **그래프를 탐색하는 방법**

  ​	:pushpin: 그래프란? 

   - 정점(node)과 그 정점을 연결하는 간선으로 이루어진 자료구조의 일종

  ​	:pushpin: 그래프 탐색 

  - 하나의 정점으로부터 시작하여 차례대로 모든 정점들을 한 번씩 방문하는 것

<BR>

## 깊이 우선 탐색(DFS)

- **최대한 깊이 내려간 뒤, 더 이상 깊이 갈 곳이 없을 경우 옆으로 이동**

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxC9Vq%2FbtqB8n5A25K%2FGyOf4iwqu8euOyhwtFuyj1%2Fimg.gif" height=300>

​													<small>출처 : https://developer-mac.tistory.com/64</small>

- 루트 노드(혹은 다른 임의의 노드)에서 시작해서 다음 분기(branch)로 넘어가기 전에 **해당 분기를 완벽하게 탐색** 하는 방식
- **모든 노드를 방문** 하고자 하는 경우 사용
- 자기 자신을 호출하는 **순환 알고리즘** 의 형태를 가짐

#### DFS의 특징

- 현 경로상의 노드만을 기억하면 되므로 저장 공간의 수요가 비교적 적다.
- BUT, 한 경로가 무한히 깊을 경우, 오버플로우 발생 가능
- 목표 노드에 도달하지 못할 가능성 존재
- 목표 노드에 도달 한다고 해도 해당 경로가 **최단 경로라는 보장이 없다.**

#### DFS의 JAVA코드

1. 스택

1. 재귀함수

   - 재귀 호출은 함수가 자기 자신을 계혹 호출하므로, 재귀 호출을 중단하도록 조건이 변경될 명령문을 반드시 포함해야한다.

   ~~~java
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
   	
   void addEdge(int v, int w) { 
   	adj[v].add(w); 
   } 
   	
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
   ~~~

<BR>

## 너비 우선 탐색(BFS)

- **최대한 넓게 이동한 다음, 더 이상 갈 수 없을 때 아래로 이동**

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc305k7%2FbtqB5E2hI4r%2Fea7vFo08tkDYo4c8wkfVok%2Fimg.gif" height="300">

​													<small>출처 : https://developer-mac.tistory.com/64</small>

- 루트 노드에서 시작해서 **인접한 노드를 먼저 탐색** 하는 방법, 시작 정점으로부터 가까운 정점을 먼저 방문하고 멀리 떨어져 있는 정점을 나중에 방문하는 순회 방법
- 두 노드 사이의 **최단 경로** 를 찾고 싶을 때 사용
- 방문한 노드들을 차례로 저장한 후 꺼낼 수 있는 자료 구조인 **큐(Queue)** 를 사용
  - 즉, **선입선출(FIFO)** 원칙으로 탐색

#### BFS의 특징

- 경로가 긴 경우 저장 공간의 수요가 매우 커짐
- 해가 존재하지 않는 경우 모든 노드의 탐색을 마치고 실패

#### BFS의 JAVA코드

1. 큐(Queue)

   ~~~java
   class Graph { 
   private int V; 
   private LinkedList<Integer> adj[]; 
   
   Graph(int v) { 
   	V = v; 
   	adj = new LinkedList[v]; 
   	for (int i=0; i<v; ++i) 
   		adj[i] = new LinkedList(); 
   } 
   
   void addEdge(int v, int w) { 
   	adj[v].add(w); 
   } 
   
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
       	int n = i.next(); 
       	
       	// 방문하지 않은 노드면 방문한 것으로 표시하고 큐에 삽입(enqueue) 
       	if (!visited[n]) { 
       		visited[n] = true; 
       		queue.add(n); 
       	} 
       } 
      } 
     } 
   }
   ~~~

<BR>

## DFS와 BFS 비교

|               | **DFS(깊이우선탐색)**                             | **BFS(너비우선탐색)**                   |
| ------------- | ------------------------------------------------- | --------------------------------------- |
| **탐색**      | 현재 정점에서 갈 수 있는 점들까지 들어가면서 탐색 | 현재 정점에 연결된 가까운 점들부터 탐색 |
| **구현**      | 스택 또는 재귀함수로 구현                         | 큐를 이용해서 구현                      |
| **검색 속도** | 상대적으로 느림                                   | 상대적으로 빠름                         |
|               | BFS 보다 간단함                                   |                                         |

- 예시) 지구 상의 존재하는 모든 친구 관계를 그래프로 표현한 후 Sam과 Eddie이라는 친구 사이의 존재하는 경로를 찾는 경우
  - 깊이 우선 탐색 : 모든 친구 관계를 다 살펴봐야할 수 도 있음
  - 너비 우선 탐색 : Sam과 가까운 관계부터 탐색

#### DFS와 BFS 시간복잡도

- 두 방식 모두 조건 내의 모든 노드를 검색한다는 점에서 **시간 복잡도는 동일**

- DFS와 BFS 둘 다 다음 노드가 방문하였는지를 확인하는 시간과 각 노드를 방문하는 시간을 합하면 된다.

- N은 노드, E는 간선일 때

  - 인접 리스트로 표현된 그래프 : O(N+E) 
  - 인접 행렬로 표현된 그래프 : O(N<sup>2</sup>)

  일반적으로 E(간선)의 크기가 N<sup>2</sup>에 비해 상대적으로 적기 때문에 **인접 리스트 방식이 효율적**

  :pushpin: 인접 리스트

  - 그래프의 연결 관계를 배열로 나타내는 방식

  :pushpin: 인접 행렬​

  - 그래프의 연결 관계를 이차원 배열로 나타내는 방식

  <small> 더 자세한 내용은 [여기](https://sarah950716.tistory.com/12)를 참고

#### DFS와 BFS를 활용한 문제 유형/응용

1. 그래프의 **모든 정점을 방문** 하는 유형
   - 단순히 모든 정점을 방문하는 것이 중요한 문제의 경우,
   - 어떤 방식을 사용해도 상관 없다.
2. **경로의 특징** 을 저장해둬야 하는 유형
   - DFS 사용
   - BFS는 경로의 특징을 가지지 못함
3. **최단거리**를 구해야 하는 유형
   - BFS 사용
   - DFS의 경우, 처음으로 발견되는 해답이 최단 거리가 아닐 수 있지만
   - BFS의 경우 현재 노드에서 가까운 곳부터 찾기 때문에 경로를 탐색 시 먼저 찾아지는 해답이 곧 최단거리

<BR>

--------

**<참조>**

- [[알고리즘] 깊이 우선 탐색(DFS) 과 너비 우선 탐색(BFS) - 튜나 개발일기](https://devuna.tistory.com/32)

- [[알고리즘] 깊이 우선 탐색(DFS) 과 너비 우선 탐색(BFS) - Yun Young's Programming Blog!](https://yunyoung1819.tistory.com/86)

- [[알고리즘] DFS / BFS](https://velog.io/@gouz7514/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-DFS-BFS)

- [[그래프] 인접 행렬과 인접 리스트](https://sarah950716.tistory.com/12)