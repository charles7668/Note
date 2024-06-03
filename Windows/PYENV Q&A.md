# PYENV Q&A

## 使用 `scoop` 安裝 `pyenv` 出現錯誤

1. `error installing "core" component MSI`

   - 使用管理員打開 `powershell` 並執行下列命令

     ```shell
     scoop uninstall pyenv
     scoop install pyenv
     pyenv update
     pyenv install {your-python-version}
     ```
