## Topological Sort(위상 정렬)

- Directed Acyclic Graph(DAG)에서 **각 정점의 선행 순서를 위배하지 않으며** 모든 정점을 나열하는 것

- 알고리즘
```
1. 진입차수(특정 정점으로 갈 수 있는 간선의 수)가 0인 정점을 큐에 삽입한다.

2. 큐에서 원소를 꺼내 연결된 모든 간선을 제거한다.

3. 간선 제거 후 진입차수가 0이 된 정점을 큐에 삽입한다.

4. 큐가 빌 때까지 2~3번 과정을 반복한다. 

  - 큐가 비었을 때 모든 정점을 방문하지 않앗으면 Acyclic Graph가 아니다.
```

- C++
```cpp
void topological_sort() {
  //NODE는 정점의 개수, EDGE는 간선의 개수
  int in_degree[NODE] = { 0 };
  vector<int> edge[NODE];
  queue<int> q;
  
  for(int i = 0; i < EDGE; i++){
    edge[before].push_back(after);
    in_degree[after]++;
  }
  
  //1. 진입차수가 0인 정점을 큐에 삽입
  for(int i = 0; i < NODE; i++){
    if(in_degree[i] == 0){
      q.push(i);
    }
  }
  
  while(!q.empty){
    int cur = q.front();
    q.pop();
    //2. 큐에서 원소를 꺼내 연결된 모든 간선을 제거
    for(int i = 0; i < edge[cur].size(); i++){
      int next = edge[cur][i];
      in_degree[next]--;
      //3. 간선 제거 후 진입차수가 0이 된 정점을 큐에 삽입
      if(in_degree[next] == 0){
        q.push(next);
      }
    }
  }
}
```
