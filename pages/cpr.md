# **C++ R**equests: Curl for People
- 是一個簡易的 library 來使你能 **下載檔案**
- # 安裝
	- ### 在專案資料夾裡運行
		- ```bash
		  vcpkg install picojson
		  scoop install curl
		  scoop bucket add java
		  scoop install openjdk
		  ```
-
- # 簡易範例
	- 詳細功能請洽 https://docs.libcpr.org/
	- ```cpp 
	  #include <cpr/cpr.h>
	  
	  int main(int argc, char** argv) {
	      cpr::Response r = cpr::Get(cpr::Url{"https://api.github.com/repos/whoshuu/cpr/contributors"},
	                        cpr::Authentication{"user", "pass", cpr::AuthMode::BASIC},
	                        cpr::Parameters{{"anon", "true"}, {"key", "value"}});
	      r.status_code;                  // 200
	      r.header["content-type"];       // application/json; charset=utf-8
	      r.text;                         // JSON text string
	      return 0;
	  }
	  ```