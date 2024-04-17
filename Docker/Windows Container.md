# Windows Container 記錄

## 執行 Docker cp 進行檔案時出現錯誤

先停止容器後再進行複製即可

```cmd
docker stop <container-name>
docker cp <src-path> <container-name>:<dest-path>
```
