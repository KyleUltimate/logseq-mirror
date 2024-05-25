## 基本概念
	- ### 型別前製
		- ```rust
		  let a: int = 5;
		  ```
		- ```cpp
		  int a = 5;
		  ```
	- ### 自動 "Cloning"
- ## 輸入輸出
	- ```cpp
	  int a; // declaration without initialization
	  int b;
	  cin >> a >> b; // right arrow
	  cout << a;
	  ```
	- cin 在新行或空格才會放入變數
- ## if 判斷式
	-
	- ```cpp
	  int a = 5;
	  int b = 5;
	  if (a==5 && b == 5) {
	    cout << "success";
	  }
	  ```
	- if 判斷式需加括號
	- 判斷式會 「短路」
- ## for 迴圈
	- ### 一般
		- ```cpp
		  for (i=0;i<=5;i++) {
		    cout << i;
		  }
		  ```
	- ### for range
		- ```cpp
		  vector<int> vec = {0,1,2,3,4};
		  for (auto x: vec) {
		  	cout << x;
		  }
		  ```
- ## 陣列
	- ### Vector
		- `.len()` -> `.size()`
		- `.push()` -> `.push_back()`
		- ```cpp
		  #include <vector>
		  using namespace std;
		  
		  vector<int> vec = {0,1,2,3,4,5}; // initilization
		  vec[0]; // direct access, automatic
		  vec.push_back(3);
		  ```
	- ### 「傳統」陣列
		- ```cpp
		  #include <array>
		  using namespace std;
		  
		  array<int, 5> = {1,2,3,4,5};
		  a[0]
		  ```
- ## Strings
	- `.contains()` -> `.find()`
	- ```cpp
	  #include <string>
	  using namespace std;
	  
	  string str = "Hello!";
	  
	  assert(str[0] == "H") // allows direct string manip
	  
	  size_t location = str.find("el"); // finds sub string, returns location
	  if (found != string::npos) {
	  	cout << "found it!"
	  }
	  ```
- ## Slicing
	- ### 迭代器
		- 創建一個新的空容器，並利用迭代器進行初始化
			- `vector<int> new(from.begin() + x, from.begin() + y)`
			- 相當於 Rust 的 `new=from[x..y]`
		- ```cpp
		  #include <iostream>
		  #include <string>
		  #include <vector>
		  #include <cassert>
		  using namespace std;
		  
		  // 字串切片範例
		  string str = "hello!";
		  string sliced_str(str.begin(), str.begin() + 4);
		  assert(sliced_str == "hell");
		  
		  // Vector 切片範例
		  vector<int> vec = {1,2,3,4,5};
		  vector<int> sliced_vec(vec.begin() + 1, vec.begin() + 3);
		  assert(sliced_vec == {2, 3});
		  
		  // array 切片範例
		  array<int,5> array = {1,2,3,4,5};
		  array<int,5> sliced_array(vec.begin() + 1, vec.begin() + 3);
		  assert(sliced_array == {2, 3});
		  ```