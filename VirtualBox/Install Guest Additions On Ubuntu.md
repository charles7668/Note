# 在 Ubuntu 系統上安裝 Guest Addions

1. 選單中選取 `裝置`->`插入 Guest Additions CD映像`
2. 打開 `terminal` 並輸入以下命令
   ```shell
   sudo apt update
   sudo apt install build-essential dkms linux-headers-generic
   ```
3. 輪入以下命令進行安裝
   ```shell
   sudo rcvboxadd setup
   ```
