## Lower bound

- lower_bound란?

  - Binary Search 기반의 탐색 방법(정렬되어 있는 데이터 필요)
  
  - 찾고자 하는 **key값이 없으면 key값보다 큰 가장 작은 수의 위치를 탐색**
  
  - 같은 원소 여러개있어도 유일한 해를 구할수 있음
  
- 직접 구현한 lower_bound

```cpp
int lower_bound(int key){
  int start = 0;
  int end = n;
  int mid;
  
  while(end > start) {
    mid = (start + end)/2;
    if(arr[mid] < key)
      start = mid + 1;
    //key가 arr[mid]보다 작거나 같을 때 mid - 1이 아닌 mid!
    else
      end = mid;
  }
  return end;
}
```

- STL에서 제공하는 lower_bound

```cpp
template <class ForwardIterator, class T>
ForwardIterator lower_bound (ForwardIterator first, ForwardIterator last, const T&val);
```

```cpp
#include <algorithm>

int main() {
  printf("index: %d value: %d\n", lower_bound(arr, arr + n, key) - arr, arr[lower_bound(arr, arr + n, key) - arr]);
  printf("index: %d ", lower_bound(v.begin(), v.end(), key) - v.begin());
  auto it = lower_bound(v.begin(), v.end(), key);
  printf("value: %d\n", *it);
}
```

## Upper bound

- upper_bound란?

  - Binary Search 기반의 탐색 방법(정렬되어 있는 데이터 필요)
  
  - **key값을 초과하는 가장 작은 수(첫번째 원소)의 위치를 탐색**
  
  - 같은 원소 여러개있어도 유일한 해를 구할수 있음
  
- 직접 구현한 upper_bound

```cpp
int upper_bound(int key){
  int start = 0;
  int end = n;
  int mid;
  
  while(end > start) {
    mid = (start + end)/2;
    if(arr[mid] <= key)
      start = mid + 1;
    //key가 arr[mid]보다 작을 때 mid - 1이 아닌 mid!
    else
      end = mid;
  }
  return end;
}
```
- STL에서 제공하는 upper_bound

```cpp
template <class ForwardIterator, class T>
ForwardIterator upper_bound (ForwardIterator first, ForwardIterator last, const T&val);
```

```cpp
#include <algorithm>

int main() {
  printf("index: %d value: %d\n", upper_bound(arr, arr + n, key) - arr, arr[upper_bound(arr, arr + n, key) - arr]);
  printf("index: %d ", upper_bound(v.begin(), v.end(), key) - v.begin());
  auto it = upper_bound(v.begin(), v.end(), key);
  printf("value: %d\n", *it);
}
```

### 참고

- http://www.cplusplus.com/reference/algorithm/lower_bound/

- http://www.cplusplus.com/reference/algorithm/upper_bound/

