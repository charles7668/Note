# 目錄

- [目錄](#目錄)
- [建立只有本地可使用的 igonre](#建立只有本地可使用的-igonre)
  - [1. 將路徑加到 .git/info/exclude](#1-將路徑加到-gitinfoexclude)
- [參考](#參考)

# 建立只有本地可使用的 igonre

通常情況下會把不需提交的檔案路徑寫到 `.gitignore` , 但有時這個檔案可能是本地建立的測試檔案, 但不一定需要被專案給忽略, 這時 `.gitignore` 就比較不適合了, 下面是可以達到此目的的方法

## 1. 將路徑加到 .git/info/exclude

將檔案加到 `.git/info/exclude` 中後,這些檔案就會被 git 給忽略 , 不過只作用於本地

# 參考

- [version control - How do you make Git ignore files without using .gitignore? - Stack Overflow](https://stackoverflow.com/questions/653454/how-do-you-make-git-ignore-files-without-using-gitignore)
- [Git - gitignore Documentation](https://git-scm.com/docs/gitignore)
