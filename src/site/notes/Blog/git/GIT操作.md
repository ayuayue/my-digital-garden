---
{"dg-publish":true,"permalink":"/Blog/git/GIT操作/","title":"GIT 操作","tags":["IT/Git"],"noteIcon":""}
---

# GIT 操作

### 删除未被追踪的文件 `Untracked files`

```SQL
git clean -nf # 删除文件,列出要删除的文件,去掉 n 为删除
git clean -nfd # 删除文件及目录, -n 列出,删除去掉n
```

### 回退到上一次提交

```SQL
git reset --hard HEAD^
```

### 暂存修改

```SQL
git stash
git stash list # 列出暂存记录
git stash apply stash@{1} # 应用暂存
git stash clear # 清空暂存：

```

### 将加入版本控制某个文件添加进 .ignore 中

```Bash
git rm --cached file or folder # 去除之前提交的,使 .ignore 文件生效
git commit -am 'add ignore file'
git push

```

## vscode 拉取失败

报错：vscode would clobber existing tag
解决：
```bash
git fetch --tags -f
```

## git 服务器切换分支后拉取冲突

用远程的分支覆盖本地
```bash
git fetch --all
git reset --hard origin/master
```

## 手机端报错

error: object file ... is empty
```bash
find .git/objects -type f -empty | xargs rm
git fetch -p
```

## 虚拟机与 windows 本地状态不同

使用 git status 查看两个系统返回的信息不同，是由于文件结束符，换行符不一致导致的。在 linux 虚拟机中执行
```bash
git config --global core.autocrlf true 
```
即可保持一致

## 将 github 仓库改为 gitee
首先到 gitee 导入 github 的仓库
```bash
git remote -v
git remote rm origin 
git remote add origin git@gitee.com:caoayu/my-docker.git
git branch --set-upstream-to=origin/main main # 分支名
```
然后把公钥添加进 gitee。
把 https 链接改为 git，设置公钥后不再需要设置密码，进入项目的 .git/config。把 url 改成 git 的链接。

## git pull fatal: Not possible to fast-forward, aborting

合并代码的方式有很多中：git merge,git rebase,git pull 等
git 在处理文件 merge 时，会分成三种处理方式
- –ff–only fast forward 模式，快速合并 有冲突就会失败
- –no–ff 非快速合并 会生成一次 commit
- –squash 将合并后的不同分支所有的提交记录作为一次提交
fase-forward 只要存在冲突就会失败， 我们得配置 git pull
```
git config pull.rebase false —- 关闭 rebase
git config pull.rebase true —–开启rebase
git config pull.ff only/false —–开启/关闭 fast-forward
```
其实我们要做的是关闭 rebase 和 fast-forward 在 pull 中的表现，可运行如下代码解决当前分支问题：
```
git config pull.rebase false
git config pull.ff false
```
可运行如下代码解决全局问题：
```
git config --global pull.rebase false
git config --global --add pull.ff false
```

## 回到远程仓库的状态

```
git fetch --all && git reset --hard origin/master
```

## 重设第一个 commit

也就是把所有的改动都重新放回工作区，并**清空所有的 commit**，这样就可以重新提交第一个 commit 了

```
git update-ref -d HEAD
```

## 查看冲突文件列表

展示工作区的冲突文件列表

```
git diff --name-only --diff-filter=U
```

## 展示工作区和暂存区的不同

输出**工作区**和**暂存区**的 different (不同)。

```
git diff
```

还可以展示本地仓库中任意两个 commit 之间的文件变动：

```
git diff <commit-id> <commit-id>
```

## 展示暂存区和最近版本的不同

输出**暂存区**和本地最近的版本 (commit) 的 different (不同)。

```
git diff --cached
```

## 展示暂存区、工作区和最近版本的不同

输出**工作区**、**暂存区** 和本地最近的版本 (commit) 的 different (不同)。

```
git diff HEAD
```

## 快速切换到上一个分支

```
git checkout -
```

## 删除已经合并到 master 的分支

```
git branch --merged master | grep -v '^\*\| master' | xargs -n 1 git branch -d
```

## 展示本地分支关联远程仓库的情况

```
git branch -vv
```

## 关联远程分支

关联之后，git branch -vv 就可以展示关联的远程分支名了，同时推送到远程仓库直接：git push，不需要指定远程仓库了。

```
git branch -u origin/mybranch
```
或者在 push 时加上 -u 参数

```
git push origin/mybranch -u
```
## 查看远程分支和本地分支的对应关系

```
git remote show origin
```
## 远程删除了分支本地也想删除

```
git remote prune origin
```
## 从远程分支中创建并切换到本地分支

```
git checkout -b <branch-name> origin/<branch-name>
```
## 删除本地分支

```
git branch -d <local-branchname>
```
## 删除远程分支

```
git push origin --delete <remote-branchname>
# or
git push origin :<remote-branchname>
```
## 重命名本地分支

```
git branch -m <new-branch-name>
```
## 修改作者名

```
git commit --amend --author='Author Name <email@address.com>'
```
## 展示所有忽略的文件

```
git ls-files --others -i --exclude-standard
```
## 强制删除 untracked 的文件
可以用来删除新建的文件。如果不指定文件文件名，则清空所有工作的 untracked 文件。clean 命令，**注意两点**：

1. clean 后，删除的文件无法找回
2. 不会影响 tracked 的文件的改动，只会删除 untracked 的文件

```
git clean <file-name> -f
```
## 强制删除 untracked 的目录

可以用来删除新建的目录，**注意**:这个命令也可以用来删除 untracked 的文件。详情见上一条

```
git clean <directory-name> -df
```
## 清除 gitignore 文件中记录的文件

```
git clean -X -f
```

# git error: error authenticating: unable to connect to agent pipe; class=Ssh (23)

到系统服务中，开启 `OpenSSH Authentication Agent`，`OpenSSH SSH Server` 并设置为自动。
## bad credentials

```powershell
ssh-add C:\Users\caoayu\.ssh\id_rsa

```

## git-sim

```bash
pip3 install git-sim

```

## git config --global --add safe.directory

```
git config --global --add safe.directory '*'
```

# lazygit

## cherry-pick 从其他分支的某个提交记录合并到当前分支上。

选中其他分支，enter 进入提交日志，按 c 选择需要挑选的提交。然后进入按 4 提交 reflog 页面，按 v 键粘贴提交。

# 使用代理 tun 模式时，无法 git 远程操作。

可能是屏蔽了 22 端口，改为443端口。

```conf
# ~/.ssh/config

Host github.com
	Hostname ssh.github.com
	Port 443
	User git

```

## 删除远程标签及本地标签


```
git push origin :refs/tags/v1.0.9.0403
git tag -d v1.0.9.0403
```


## 将本地tag推送到远程

```
git push origin --tags
```

## 把标签修改为当前分支最新的提交，并替换远程分支


```
git tag -d 1.0.9
git tag -d v1.0.9.0403
git push origin :refs/tags/v1.0.9.0403
git push origin :refs/tags/1.0.9
git tag -f v1.0.9
git push -f origin v1.0.9

```
