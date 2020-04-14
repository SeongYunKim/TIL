## #include\<queue\>

- Queue

  - ```queue<자료형> q;```

  - ```push(element)```: 큐의 제일 뒤에 원소를 추가

  - ```pop()```:  큐의 제일 앞 원소 제거

  - ```front()```: 큐의 제일 앞 원소 반환

  - ```back()```: 큐의 제일 뒷 원소 반환
  
- Priority Queue

  - ```priority_queue<자료형, 구현체, 비교 연산자> pq;```
  
    - 구현체는 기본적으로 ```vector<자료형>```
    
    - 비교 연산자는 기본적으로 ```less<자료형>``` **큰 수가 top**
    
    - 비교 연산자를 ```greater<자료형>```로 지정하면 **작은 수가 top**
    
    - 자료형이 ```pair<자료형1, 자료형2>```이면 자료형1 값이 같을 때 자료형2 값에따라 우선순위 결정
    
  - ```push(element)```: 우선순위 큐에 원소를 추가
  
  - ```pop()```: 큐의 top 제거
  
  - ```top()```: 비교 연산자가 ```less<자료형>```이면 원소 중 가장 큰 수, **```greater<자료형>```이면 원소 중 가장 작은 수** 반환
  
  - 우선순위 큐에는 ```clear()``` 메소드가 없음
  
## #include\<stack\>

- Stack

  - ```stack<자료형> s;```

  - ```push(element)```: 스택의 제일 뒤에 원소를 추가

  - ```pop()```:  스택의 제일 뒷 원소 제거

  - ```top()```: 스택의 제일 뒷 원소 반환
  
## #include\<vector\>

- Vector

  - ```vector<자료형> v;```
  
  - ```v[index]```: 벡터의 index번째 원소 참조 및 수정
  
  - ```push_back(element)```: 벡터의 제일 뒤에 원소를 추가

  - ```pop_back()```:  벡터의 제일 뒷 원소 제거

  - ```begin()```: 벡터의 제일 앞 원소 가리키는 iterator 반환

  - ```end()```: 벡터의 제일 뒷 원소 가리키는 iterator 반환

  - ```v2 = v1;```로 벡터 복사
  
    - ```vector<int> v2(v1);```로 생성자를 활용한 벡터 복사도 가능
    
  - ```v1 == v2```: 두 벡터의 원소 각각이 일치하면 True 반환
  
  - ```insert(iterator, element)```: 벡터의 iterator가 가리키는 위치에 원소를 삽입(**비효율적**)
  
  - ```erase(iterator)```: 벡터의 iterator가 가리키는 위치의 원소 제거(**비효율적**)

## #include\<deque\>

- Double Ended Queue

  - ```deque<자료형> dq;```
  
  - ```dq[index]```: 덱의 index번째 원소 참조 및 수정
  
  - ```push_back(element)```: 덱의 제일 뒤에 원소를 추가
  
  - **```push_front(element)```: 덱의 제일 앞에 원소를 추가**

  - ```pop_back()```:  덱의 제일 뒷 원소 제거
  
  - ```pop_front()```: 덱의 제일 앞 원소 제거

  - ```begin()```: 덱의 제일 앞 원소 가리키는 iterator 반환

  - ```end()```: 덱의 제일 뒷 원소 가리키는 iterator 반환
  
  - ```insert(iterator, element)```: 덱의 iterator가 가리키는 위치에 원소를 삽입(**비효율적**)
  
  - ```erase(iterator)```: 덱의 iterator가 가리키는 위치의 원소 제거(**비효율적**)
  
  - 벡터는 capacity가 고갈되면 **전체 메모리 크기만큼 reallocate**하지만, 덱은 **일정 크기를 가지는 블록 단위로 확장**

    - **저장 원소가 많고 메모리 할당량이 큰 경우** 벡터에 비해 확장 비용이 작음
