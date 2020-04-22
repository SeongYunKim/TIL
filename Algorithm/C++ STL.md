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
    
## #include\<set\>

  - Set
  
    - ```set<자료형> s;```

    - **```insert(key)```: 셋에 키를 정렬된 위치에 삽입**

    - ```erase(key)```: 셋의 iterator가 가리키는 위치의 키 제거

    - ```find(key)```: 셋에서 키를 가리키는 iterator 반환

      - **키가 존재하지 않는다면 s.end() 반환**

    - iterator를 사용한 키 참조

    ```cpp
    //auto iter; 도 가능
    set<int>::iterator iter;
    for(iter = s.begin(); iter != s.end(); iter++) {
      cout << *iter << " ";
    }
    ```
  
## #include\<map\>

  - Map
  
    - ```map<key 자료형, value 자료형> m;```

    - ```insert({key, value})```: 맵에 {키, 밸류}를 정렬된 위치에 삽입

    - ```find(key)```: 맵에서 키를 가리키는 iterator 반환

      - **키가 존재하지 않는다면 m.end() 반환**

    - **```m[key] = value;```로 맵에 {키, 밸류} 삽입 또는 수정 가능**
  
## #include\<algorithm\>

  - Sort: 특정 범위의 원소들을 정렬
  
    ```cpp
    //원소의 개수가 n개인 배열 오름차순 정렬
    sort(arr, arr + n);
    //벡터 오름차순 정렬
    sort(v.begin(), v.end());
    //벡터 내림차순 정렬
    sort(v.begin(), v.end(), greater<자료형>());
    //벡터 사용자 정의 함수 사용 정렬
    bool cmp(자료형 a, 자료형 b){
      // 내림차순!!!
      return a > b;
    }
    sort(v.begin(), v.end(), cmp);
    ```
    
  - Reverse: 원소들의 순서를 역순으로
  
    ```cpp
    //원소의 개수가 n개인 배열 역순으로
    reverse(arr, arr + n);
    //벡터 원소 역순으로
    reverse(v.begin(), v.end());
    //문자열 역순으로
    reverse(s.begin(), s.end());
    ```
    
  - Binary Search: **정렬된 원소**에 대해서만 작동
  
    - ```lower_bound```: 특정 값보다 **작지 않은(크거나 같은)** 첫번째 원소의 iterator를 반환(하한)
    
    - ```upper_bound```: 특정 값보다 **큰** 첫번째 원소의 iterator 반환(상한)
    
    - 사용 예시는 [여기](https://github.com/SeongYunKim/TIL/blob/master/Algorithm/Lower%20bound%2C%20Upper%20bound.md "binary_search") 참고


  - Permutation: **정렬된 원소**에 대해서만 작동
  
    - ```next_permutation```: **다음 수열**을 구하고 true 반환. 다음 수열이 없다면 false 반환
    
    - ```prev_permutation```: **이전 수열**을 구하고 true 반환. 이전 수열이 없다면 false 반환
    
    ```cpp
    sort(v.begin(), v.end());
    do {
      for(int i = 0; i < v.size(); i++)
        printf("%d ", v[i]);
      printf("\n");
    } while(next_permutation(v.begin(), v.end());
    ```
    
    - Permutation를 사용하여 Combination 구하기
    
    1. nCr에 대해, **전체 길이가 n, 1의 개수가 r, 나머지가 0인 보조 수열** 생성
    
    2. 보조 수열에 대한 순열(next_permutation) 구하기
    
    3. 보조 수열에서 값이 1인 인덱스의 값을 원래 자료에서 추출
