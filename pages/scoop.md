- Windows 環境的命令列套件管理工具
- # **Scoop**: Windows 的套件管理工具
	- Scoop 是一個命令列工具，讓你在 Windows 上輕鬆安裝和管理應用程式。
	- 它簡化了安裝過程，自動處理下載、解壓縮和設定環境變數等繁瑣步驟。
- # 安裝
	- ### 使用 PowerShell (管理員權限)：
	  ```powershell
	  Set-ExecutionPolicy RemoteSigned -scope CurrentUser # 允許執行腳本
	  irm get.scoop.sh | iex
	  ```
- # 簡易範例
	- 詳細功能請洽 https://scoop.sh/
	- ### 安裝 7-Zip：
	  ```powershell
	  scoop install 7zip
	  ```
	- ### 搜尋 Firefox：
	  ```powershell
	  scoop search firefox
	  ```
	- ### 更新所有已安裝的應用程式：
	  ```powershell
	  scoop update
	  ```
	- ### 移除 Notepad++：
	  ```powershell
	  scoop uninstall notepadplusplus
	  ```
	- ### 新增額外的應用程式來源 (Bucket)：
	  ```powershell
	  scoop bucket add extras
	  ```
	- ### 從 `extras` Bucket 安裝 Git：
	  ```powershell
	  scoop install extras/git
	  ```