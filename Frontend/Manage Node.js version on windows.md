# 在 windows 中管理使用的 node.js 版本

主要使用 [nvm-windwos](https://github.com/coreybutler/nvm-windows) 來進行管理 , 這裡我選擇使用 [scoop](https://scoop.sh/) 來進行安裝

# 使用 Scoop 安裝 nvm-windwows

使用命令行工具執行以下指令

```bash
scoop bucket add main
scoop install main/nvm
```

# 確認安裝是否成功

安裝完後可使用 `nvm -v` 確認是否安裝完成, 如果正確安裝, 會顯示版本號

# 查看可用命令

之後可使用 `nvm help` 來查看可用命令或到 [nvm-windwos](https://github.com/coreybutler/nvm-windows) 來看可以使用哪些命令

# 基本操作

最基本的使用方式如下

1. `nvm install {version}` 替換 version 來安裝對應版本的 node.js
2. `nvm use {version}` 選擇使用的 node.js 版本
