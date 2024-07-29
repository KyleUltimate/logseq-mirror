# 俄羅斯方塊（C++）
- # C++ 語法補充
	- ## 結構體(struct)
		- ### 定義
			- 儲存**資料**的結構，並且每個結構體都有對其資料運用的**方法**（method）
			- 你可以把他想像為一個**設計藍圖**，設計者可以利用這個藍圖來去建立物件，換句話說 struct 是一種使用者定義的型態。
			- 資料可以是其他結構體、型別
		- ### 使用方法
			- #### 何謂建構子
			- ```cpp
			  enum Tetrominos { T, I, J, L, Z, S, O };
			  
			  struct Color {
			      float r, g, b, a;
			  };
			  
			  struct OccupiedBlock {
			      enum StatusType { Falling, Finished };
			  
			      Color color;
			      std::variant<Tetrominos, Color> data;
			      StatusType type;
			  
			      constexpr OccupiedBlock(Tetrominos mode) : type(StatusType::Falling), data(mode) {}
			      constexpr OccupiedBlock(Color color) : type(StatusType::Finished), data(color) {}
			  
			      const bool is_falling() const {
			          return type == Falling;
			      }
			  
			      const bool is_finished() const {
			          return type == Finished;
			      }
			  
			  };
			  ```
	- ## 枚舉（enum、std::variant）
		- ### 定義
			- enum -> 告訴你有哪些種類
			- std::variant -> 可以擁有含有各類型別的型別
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
		  
		  
		  enum Tetrominos { T, I, J, L, Z, S, O };
		  
		  struct Color {
		      float r, g, b, a;
		  };
		  
		  std::variant<Tetrominos, Color> data;
		  
		  auto visitor = match {
		    	// a lambada that has a reference to the type of the variant
		      [](const Tetrominos& mode) -> Color {
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
		      [](const Color& color) -> Color {
		        return color;
		      }
		  };
		  return std::visit(visitor, data);
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