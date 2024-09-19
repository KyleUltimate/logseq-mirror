- https://github.com/GermanAizek/webdriverxx
- # 安裝所需前製函式庫
	- 在 Powershell 執行以下命令
		- ```pwsh
		  git clone --recurse-submodules https://github.com/GermanAizek/webdriverxx.git
		  cd webdriverxx
		  
		  vcpkg install picojson
		  scoop install curl
		  scoop bucket add java
		  scoop install openjdk
		  scoop install selenium
		  
		  mkdir build
		  cd build
		  cmake ../src
		  ```
- # 執行 ChromeDriver
	- `java -jar selenium.jar standalone`