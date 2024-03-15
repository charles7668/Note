# 執行 Docker(On Windows) exec 時出現找不到路徑

參考 : [Docker exec in docker windows - Stack Overflow](https://stackoverflow.com/questions/47891256/docker-exec-in-docker-windows)

可在執行的路徑上多加一個斜線  
origin:  
`docker exec -it [containerid] /bin/sh`  
solution:  
`docker exec -it [containerid] //bin/sh`
