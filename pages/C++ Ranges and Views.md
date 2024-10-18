# Programming Paradigms
	- ## Procedural Programming
	  id:: 671267b9-aae8-45cd-8b3a-4eb37b055d1a
	- ## Object Oriented Programming
	- ## Functional Programming
	- ## **Collection** Oriented Programming
- # 簡介
	- ## Ranges
		- **一大坨可迭代元素的集合**，大部分 STL 的容器都是一種 Range
	- ## Views
		- 為一種 **視圖**，可以想像成一種特殊的只讀 sub-range
		- 所以，任何 range 同時也是 views
	- ## Views adapter
		- 可將 Views 內的元素，進行各類的轉換，轉換後仍然是一種 **Views**
		- 可利用 `pipe |` operator 進行串接
	- 以上概念，都被包括在 `#include <ranges>` 裡面
- # 如何創建 range?
	- 更標準的說法，**Range Factory** - **範圍工廠**
	- ## Range 的 `for` 迴圈語法
		- `for(auto x: [range]) { .. }`
		- 創建一個變數，從 range 裡面迭代過去
	- ## `std::vector`
		- 沒錯! vector 本身也是一種 range!（畢竟她也是 STL 容器）
		- ```cpp
		  vector<int> v = {1,3,4,5};
		  for (auto x: v) {
		    std::cout << x << ' ';
		  }
		  // 1 3 4 5
		  ```
	- ## `std::views::iota`
		- 用法 `std::views::iota(from, to)`
		- `std::views::iota(1, 11)` 創建一個 Range，從 1 到 10
		- ```cpp
		  for (int i: std::views::iota(1, 11)) {
		    std::cout << i << ' ';
		  }
		  // 1 2 3 4 5 6 7 8 9 10
		  ```
- # Views adapters
	- 先介紹一些經典的 adapters（在 C++ 20 推出的）
	- 後半部則是較新穎（在 C++ 23 才推出的）adapters
	- ## 術語
		- `func`：在此教材中，指的是任意的**可呼叫物件**，可以是 lambda function、函式指針
			- **可呼叫物件**是任何可以用此語法 `x()` 呼叫的物件
			- 不會 **lambda function** ? 以下是用法簡介
				- lambda function 就是**匿名函數**，但可以直接存取非在其 scope 底下的變數，語法如下
				- （如果想詳細了解 capture by value 與 by reference 的差異，請先確保你理解 [[指標與參考]]）
				  collapsed:: true
					- > Capture By Value -  是普通函式的預設行為，會將所有用的值，**複製**一份到 lambda 裡面
					- > Capture By Reference - 會讓所有使用這個 lambda 的地方，**共用一塊記憶體**，形同參考
				- ```cpp
				  int one = 1;
				  
				  // 中括號內的 `&` 在此指 capture by reference，可替換成 `=` 來表達 capture by value。
				  // 小括號的是此 lambda 的參數，如同普通函式一般，可以有無限量的參數數量
				  int func = [&] (int x) {
				    	return one + x;
				  };
				  
				  cout << func(3) << func(7) << func(2); // 利用 `()` 來呼叫，可重複呼叫
				  // 4 8 3
				  ```
	- ## 經典
		- ### `std::views::transform(func)`
		- ### `std::views::filter(func)`
		- ### `std::views::take(int)`
		- ### `std::views::enumerate`
			- 意義：將 range 的 index 給「枚舉」出來
			- 如果要輸出 vector 裡的每個 element，有兩種方法。
				- 傳統 for loop
					- ```cpp
					  vector<string> v = {"a", "b", "c", "d"}
					  
					  // 傳統 for loop
					  for(int i = 0; i<v.size();i++) {
					    	cout << v[i] << " ";
					  }
					  ```
				- for range
					- ```cpp
					  vector<string> v = {"a", "b", "c", "d"}
					  
					  // ranges based for loop
					  for(int x: v) {
					    	cout << x << " ";
					  }
					  ```
			- 如果同時要輸出 index 則只能使用傳統 for loop
			- `views::enumerate` 將每個 element 從 `element` 轉化成 `[index, element]`
			- 有了 `views::enumerate` 之後，就可以做以下動作
				- ```cpp
				  vector<string> v = {"a", "b", "c", "d"}
				  
				  // 這種方式叫做 `de-structring`，可以叫方便的獲取
				  for(auto [index, element]: v | views::enumerate) {
				    	cout << index << ':' << element << '\n';
				  }
				  ```
		- ### `std::views::adjacent_transform(func)`
		- ### `std::views::chunk(int)`
	- ## 進階
		- ### `std::views::chunk_by(func)`
		- ### `std::ranges::to<type>`
- # Ranges algorithms
	- #+BEGIN_IMPORTANT
	  跟 Views adapters 差在輸出**不能**使用 `|` 來串接。
	  有時甚至輸出的連 range 都不是。
	  #+END_IMPORTANT
	- ## `std::ranges::all_of`
	- ## `std::ranges::any_of`
	- ## `std::ranges::accumulate`
	- ## `std::ranges::fold_left`
		- 可以視為，有著「記憶」的 for loop
		- 結果：把所有 elements 給 「折起來」"fold" 成一個數值
		- 語法：`fold_left(vec, func(accumulater,x))`
			- `func(accumulater,x)` 指的是，擁有兩個參數的一個可呼叫物件
		- `std::ranges::fold_left_first`
	-
- # 題目練習
	- #+BEGIN_IMPORTANT
	  要注意，因為多數競程平台（甚至 IDE）都尚不支援 C++ 23 標準
	  將你的程式碼丟上去會編譯失敗!
	  #+END_IMPORTANT
	- https://zerojudge.tw/ShowProblem?problemid=o076