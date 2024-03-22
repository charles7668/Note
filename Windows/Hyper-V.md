# 啟用/禁用 Hyper-V

使用系統管理員開啟`cmd`後在`cmd`中輸入下列命令後重新登入或重新開機

## Disable Hyper-V

```cmd
bcdedit /set hypervisorlaunchtype off
```

## Enable Hyper-V

```cmd
bcdedit /set hypervisorlaunchtype auto
```
