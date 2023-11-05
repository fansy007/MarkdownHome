#java #basic
[[Mac开发环境搭建#Setup Git]]

![[Mac开发环境搭建#git account]]
# Git operations
```sh
## 回到过去
git reset --hard HEAD~n

## log latest 6 records
git log --oneline -n 6

## 加入暂存区，从暂存区消除
git add *txt
git rm --cached *txt

## merge冲突解决
正常改文件
git add
git commit

## git rebase 冲突时
正常改文件
git add
git rebase --continue
git commit

## cherry pick 多版本同时cherry pick
git cherry-pick A^..B

## delete branch
git branch -d feature/XXX
```

![[Mac开发环境搭建#push local code remote]]

