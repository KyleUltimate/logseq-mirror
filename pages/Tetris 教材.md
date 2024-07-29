# 俄羅斯方塊（C++）
- # C++ 語法補充
	- ## 結構體(struct)
		- ### 定義
			- 儲存**資料**的結構，並且每個結構體都有對其資料運用的**方法**（method）。
			- 你可以把他想像為一個**設計藍圖**，設計者可以利用這個藍圖來去建立物件，換句話說 struct 是一種使用者定義的型態。
			- 資料可以是其他結構體、型別。
		- ### 如何宣告及使用
			- #### `this`  指標
				- 在結構體內，若需要使用對指到自己的指標，則可利用 `this` 指標，可以把她想成 `self`，指向**自己**的指標
				- 另外，對於解決結構體內與結構體外的方法重名問題，`this` 指標也是非常重要的
				- 利用 `operator->` 來得到內部
			- ```cpp
			  struct ScientificNumber {
			    	// 在一開始定義結構體要含有什麼資料
			    	double m_fraction;
			    	int m_exponent;
			    	bool m_sign;
			    
			    	// 如何初始化，在「參數」內傳入使用者所需的傳入的資料
			    	ScientificNumber(double fract, int expo): m_sign(true), m_exponent(expo), m_fraction(fract) {}
			    	// 若需使用者傳入的參數不同，則也可有重載不同的初始化方法
			    	ScientificNumber(double fract, int expo, bool sign): m_sign(sign), m_exponent(expo), m_fraction(fract) {}
			    	// 若需對使用者傳入的參數做操縱，則利用 `this` 指標做創建
			    	// **注意**: 這裡的 `this` 指標是指到尚未創建的結構體，要小心使用
			    	ScientificNumber(double number) {
			        	int exponent = std::ceil(log10(number));
			          double fraction = number/(pow(10,exponent));
			          this->m_fraction = fraction;
			        	this->m_exponent = exponent;
			        	this->m_sign = number > 0;
			      }
			    
			    	// 可以在內部創建方法，可直接存取結構體的欄位(fields)
			    	int signum() {
			        	if (m_sign) return 1;
			        	return -1;
			      }
			    
			    	// 如果遇到名稱衝突，則可利用使用 `this->signum()` 做索取
			    	double value() {
			          int sign = signum();
			       	return sign * m_fraction * pow(10, m_exponent);
			      }
			    
			    	// 若要傳回對於整個結構體的指標，可利用 `this` 指標
			    	ScientificNumber* doubled() {
			    		this->m_fraction *= 2;
			        	return this;
			      }
			  };
			  int main() {
			    	auto num = ScientificNumber { 0.8772, 82 };
			    	// 對於得到的結構體，可利用 `operator.` 來執行其方法
			    	std::cout << num.value() << "\n";
			     	auto num_ref = &num;
			    	// 對於得到結構體參考（或是指針），可利用 `operator->` 來執行其方法
			    	std::cout << num_ref->value();
			  }
			  ```
	- ## 枚舉（enum、std::variant）
		- ### std::variant
			- 定義：可以擁有含有各類型別的型別，可以想為型別安全版的 union
				- `std::variant<int, double, string>`
			- ```cpp
			  ```
		- ### enum
			- 告訴你有哪些種類
			- ```cpp
			  enum Tetrominos { T, I, J, L, Z, S, O };
			  int get_str() {
			    	// 利用 `::` 來存取欄位(field)
			    	auto block = Tetrominos::T;
			      switch (mode) {
			          using B = Tetrominos;
			        case B::T: ;
			        case B::I: return {0.40, 0.75, 1.00, 1.00};
			        case B::J: return {1.00, 0.63, 0.00, 1.00};
			        case B::L: return {0.00, 0.47, 0.95, 1.00};
			        case B::Z: return {0.00, 0.89, 0.19, 1.00};
			        case B::S: return {0.90, 0.16, 0.22, 1.00};
			        case B::O: return {0.99, 0.98, 0.00, 1.00};
			      }
			  }
			  ```
		- ###  與 struct 一起用的方式
		- 看不懂沒有關係，不一定要這樣寫，對於小型專案而言，可以不必那麼在乎型別安全
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