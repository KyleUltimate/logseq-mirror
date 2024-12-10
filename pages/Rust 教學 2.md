# 複習
	- 可變借用
	  https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&gist=0e7c75c0852c149880204eabe30ffdda
	- Slicing 練習
	  https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&gist=436fd14e997c4f22285073f79a116749
	- 合法借用練習
	  https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&gist=509d395397ca3d70e70d04d74b30ad23
- # 方法(method)
	- 定義：能存取**結構體**的資料的函式
	- ```rust
	  enum Gender {
	   	Boy,
	    	Girl,
	    	Unspeficied
	  }
	  
	  struct Person {
	    	age: u8,
	    	name: String,
	    	gender: Gender,
	  }
	  
	  fn print_person(person: &Person) {
	    	println!("age: {}", person.age);
	    	println!("name: {}", person.name);
	    	let gender_display = match person.gender {
	        	Gender::Boy => "boy",
	        	Gender::Girl => "girl"
	        	Gender::Unspeficied => "prefers not to say", 
	    	};
	    	println!("gender: {}", gender_display);
	  }
	  
	  fn main() {
	    	let person = Person {
	        	age: 32,
	        	name: String::from("Kyle"),
	        	gender: Gender::Boy
	    	};
	    	print_person(&person);
	  }
	  ```
	- 利用方法，可以將 `print_person` 「寫在」 `Person` 結構體裡面
		- ```rust
		  enum Gender {
		   	Boy,
		    	Girl,
		    	Unspeficied
		  }
		  
		  struct Person {
		    	age: u8,
		    	name: String,
		    	gender: Gender,
		  }
		  
		  impl Person {
		    	fn print(&self) {
		          println!("age: {}", self.age);
		          println!("name: {}", self.name);
		          let gender_display = match self.gender {
		              Gender::Boy => "boy",
		              Gender::Girl => "girl"
		              Gender::Unspeficied => "prefers not to say", 
		          };
		          println!("gender: {}", gender_display);
		    	}
		  }
		  
		  fn main() {
		    	let person = Person {
		        	age: 32,
		        	name: String::from("Kyle"),
		        	gender: Gender::Boy
		    	};
		    	person.print();
		  }
		  ```
	- 語法如下
		- `&self == &[結構體名稱]`
		  `&mut self == &mut [結構體名稱]`
		  `self == 結構體名稱`
		- ```rust
		  impl [結構體名稱] {
		  	fn [函式名稱]([&self, &mut self, self]) {
		        
		    	}
		  }
		  
		  // 使用方式
		  let var = [結構體名稱] {};
		  var.[函式名稱]();
		  ```
	- 當宣告時，沒有使用到 (`self`) 則稱為關聯函數，使用 `[結構體名稱]::[函式名稱]()`
		- ```rust
		  struct Circle {
		    	radius: f32,
		  }
		  
		  impl Circle {
		    	fn new() -> Circle {
		        	Circle {
		          	radius: 1.0 
		        	}
		    	}
		  }
		  
		  fn main() {
		    	let circle = Circle::new();
		  }
		  ```
- # 特徵與泛型(traits and generics)
	- ## 泛型
		- 定義：使得以函數接受**多種**型別。
		- ((6756de66-b4b6-40c3-994b-48d4f8efc2c8))
	- ## 特徵
		- 定義：說明結構體具有**哪些函數**，但實現留給結構體。
		- ((6756de66-e1e7-4c7e-aedc-db35dcdee79b))
- # `Result<T,E>`
	- `Result<T,E>`：簡化定義如下
		- ```rust
		  struct Result<T,E> {
		    	Ok(T),
		    	Err(E)
		  }
		  ```
		- `Ok(T)` 代表的是成功運行的值
		- `Err(E)` 代表的是失敗的話，他的錯誤訊息
	- ```rust
	  ```
- [[迭代器]]
- # 習題練習
	- ((67336fdf-8b40-4cdb-9338-bae17b0b63f3)) 練習
		- ```rust
		  #[derive(PartialEq)]
		  enum Message {
		      Quit,
		      Move { x: i32, y: i32 },
		      Write(String),
		      ChangeColor(i32, i32, i32),
		  }
		  
		  fn main() {
		      let msgs = [
		          Message::Quit,
		          Message::Move { x: 1, y: 3 },
		          Message::ChangeColor(255,255,0)
		      ];
		  
		      for msg in msgs {
		          show_message(msg)
		      }
		  } 
		  
		  fn show_message(msg: Message) {
		      match msg {
		          __ => { // 匹配到 `Message::Move`
		              assert_eq!(a, 1);
		              assert_eq!(b, 3);
		          },
		          Message::ChangeColor(r, g, b) => {
		            	assert_eq!(r, __)
		              assert_eq!(g, __);
		              assert_eq!(b, __);
		          }
		          x => assert_eq!(x, Message::Quit),
		      }
		  }
		  ```