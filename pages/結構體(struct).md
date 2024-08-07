### 定義
	- 將相關的欄位與資訊**組織**在一起，並且每個結構體都有對其資料運用的**成員方法**（method）。
	- 你可以把他想像為一個**設計藍圖**，設計者可以利用這個藍圖來去建立物件，換句話說 struct 是一種使用者定義的**型態**。
	- 資料可以是其他結構體、型別。
- # 如何宣告及使用
	- ## `this`  指標
		- 在結構體內，若需要使用對指到自己的指標，則可利用 `this` 指標，可以把她想成 `self`，指向**自己**的指標
		- 另外，對於解決結構體內與結構體外的方法重名問題，`this` 指標也是非常重要的
		- 利用 `operator->` 來得到內部方法及資料欄位，而非普通的 `operator.`
	- ## 宣告方法
		- ### Member List-initialization
		- ### Aggregate Initialization + Designated Initializer
		- ### 建構子
			- 目的：若需對使用者傳入的參數進行前製作業，則需利用建構子
			- 定義：是一種特殊的成員方法，用於初始化類別或結構體的實例。它的名稱與類別名相同，沒有返回類型。
			- ```cpp
			  #include <iostream>
			  
			  struct ScientificNumber {
			    	// 在一開始定義結構體要含有什麼資料
			    	// convention 會將資料加個 `m_` prefix ，減少可能的重名機會
			    	double m_fraction;
			    	int m_exponent;
			    	bool m_sign;
			    
			    	// 此為 「建構子」，宣告方式即為 `Struct(args) {}`
			    	// 利用 `this` 指標設定結構體
			    	// **注意**: 這裡的 `this` 指標是指到尚未創建的結構體，要小心使用
			    	ScientificNumber(double number) {
			        	int exponent = std::ceil(log10(number));
			          double fraction = number/(pow(10,exponent));
			          this->m_fraction = fraction;
			        	this->m_exponent = exponent;
			        	this->m_sign = number > 0;
			      }
			  };
			  int main() {
			    	// 利用大括弧（`{}`）來利用建構子
			    	ScientificNumber num = ScientificNumber { 8202.87332 };
			  }
			  ```
	- ## 成員方法
		- 目的：利用結構體的資料，進行特殊
		- ```cpp
		  #include <iostream>
		  
		  struct ScientificNumber {
		    	double m_fraction;
		    	int m_exponent;
		    	bool m_sign;
		  
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
		    	ScientificNumber num = ScientificNumber { 0.8772, 82 };
		    	// 對於得到的結構體，可利用 `operator.` 來執行其方法，或得到其欄位
		    	std::cout << num.m_sign << " " << num.value() <<  "\n";
		     	auto num_ref = &num;
		    	// 對於得到指向結構體的指針，可利用 `operator->` 來執行其方法
		    	std::cout << num_ref->value();
		  }
		  ```
	- ```cpp
	  #include <iostream>
	  
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
	    	ScientificNumber num = ScientificNumber { 0.8772, 82 };
	    	// 對於得到的結構體，可利用 `operator.` 來執行其方法，或得到其欄位
	    	std::cout << num.m_sign << " " << num.value() <<  "\n";
	     	auto num_ref = &num;
	    	// 對於得到指向結構體的指針，可利用 `operator->` 來執行其方法
	    	std::cout << num_ref->value();
	  }
	  ```