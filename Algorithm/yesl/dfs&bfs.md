# 깊이/너비 우선 탐색(DFS/BFS)

### DFS(깊이 우선 탐색)

- DFS는 (Depth - First Search), 깊이 우선 탐색이라고도 부른다.
- 스택(또는 재귀 함수)을 사용하여 구현할 수 있으며, 그래프와 트리의 깊은 부분을 우선적으로 탐색하는 알고리즘이다.

**동작과정**

- 한 정점에서 시작해 다음 경로로 넘어가기 전에 해당 경로를 완벽하게 탐색할 때 사용한다.
  > 1. 탐색 시작 노드를 스택에 삽입하고 방문 처리를 한다.
  > 2. 스택의 최상단 노드에 방문하지 않은 인접 노드가 있으면 그 인접 노드를 스택에 넣고 방문 처리를 한다.
  > 3. 그리고 방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 꺼낸다.
  > 4. 두 번째 과정을 더 이상 수행할 수 없을 때까지 반복한다.

**특징**

- 스택 자료 구조에 기초하며, 구현할 때 재귀 함수로 구현하는 것이 좀더 간편하다.
- 경로의 특징을 저장하면서 탐색하는 문제에 적합하다.
- DFS를 구현할 때, 그래프 탐색의 경우 어떤 노드를 방문했었는지 여부를 검사하지 않을 시 무한 루프에 빠질 위험이 있으므로 반드시 검사해야한다.
- 미로를 탐색할 때, 해당 분기에서 갈 수 있을 때까지 계속 가다가 더 이상 갈 수 없게 되면 다시 가장 가까운 갈림길로(새로운 분기)로 돌아와서 다른 방향으로 다시 탐색을 진행하는 방법과 유사하다.
- 모든 경우를 하나하나 다 탐색을 해야될경우 사용한다. ( 순열, 조합 구현 )
- 검색 속도 자체는 BFS에 비해 느리다.

### BFS(너비 우선 탐색)

- BFS는 (Breadth - First Search), 너비 우선 탐색이라고도 부른다.
- 큐를 사용하여 구현되며, 그래프와 트리의 가까운 노드부터 탐색하는 알고리즘이다.

**동작과정**

- 한 정점에서 가장 인접한 노드를 먼저 넓게 탐색하면서 깊이 내려간다.

  > 1. 탐색 시작 노드를 큐에 삽입하고 방문 처리를 한다.
  > 2. 큐에서 노드를 꺼내 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입하고 방문 처리를 한다.
  > 3. 두 번째 과정을 더 이상 수행할 수 없을 때까지 반복한다.

**특징**

- 재귀적으로 동작하지 않습니다.
- 모든 인접 노드를 동일한 거리에서 탐색한다.
- BFS도 DFS처럼 노드 방문 여부를 반드시 검사해야합니다.
- 방문한 노드들을 차례로 저장한 후 꺼낼 수 있는 선입 선출 자료구조 큐를 사용합니다. (선입선출 원칙으로 탐색)
- 큐를 사용하여 구현하며, DFS보다 구현이 조금 더 복잡할 수 있다.
- 최단경로(다익스트라, 플로이드)를 찾거나, 노드와 노드 사이의 최단 거리를 구할 때 유용하다.

### DFS와 BFS 차이

<img width="500" alt="dfs와bfs 차이" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F997C3C3E5BD01AF41D">

### DFS와 BFS 구현 방법

**그래프 표현**

```
const graph = {
  A: ["B", "C"],
  B: ["A", "D", "E"],
  C: ["A", "F"],
  D: ["B"],
  E: ["B", "F"],
  F: ["C", "E"]
};
```

**DFS 구현**

```
function dfs(graph, node, visited = new Set()) {
  // 현재 노드를 방문 처리
  visited.add(node);

  console.log(node); // 현재 노드 출력

  // 현재 노드에 인접한 모든 노드에 대해
  graph[node].forEach(neighbor => {
    // 아직 방문하지 않았다면 재귀적으로 방문
    if (!visited.has(neighbor)) {
      dfs(graph, neighbor, visited);
    }
  });
}

// DFS 실행 예
dfs(graph, 'A');
```

**BFS 구현**

```
function bfs(graph, start) {
  const visited = new Set(); // 방문한 노드를 추적하는 집합
  const queue = [start]; // 시작 노드를 큐에 추가

  while (queue.length > 0) {
    const node = queue.shift(); // 큐에서 하나의 노드를 꺼냄

    if (!visited.has(node)) {
      visited.add(node); // 노드를 방문 처리
      console.log(node); // 현재 노드 출력

      // 현재 노드에 인접한 모든 노드를 큐에 추가
      graph[node].forEach(neighbor => {
        if (!visited.has(neighbor)) {
          queue.push(neighbor);
        }
      });
    }
  }
}

// BFS 실행 예
bfs(graph, 'A');
```