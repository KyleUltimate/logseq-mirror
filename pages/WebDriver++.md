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
		  
		  mkdir build
		  cd build
		  cmake ../src
		  
		  wget https://selenium-release.storage.googleapis.com/4.0-beta-4/selenium-server-4.0.0-beta-4.jar
		  ```
- # 執行 ChromeDriver