# Yarn install command error No such file or directory: 'install'

使用 apt install 安裝 yarn 後出現這個錯誤
解決方法是先移除後改用 npm 來安裝 yarn

```bash
sudo apt remove cmdtest
sudo apt remove yarn
sudo npm install -g yarn
```

## 參考

- [ubuntu - Yarn install command error No such file or directory: 'install' - Stack Overflow](https://stackoverflow.com/questions/46013544/yarn-install-command-error-no-such-file-or-directory-install)
