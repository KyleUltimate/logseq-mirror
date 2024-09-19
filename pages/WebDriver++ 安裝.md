# 安裝所需前製函式庫
	- 在 Powershell 執行以下命令
		- ```bash
		  git clone --recurse-submodules https://github.com/GermanAizek/webdriverxx.git
		  cd webdriverxx
		  
		  vcpkg install picojson
		  scoop install curl
		  scoop bucket add java
		  scoop install openjdk
		  scoop install selenium
		  scool install chromedriver
		  
		  mkdir build
		  cd build
		  cmake ../src
		  ```
- # 執行 ChromeDriver
  id:: 66ec0852-de5d-48de-a3fe-7b679e3ec7fc
	- #+BEGIN_IMPORTANT
	  在執行任何爬蟲之前，此步驟**非常重要**
	  這串命令得使你 C++ 內部的程式碼能連結到實際的網頁瀏覽器
	  #+END_IMPORTANT
	- `java -jar selenium.jar standalone`