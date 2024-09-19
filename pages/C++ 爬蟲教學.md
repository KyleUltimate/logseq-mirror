# 何謂爬蟲
-
- # C++ 爬蟲環境設置
	- ## 爬蟲所需函式庫
		- ##  [[C++ 安裝教學]]
			- 將 C++ 專案之基礎設置搞好
		- ## [[WebDriver++ 安裝]]
			- 為爬蟲所需函式庫。
		- ## [[cpr 安裝]]
			- ((66ec06bc-d677-43d3-a42d-44d5fe20dbb4))
	- ## 將函式庫 include 到你的專案中
		- ### 在 `Cmakelists.txt` 中增加下列行數
			- ```cmake  
			  find_package( CONFIG REQUIRED)
			  
			  target_link_libraries(HelloWorld PRIVATE raylib)
			  ```