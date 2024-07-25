# Ignore Local File Changes

Sometimes we want certain local files to be ignored when pushing to the server but do not want to add them to `.gitignore`. For this, we need a local ignore rule.

- [Ignore Local File Changes](#ignore-local-file-changes)
  - [1. Use `.git/info/exclude`](#1-use-gitinfoexclude)
  - [2. Use `git update-index --assume-unchanged`](#2-use-git-update-index---assume-unchanged)
  - [Reference](#reference)

## 1. Use `.git/info/exclude`

we can add files to be ignored in `.git/info/exclude`, similar to how you would with `.gitignore`. This way, the files will be ignored during commits.

## 2. Use `git update-index --assume-unchanged`

This command can be used to ignore changes to files during commits. To revert and continue tracking changes, use `git update-index --no-assume-unchanged`.

## Reference

- [version control - How do you make Git ignore files without using .gitignore? - Stack Overflow](https://stackoverflow.com/questions/653454/how-do-you-make-git-ignore-files-without-using-gitignore)
- [Git - gitignore Documentation](https://git-scm.com/docs/gitignore)
- [Git - git-update-index Documentation](https://git-scm.com/docs/git-update-index)
