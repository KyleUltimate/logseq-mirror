# 簡介
	- ## Ranges
		- **一大坨可迭代元素的集合**，大部分 STL 的容器都是一種 Range
	- ## Views
		- 為一種 **視圖**，可以想像成一種特殊的只讀 sub-range
	- ## Views adapter
		- 可將視圖內的元素，進行各類的轉換
- # 如何創建 range?
	- 更標準的說法，**Range Factory** - **範圍工廠**
	- 新建標頭擋，`#include <ranges>` 裡面
	- ## `std::vector`
		-
	- ## `std::views::iota`
		- 用法 `std::views::iota(from, to)`
		- `std::views::iota(1, 11)` 創建一個 Range，從 1 到 10
		- ```cpp
		  for (int i : std::views::iota(1, 11)) {
		    std::cout << i << ' ';
		  }
		  std::cout << '\n';
		  // 1 2 3 4 5 6 7 8 9 10
		  ```