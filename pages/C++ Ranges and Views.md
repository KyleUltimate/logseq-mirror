# 簡介
	- ## Ranges
		- **一大坨可迭代元素的集合**，大部分 STL 的容器都是一種 Range
	- ## Views
		- 為一種 **視圖**，可以想像成一種特殊的只讀 sub-range
		- 所以，任何 range 同時也是 views
	- ## Views adapter
		- 可將視圖內的元素，進行各類的轉換，轉換後仍然是一種 **Views**
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
			- 不會 **lambda function**? 以下是用法簡介
				- lambda function 就是**匿名函數**，但可以直接存取非在其 scope 底下的變數，語法如下
				- （如果想詳細了解 capture by value 與 by reference 的差異，請先確保你理解 [[指標與參考]]）
				- > Capture By Value -  是普通函式的預設行為，會將所有的
				- ```cpp
				  int one = 1;
				  
				  int x = [=] (type x) { // `=` 在此指 capture by value， 可替換成 `&` 來表達 capture by reference
				    	return one;
				  }
				  
				  cout << x() << x() << x(); // 利用 `()` 來呼叫，可重複呼叫
				  ```
	- ## 經典
	- ## 進階