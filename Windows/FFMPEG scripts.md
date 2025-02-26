# ffmpeg scripts

## Covert all `ts` video file in folder to `mp4`

```bash
@echo off
setlocal enabledelayedexpansion

REM 迴圈處理所有TS文件
for %%f in (*.ts) do (
    REM 獲取文件名（不含副檔名）
    set "filename=%%~nf"
    REM 將TS轉換為MP4
    ffmpeg -i "%%f" -c:v copy -c:a aac "!filename!.mp4"
)

echo 所有TS文件已轉換完成。
pause

```
