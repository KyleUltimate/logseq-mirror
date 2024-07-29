# 俄羅斯方塊（C++）
- # C++ 語法補充
	- ## 結構體(struct)
		- ### Constructor(member initializer list)
	- ## 枚舉（ enum class、std::variant）
		- enum -> 型別安全的方法來告訴你有哪些種類
		- std::variant -> 型別
		- std::holds_alternative 用來確認 std::variant 目前所含的型別
		  ```c++
		  struct OccupiedBlockStatus {
		      enum StatusType { Falling, Finished };
		      std::variant<BlockMode, Color> data;
		      StatusType type;
		  
		      OccupiedBlockStatus(BlockMode mode)
		          : data(mode), type(Falling) {}
		      OccupiedBlockStatus(Color color)
		          : data(color), type(Finished) {}
		  
		      const bool is_falling() const {
		          return type == Falling;
		      }
		  
		      const bool is_finished() const {
		          return type == Finished;
		      }
		  
		      auto get_color() const -> Color {
		          if (type == Finished) {
		              return std::get<Color>(data);
		          }
		          if (std::holds_alternative<T>(data)) return {0.5f, 0.0f, 0.5f, 1.0f}; // Purple for T
		          if (std::holds_alternative<I>(data)) return {0.0f, 1.0f, 1.0f, 1.0f}; // Cyan for I
		          if (std::holds_alternative<J>(data)) return {0.0f, 0.0f, 1.0f, 1.0f}; // Blue for J
		          if (std::holds_alternative<L>(data)) return {1.0f, 0.65f, 0.0f, 1.0f}; // Orange for L
		          if (std::holds_alternative<Z>(data)) return {1.0f, 0.0f, 0.0f, 1.0f}; // Red for Z
		          if (std::holds_alternative<S>(data)) return {0.0f, 1.0f, 0.0f, 1.0f}; // Green for S
		          if (std::holds_alternative<O>(data)) return {1.0f, 1.0f, 0.0f, 1.0f}; // Yellow for O
		          return {0.0f, 0.0f, 0.0f, 1.0f}; // Default color
		      }
		  };
		  ```
	- ## std::span
- # 俄羅斯方塊術語與規則介紹
	- ## ARR
	- ## DAS
	- ## 旋轉機制
- # 難點攻關
- ## 1. 旋轉如何實施？
- 直接把旋轉完的方塊 array 寫在程式碼中
- 根據每個不同的方塊，撰寫獨立的旋轉軸(pivot)