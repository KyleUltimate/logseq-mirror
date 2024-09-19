# 何謂爬蟲
	- 爬蟲最簡單的概念即為 - 將網路上的資訊給 **爬** 下來。
	- 對於如何思考撰寫爬蟲程式，有兩個思路
		- 1. 想成你是**人類使用者**，你會去按哪些按鍵來得取你所想要的資訊。
		- 2. 想成你是**網站設計者**，你會將資訊放在哪些地方。
	- 對於簡易的網站而言，可以將網站的 `.html` 檔**直接下載**下來實作分析。
	- 但對於較複雜的網站而言，html 是 **動態生成** 的，因此需要 **特殊手法** 來將其爬下來。
- # C++ 爬蟲環境設置
	- ##  [[C++ 安裝教學]]
		- 將 C++ 專案之基礎設置搞好
	- ## 爬蟲所需函式庫
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
	- #+BEGIN_IMPORTANT
	  ((66ec0852-de5d-48de-a3fe-7b679e3ec7fc)) 請確認 Chromedriver 有在執行
	  #+END_IMPORTANT