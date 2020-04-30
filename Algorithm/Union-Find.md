## Union-Find

- Disjoint Set이란?

  - 서로 중복되지 않는 **서로소 부분집합**들로 나눠진 원소들에 대한 정보를 저장하는 자료구조
  
- Disjoint Set의 연산

  - Make-set(x): 주어진 원소(x)를 유일한 원소로 하는 새로운 집합을 만든다.

  - Union(x, y): x와 y가 속한 두개의 Disjoint Set을 하나로 합친다.
  
  - Find(x): 주어진 원소(x)가 속한 **집합(의 대푯값, 주로 루트 노드 값)을 반환**한다.
  
- Union-Find 구현 방식

  - 배열
  
    - arr[i]: i번 원소가 속하는 집합 번호를 저장
    
    - Make-set(x): arr[i] = i와 같이 자기 자신으로 초기화
    
    - Union(x, y): **배열의 모든 원소를 순회**하며 y의 집합번호를 x의 집합번호로 값을 변경 **(O(n))**
    
    - Find(x): arr[x]가 저장하고 있는 값을 반환 **(O(1))**
    
  - 트리
  
    - 같은 집합=하나의 트리, **집합 번호=루트 노드 값**
    
    - Make-set(x): 모든 원소에 대한 루트 노드를 생성하고 자기 자신으로 초기화
    
    - Union(x, y): x와 y의 **루트 노드를 찾고** 다르면, y 트리를 x 트리의 자손으로 병합
    
      - 두 노드의 루트 노드를 찾는 **Find 연산이 시간복잡도 지배**
    
    - Find(x): 루트 노드 값 반환 (**최악의 경우 O(n-1)**)

- Union-Find 구현

```cpp
int root[MAX_SIZE];
for(int i = 0; i < MAX_SIZE; i++)
  root[i] = i;
  
int find(int x) {
  if(root[x] == x)
    return x;
  else
    //find 하며 만난 모든 노드의 부모 노드를 루트 노드로!!
    return root[x] = find(root[x]);
}

void union(int x, int y) {
  x = find(x);
  y = find(y);
  if(x != y)
    root[y] = x;
}
```
