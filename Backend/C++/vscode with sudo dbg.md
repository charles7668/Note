# Debug C++ Program with sudo gdb

## 1. Create the Script

Create a shell script file. Replace `your-password` with your actual password.

```shell
#!/bin/sh
password="your-password"
echo $password
if [ $password = "your-password" ]; then
    echo "Please set your password in the script"
    exit 1
fi
echo $password | sudo -S echo "" > /dev/null
sudo /usr/bin/gdb "$@"
```

## 2. Use the Script in `.vscode/launch.json`

Add or replace the following configuration to `.vscode/launch.json`

```json
"miDebuggerPath": "your-script-path"
```
