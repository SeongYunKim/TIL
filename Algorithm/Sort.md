# Sort Algorithm

> CS 전공이면 Merge, Quick, Heap Sort는 구현할 줄 알아야지?

## Merge Sort
  
  - Divde and Conquer
   
    - Divide: 배열을 반으로 분할
    
    - Conquer: 분할한 배열을 각각 정렬, 분할한 배열의 원소가 2개 이상이면 ```재귀 호출을 사용하여 다시 Divide and Conquer```
    
    - Combine: 정렬된 부분 배열들을 하나의 배열로 합병하며 정렬
    
  - 시간 복잡도
  
    - T(n) = 2*T(N/2) + O(n)
    
    - 위 점화식에 의해, ```Ω(n log(n)), θ(n log(n)), O(n log(n))```
    
  - k-way Merge Sort
  
    - [블로그 잠시할 때 작성했던 글](https://pro-programmer.tistory.com/entry/kway-Merge-Sort%ED%95%A9%EB%B3%91-%EC%A0%95%EB%A0%AC%EC%9D%98-%EC%8B%9C%EA%B0%84%EB%B3%B5%EC%9E%A1%EB%8F%84-%EA%B3%84%EC%82%B0%ED%95%98%EA%B8%B0 "k-way Merge Sort")을 참고하시라
  
  - 구현
  
  ```cpp
  void merge(int arr[], int l, int m, int r) {
	int n1 = m - l + 1;
	int n2 = r - m;
	//임시 배열에 원소 복사
	int tempLeft[100], tempRight[100];
	for (int i = 0; i < n1; i++)
	  tempLeft[i] = arr[l + i];
	for (int i = 0; i < n2; i++)
	  tempRight[i] = arr[m + 1 + i];
	//임시 배열 합병
	int i = 0, j = 0, k = l;
	while (i < n1 && j < n2) {
	  if (tempLeft[i] <= tempRight[j])
	    arr[k++] = tempLeft[i++];
	  else
	    arr[k++] = tempRight[j++];
	}
	//남은 임시 배열 원소 복사
	while (i < n1)
	  arr[k++] = tempLeft[i++];
	while (j < n2)
	  arr[k++] = tempRight[j++];
}

void mergeSort(int arr[], int l, int r) {
	if (l < r) {
	  // (l + r) / 2와 같지만 자료형 오버플로우 방지 위해
	  int m = l + (r - l) / 2;  //Divide
	  mergeSort(arr, l, m);     //Conquer
	  mergeSort(arr, m + 1, r); //Conquer
	  merge(arr, l, m, r);      //Combine
   }
}
  ```
## Heap Sort

## Quick Sort

