# 按鈕控件加入系統管理員的盾牌顯示

主要透過 windows 的 control message 來實現

簡易示例

```c#
Button b = new Button();
const uint BCM_FIRST = 0x1600; //Button Control Message Base
const uint BCM_SETSHIELD = (BCM_FIRST + 0x000C); //BCM_SETSHIELD message

b.FlatStyle = FlatStyle.System; // only system style button can display shield
SendMessage(b.Handle, BCM_SETSHIELD, 0, 0xFFFFFFFF); // send message to button
```

- BCM_FIRST 是 Button Control Message 的起始位置
- BCM_SETSHIELD 消息的 Hex 值是 BCM_FIRST + 0x000C Offset
- SendMessage 是 `user32.dll` 內的 api

關於更多控件訊息的 message 值可參考 [Button Control Messages - Win32 apps | Microsoft Learn](https://learn.microsoft.com/en-us/windows/win32/controls/bumper-button-control-reference-messages)，文檔中並無列出實際的數值，數值部分可在安裝的 Windows SDK 路徑下找到 `CommCtrl.h` 內找到(按照消息名搜尋即可)

# 參考

- [Button Control Messages - Win32 apps | Microsoft Learn](https://learn.microsoft.com/en-us/windows/win32/controls/bumper-button-control-reference-messages)
