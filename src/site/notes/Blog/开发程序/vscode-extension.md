---
{"dg-publish":true,"permalink":"/blog//vscode-extension/","tags":["Blog/vscode"],"noteIcon":"1","created":"2023-05-26T23:29:07+08:00"}
---

# 创建一个自己的 vscode 插件

创建一个普通的 pack 类型的插件，包含了一些其他的插件。比如：

![../../Attachment/vscode-extension-20230526233056954.png](/img/user/Attachment/vscode-extension-20230526233056954.png)

当然还可以创建其他类型的插件，具体的需要查阅 vscode 的 api。

## 首先搭架子

首先创建一个目录，命名如：vscode-php-pack，并进入目录。

执行下面代码

```bash
npm install -g yo generator-code
yo code
```

会在终端提示你关于扩展的所有配置信息，自己手动填写后会生成一个项目，最终会提示你使用 vscode 或者预览版打开。

## 添加扩展

因为只是做一个扩展包，所以只需要修改 package. json 就行了。具体改动如下：


```json

  "extensionPack": [

    "xdebug.php-debug",

    "jaguadoromero.vscode-php-create-class",

    "neilbrayfield.php-docblocker",

    "pwarchol.vscode-php-file-link",

    "phproberto.vscode-php-getters-setters",

    "bmewburn.vscode-intelephense-client",

    "mehedidracula.php-namespace-resolver",

    "st-pham.php-refactor-tool",

    "phiter.phpstorm-snippets",

    "linyang95.php-symbols",

    "onecentlin.phpunit-snippets",

    "recca0120.vscode-phpunit"

  ]

```

注意这里的扩展唯一标识在上面的图中有标注，复制填写即可。

## 打包扩展

使用命令：`vsce package` 打包即可在本地安装。

## 发布扩展

1. 首先需要创建一个 azure 的组织
2. 生成一个 access_token
3. 添加发布者到 package.json
4. 使用 vsce login 登录并发布

具体操作步骤：[Publishing Extensions | Visual Studio Code Extension API](https://code.visualstudio.com/api/working-with-extensions/publishing-extension)

发布成功效果：

![../../Attachment/vscode-extension-20230527002156661.png](/img/user/Attachment/vscode-extension-20230527002156661.png)

![../../Attachment/vscode-extension-20230527002208561.png](/img/user/Attachment/vscode-extension-20230527002208561.png)

![../../Attachment/vscode-extension-20230527002305074.png](/img/user/Attachment/vscode-extension-20230527002305074.png)


# 自己常用的插件

chinese 
Gitlens
Wakatime
Path Intellisense
Emoji Log
Error Lens
Prettier
Code Runner 
WSL 
SFTP
vscode-toggle-case
vscode-common-pack
GitHub Copilot Chat
Native Debug
IntelliCode 
Docker
markdownlint
better-comments
MySQL
dbclient-jdbc
koroFileHeader