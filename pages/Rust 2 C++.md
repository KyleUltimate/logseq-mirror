## 基本概念
	- ### 型別前製
		- ```rust
		  let a: int = 5;
		  ```
		- ```cpp
		  int a = 5;
		  ```
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
		  for (int i=0;i<=5;i++) {
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
	- ### Vector（可變大小陣列）
		- #### 標頭擋
			- `#include <vector>`
		- `.len()` -> `.size()`
		- `.push()` -> `.push_back()`
		- ```cpp
		  #include <vector>
		  using namespace std;
		  
		  vector<int> vec = {0,1,2,3,4,5}; // initilization
		  vec[0]; // direct access, automatic
		  vec.push_back(3);
		  ```
	- ### 「傳統」陣列（固定大小陣列）
		- #### 標頭擋
			- `#include <array>`
		- ```cpp
		  #include <array>
		  using namespace std;
		  
		  array<int, 2> init = {0,0};
		  array<int, 2> empty; 
		  assert(empty == init);
		  ```
- ## Strings
	- ### 標頭擋
		- `#include <string>`
	- `.contains()` -> `.find()`
	- ```cpp
	  #include <string>
	  #include <cassert>
	  using namespace std;
	  
	  string str = "Hello!";
	  
	  assert(str[0] == "H") // allows direct string manip
	  
	  size_t location = str.find("el"); // finds sub string, returns location
	  if (found != string::npos) {
	  	cout << "found it!"
	  }
	  ```
- ## Slicing（切片）
	- ### 迭代器範圍構造
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
		  vector<int> ans = {2,3};
		  assert(sliced_vec == ans);
		  ```
	- ### `std::copy`
		- #### 缺點
			- 比範圍構造方法醜
			- 需先初始化大小（或利用 `std::back_inserter`）
				- `back_inserter` 簡單來說就是一直 `push_back`，因此效率不盡理想
		- #### 語法
			- `copy(from_str.begin(), from_str.begin() + 4, to_str.begin())`
			- 前兩個參數為「範圍」，第三個參數為要插入的變數之 `begin` 迭代器
		- 優點：較廣泛，能用於「傳統」陣列
		- ```cpp
		  #include <iostream>
		  #include <algorithm>
		  #include <string>
		  #include <vector>
		  #include <cassert>
		  using namespace std;
		  
		  // 字串切片範例
		  string str = "hello!";
		  string sliced_str(4); // 大小初始化方法
		  copy(str.begin(), str.begin() + 4, sliced_str.begin());
		  assert(sliced_str == "hell");
		  
		  // Vector 切片範例
		  vector<int> vec = {1,2,3,4,5};
		  vector<int> sliced_vec(2); // 大小初始化方法
		  copy(vec.begin() + 1, vec.begin() + 3, sliced_vec.begin());
		  vector<int> ans = {2,3};
		  assert(sliced_vec == ans);
		  
		  // array 切片範例
		  array<int, 5> my_array = {1,2,3,4,5};
		  array<int, 2> sliced_array;
		  std::copy(my_array.begin() + 1, my_array.end() + 3, sliced_array.begin());
		  array<int, 2> array_ans = {2,3};
		  assert(sliced_array == array_ans);
		  ```