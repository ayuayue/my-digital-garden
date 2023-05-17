---
{"dg-publish":true,"permalink":"/quartz/content/notes/git/git-submodule/","title":"Git Submodule"}
---


# Git 子模块

## 添加子模块

git submodule add <子项目 Git 仓库 URL> <子模块存放路径>

## 拉取子模块

git submodule update --init --recursive

## 更新子模块

cd submodules/subproject
git pull

## 推送子模块

git add submodules/subproject
git commit -m "Update subproject"
git push

## 删除子模块

git add submodules/subproject
git commit -m "Update subproject"
git push
