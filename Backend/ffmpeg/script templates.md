# script templates for ffmpeg

## Convert `ts` files in folder to `mp4`

```bat
@echo off
setlocal enabledelayedexpansion

for %%f in (*.ts) do (
    set "filename=%%~nf"
    ffmpeg -i "%%f" -c:v copy -c:a aac "!filename!.mp4"
)

echo complete
pause
```
