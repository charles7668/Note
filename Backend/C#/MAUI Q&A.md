# MAUI 問題記錄

- [MAUI 問題記錄](#maui-問題記錄)
  - [編譯後的 exe 檔無法直接執行](#編譯後的-exe-檔無法直接執行)
    - [參考](#參考)

## 編譯後的 exe 檔無法直接執行

1. 先在 `.csproj` 的 `PropertyGroup` 中加入 `WindowsPackageType` 為 `None`

   ```xml
   <PropertyGroup>
       ...other setting
       <WindowsPackageType>None</WindowsPackageType>
   </PropertyGroup>
   ```

2. 修改 `launchSettings.json` 中的 `commandName` 為 `Project`(原本可能為`MSIX`)

   ```json
   {
     "profiles": {
       "Windows Machine": {
         "commandName": "Project",
         "nativeDebugging": false
       }
     }
   }
   ```

### 參考

- [c# - Easiest way to launch a MAUI app exe on Windows? - Stack Overflow](https://stackoverflow.com/questions/73718305/easiest-way-to-launch-a-maui-app-exe-on-windows)
