# 在 VS2022 使用老舊的 .Net Framework

1. 建立一個新專案
2. 使用`nuget`安裝對應版本的`Microsoft.NETFramework.ReferenceAssemblies`，例如要安裝 4.0 版本則是 `Microsoft.NETFramework.ReferenceAssemblies.net40`
3. 在 `C:\Users\{username}\.nuget\packages\Microsoft.NETFramework.ReferenceAssemblies.net40\{version}\build\.NETFramework` 下找到對應版本的資料夾，這裡的情況是 `v4.0`
4. 複製到 `C:\Program Files (x86)\Reference Assemblies\Microsoft\Framework\.NETFramework` 後即可在 `VS2022` 中使用
