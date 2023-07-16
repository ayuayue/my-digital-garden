---
{"dg-publish":true,"permalink":"/Blog/git/git-submodule/","title":"Git Submodule","noteIcon":"1","created":"2023-05-07T16:54:12+08:00","updated":""}
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

git submodule deinit -f <submodule_path>
git rm <submodule_path>
git config -f .gitmodules --remove-section submodule.<submodule_path>
git commit -m "Remove submodule <submodule_path>"
rm -rf <submodule_path>

[[Blog/git/GIT操作\|GIT操作]]