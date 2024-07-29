# 俄羅斯方塊（C++）
- # C++ 語法補充
	- ## 結構體(struct)
		- ### Constructor(member initializer list)
	- ## 枚舉（enum class、std::variant）
		- enum -> 告訴你有哪些種類
		- std::variant -> 可以擁有含有型別的型別
			- `std::variant<int, double, string>`
			- 可以想為型別安全版的 union
		- ###  用法
		- ```cpp
		  // Utility to allow overloading lambdas for use in std::visit
		  template<class... Ts>
		  struct match : Ts... {
		      using Ts::operator()...;
		  };
		  template<class... Ts>
		  match(Ts...) -> match<Ts...>;
		  
		  #define path(T, K) [&](const T& K)
		  
		  enum Tetrominos { T, I, J, L, Z, S, O };
		  
		  struct Color {
		      float r, g, b, a;
		  };
		  
		  auto visitor = match {
		    path(Tetrominos, mode) -> Color {
		      switch (mode) {
		          using B = Tetrominos;
		          case B::T: return {0.78, 0.48, 1.00, 1.00};
		          case B::I: return {0.40, 0.75, 1.00, 1.00};
		          case B::J: return {1.00, 0.63, 0.00, 1.00};
		          case B::L: return {0.00, 0.47, 0.95, 1.00};
		          case B::Z: return {0.00, 0.89, 0.19, 1.00};
		          case B::S: return {0.90, 0.16, 0.22, 1.00};
		          case B::O: return {0.99, 0.98, 0.00, 1.00};
		      }
		    },
		    path(Color, color) -> Color {
		      return color;
		    }
		  };
		  return std::visit(visitor, block->data);
		  ```
	- ## std::span
		- ### 定義
			- 不可寫的連續的一塊記憶體
		- ### 適用於
			- 函式參數，能使使用者傳入各式資料型態
		- ## 用法
			- ```cpp
			  void printSpan(std::span<int> span) {
			      for (const auto& elem : span) {
			          std::cout << elem << " ";
			      }
			      std::cout << "\n";
			  }
			  int main() {
			    	// Create a vector
			      std::vector<int> vec = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
			      std::cout << "Vector span: ";
			      printSpan(vec);
			    
			    	// Create a subspan from the vector (starting at index 2, length 5), does not reallocate array
			      std::span<int> subSpan(vec.begin() + 2, 5); // {3, 4, 5, 6, 7}
			      std::cout << "Sub span: ";
			      printSpan(subSpan);
			  
			      // Create a std::array
			      std::array<int, 5> stdArray = {11, 12, 13, 14, 15};
			      std::cout << "std::array span: ";
			      printSpan(stdArray);
			  }
			  ```
- # 俄羅斯方塊術語與規則介紹
	- ## ARR
	- ## DAS
	- ## 旋轉機制
- # 難點攻關
- ## 1. 旋轉如何實施？
- 直接把旋轉完的方塊 array 寫在程式碼中
- 根據每個不同的方塊，撰寫獨立的旋轉軸(pivot)