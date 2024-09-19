# 何謂爬蟲
	- 爬蟲最簡單的概念即為 - 將網路上的資訊給 **爬** 下來。
	- 而
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
		- ### 在 `CMakelists.txt` 中增加下列行數
			- ```cmake  
			  find_package(webdriverxx CONFIG REQUIRED)
			  find_package(cpr CONFIG REQUIRED)
			  
			  target_link_libraries(HelloWorld PRIVATE webdriverxx)
			  target_link_libraries(HelloWorld PRIVATE cpr)
			  ```