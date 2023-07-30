---
{"dg-publish":true,"permalink":"/Blog/开发程序/java/idea-config/","title":"IDEA 配置","noteIcon":"1","created":"2023-05-28T13:40:53+08:00","updated":""}
---


# 配置

开启自动构建及编译

![](https://s3.caoayu.eu.org/2023/07/31/202307310016059.png)

Jrebel 配置自动热加载，首先注册安装 Jrebel，并激活。

![](https://s3.caoayu.eu.org/2023/07/31/202307310059325.png)

![](https://s3.caoayu.eu.org/2023/07/31/202307310100994.png)

启动后，会有一个刷新的按钮，点击后不需要重新运行就可以看到更新代码后的更改。

![](https://s3.caoayu.eu.org/2023/07/31/202307310101467.png)


文件编码

![](https://s3.caoayu.eu.org/2023/07/31/202307310015548.png)

菜单栏增加按钮，新 UI 可能有些按钮跟旧 UI 不一致，如果需要显示可以自己自定义添加。如增加一个显示 git stash 的按钮。

![](https://s3.caoayu.eu.org/2023/07/31/202307310021795.png)


# 插件

1. GitToolBox： 显示 git 上次提交信息
2. Gitfox： git commit 提交规范、开源协议生成
3. JavaBean to Json：java bean 转成 json 
4. maven-search：maven 仓库搜索并生成依赖
5. MybatisX：与 MybatisCodeHelperPro 冲突
6. MybatisCodeHelperPro
7. String Mainpulation：各自变量命名风格
8. RestfulToolKit-fix：自动生成 springboot 访问路由地址并可以模拟请求，类似 apifox
9. jrebel：热加载工具，可以注册免费试用 14 天，可以一直换临时邮箱注册
