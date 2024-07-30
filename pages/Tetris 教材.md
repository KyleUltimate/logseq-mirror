# C++ 語法補充
	- ## lambda
	- ## std::optional
	  collapsed:: true
		- ### 定義
		  collapsed:: true
			- 一個指標，代表所其指到一個值可能是存在或不存在的。
			- 在標頭擋裡 `optional`
		- ### 用法
		  collapsed:: true
			- 若為無，將其值設為 `std::nullopt`
			- 以 `.has_value()` 確認其值是否存在
			- 以 `.value()` 得到其值
			- ```cpp
			  #include <optional>
			  #include <iostream>
			  
			  // 以 `std::optional<type>` 來代表
			  std::optional<int> fetch_bank_account(name: std::string) {
			    	switch name {
			        	case "kyle": return 334,
			        	case "kevin": return 221,
			        	case "amy": return 209,
			        	default: return std::nullopt
			      }
			  }
			  
			  int main() {
			    	std::optional<int> bank_account = fetch_bank_account("kyle");
			    	
			    	// 第一種存取方法，不倚賴自動型別轉換
			    	if (bank_account.has_value()) {
			        	std::cout << bank_account.value();
			      }
			    
			    	// 第二種，較方便使用，要注意，因為拿回來的是指標，所以必須利用 `operator*` 來執行解參考
			    	// 或是 `operator->` 來存取 struct 的方法(method)與欄位(field)
			    	if (auto val = bank_account) {
			        	std::cout << *val;
			      }
			    	
			  }
			  ```
	- ## 結構體(struct)
	  id:: 66a7a403-20df-4ce1-86a6-75cef5c3640e
		- ### 定義
			- 儲存**資料**的結構，並且每個結構體都有對其資料運用的**成員方法**（method）。
			- 你可以把他想像為一個**設計藍圖**，設計者可以利用這個藍圖來去建立物件，換句話說 struct 是一種使用者定義的型態。
			- 資料可以是其他結構體、型別。
		- ### 如何宣告及使用
			- 使用者端如何使用請參考下方 `main` 函數的使用方式。
			- #### `this`  指標
				- 在結構體內，若需要使用對指到自己的指標，則可利用 `this` 指標，可以把她想成 `self`，指向**自己**的指標
				- 另外，對於解決結構體內與結構體外的方法重名問題，`this` 指標也是非常重要的
				- 利用 `operator->` 來得到內部方法及資料欄位，而非普通的 `operator.`
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
			    	// 對於得到的結構體，可利用 `operator.` 來執行其方法，或得到其欄位
			    	std::cout << num.m_sign << " " << num.value() <<  "\n";
			     	auto num_ref = &num;
			    	// 對於得到結構體參考（或是指針），可利用 `operator->` 來執行其方法
			    	std::cout << num_ref->value();
			  }
			  ```
		- ### tl;dr
			- **結構體**：是一種自定義的數據類型，用於儲存和操作相關的數據。
			- **宣告及使用**：通過構造函數初始化，並使用成員方法來操作數據。
			- **`this` 指標**：用於指向當前對象，解決方法名稱衝突，並在內部方法中訪問成員數據。
	- ## 枚舉（enum、std::variant）
	  collapsed:: true
		- ### std::variant
		  collapsed:: true
			- 定義：可以擁有含有各類型別的型別，可以想為型別安全版的 union。
			  collapsed:: true
				- `std::variant<int, double, string>`
			- ```cpp
			  ```
		- ### enum
		  collapsed:: true
			- 以型別安全的方式，告訴你有哪些種類。
			- ```cpp
			  enum Tetrominos { T, I, J, L, Z, S, O };
			  
			  std::string get_str() {
			    	// 利用 `::` 來存取欄位(field)
			    	auto block = Tetrominos::T;
			      switch (block) {
			          // 可利用 using 來縮短名稱
			          using B = Tetrominos;
			          case B::T: return "T Block!";
			          case B::I: return "I Block!";
			          case B::J: return "J Block!";
			          case B::L: return "L Block!";
			          case B::Z: return "Z Block!";
			          case B::S: return "S Block!";
			          case B::O: return "B Block!";
			      }
			  }
			  ```
		- ###  與 struct 一起用的方式
		  collapsed:: true
			- 看不懂沒有關係，對於小型專案而言，可以先不必那麼在乎型別安全，等未來大點的專案在做考慮。
			- ```cpp
			  // Utility to allow overloading lambdas for use in std::visit
			  // 請忽略這些 template 的東西
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
	  collapsed:: true
		- ### 定義
		  collapsed:: true
			- 只讀的連續的一塊記憶體。
			- 不會重新複製資料，可以想成是對原本的資料的參考而已。
		- ### 優勢及適用時機
		  collapsed:: true
			- 適用時機：函式參數。
			- #### 優勢
			  collapsed:: true
				- 能使使用者傳入各式資料型態。
				- 對於創造 subspan 而言極為輕鬆且有效率，不必宣告多餘的空間（與 `std::vector<int> subvec(vec.begin() + 2, 5)`相異）
				- 不必利用雙指標（亦或者雙迭代器）達成。
		- ### 用法
		  collapsed:: true
			- ```cpp
			  void printSpan(std::span<int> span) {
			      for (const auto& elem : span) {
			          std::cout << elem << " ";
			      }
			      std::cout << "\n";
			  }
			  int main() {
			      std::vector<int> vec = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
			      std::cout << "Vector span: ";
			      printSpan(vec);
			     
			    	// 創建一個自 vec 的 subspan (索引 2, 長度 5), 不會重新複製陣列
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