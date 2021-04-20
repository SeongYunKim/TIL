## #include \<string\>

- String

  - ```string s = "String";```
  
    - string은 char\*, char[]과 달리 **문자열 끝에 '\0'이 없음**
  
  - ```s[index]```: 문자열의 index번째 문자 참조 및 수정
  
  - ```size()```, ```length()```: 문자열의 길이 반환
  
  - ```c_str()```: C++ 스타일의 string 문자열을 C 스타일의 문자열로 변환
  
    - "String"을 "String\0"로 변환
    
  - ```substr(index, len)```: 문자열의 **index번째 문자부터 길이가 len인 부분 문자열**을 반환
  
  - ```compare(str)```: 문자열이 str과 **일치하면 0 반환, 일치하지 않으면 0이 아닌 값 반환**
  
    - 문자열이 str보다 작으면(사전순 빠르면) 음수(-1) 반환
    
    - 문자열이 str보다 크면(사전순 느리면) 양수(1) 반환
    
  - ```replace(index, len, str)```: 문자열의 index번째 문자부터 길이가 len인 부분 문자열을 str로 대체
  
  - ```find(str)```: 문자열에 str과 일치하는 부분 문자열이 존재하는지 검사
  
    - 일치하는 부분 문자열이 존재하면 부분 문자열의 시작 인덱스를 반환
    
    - 일치하는 부분 문자열이 존재하지 않으면 -1 반환
    
  - ```push_back(c)```: 문자열의 제일 뒤에 문자 c 추가
  
    - 연산 속도가 느리므로 **+ 연산자 사용 권장**
  
  - ```pop_back()```: 문자열의 제일 뒷 문자 제거 
  
## #include \<cstring\>

- Cstring

  - ```memset(ptr, value, size)```: **바이트 단위**로 메모리를 초기화
  
    - **1 바이트 변수(char, unsigned char 등)가 아닌 변수를 초기화할 때는 0, -1 이외의 값으로 초기화 금지!!**
    
    ```cpp
    //정수 배열을 0으로 초기화
    int arr1[100][100];
    memset(arr1, 0, sizeof(arr1));
    //정수 배열을 -1로 초기화
    int arr2[100][100];
    memset(arr2, -1, sizeof(arr2));
    //정수 배열을 2139062143(int형 최대 크기가 2147438647)로 초기화
    int arr3[100][100];
    memset(arr3, 0x7f, sizeof(arr3))
    ```
