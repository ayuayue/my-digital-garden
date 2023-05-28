---
{"dg-publish":true,"permalink":"/Blog/软件使用/github-cli/","title":"Github-CLI使用","noteIcon":""}
---


# GITHUB_CLI

win 使用 scoop install github-CLI 进行安装。

# 功能

可以对仓库、action、pull request、issuse 等进行管理，而不需要打开网页或者 GitHub desktop 软件，方便快捷。

首先需要登录或者授权才可以，可以使用浏览器跳转登录，也可以直接输入生成的 token 进行认证。

1. 登录： gh auth login 
2. 登录后打印 token ：gh auth token
3. 查看所有的仓库：gh repo list
4. 删除仓库：首先需要授权 gh auth refresh -h github.com -s delete_repo ，然后删除 gh repo delete ayuayue/xxx 。
5. 重命名仓库：gh repo rename 
6. 创建仓库：gh repo create 根据指引输入即可。
7. 编辑仓库配置：gh repo edit 使用空格选中设置项，回车确认。