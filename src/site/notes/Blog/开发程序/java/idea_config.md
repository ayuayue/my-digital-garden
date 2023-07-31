---
{"dg-publish":true,"permalink":"/Blog/开发程序/java/idea_config/","title":"IDEA 配置","noteIcon":"1","created":"2023-05-28T13:40:53+08:00","updated":""}
---


# 配置

开启自动构建及编译

![_resources/idea-config/384c615ea3fabcbd8f0c93c2e54040f5_MD5.png](/img/user/_resources/idea-config/384c615ea3fabcbd8f0c93c2e54040f5_MD5.png)

Jrebel 配置自动热加载，首先注册安装 Jrebel，并激活。

![_resources/idea-config/37ba5c281461a360e3fd34f7bee737f8_MD5.png](/img/user/_resources/idea-config/37ba5c281461a360e3fd34f7bee737f8_MD5.png)

![_resources/idea-config/aaed0bc69af3a313cd58001a7ea0ff17_MD5.png](/img/user/_resources/idea-config/aaed0bc69af3a313cd58001a7ea0ff17_MD5.png)

启动后，会有一个刷新的按钮，点击后不需要重新运行就可以看到更新代码后的更改。

![_resources/idea-config/0bbd0b3a0b2f4dc4ca9796a4446f60f7_MD5.png](/img/user/_resources/idea-config/0bbd0b3a0b2f4dc4ca9796a4446f60f7_MD5.png)


文件编码

![_resources/idea-config/3ebac20da1ee1edfecfaabd8101a9863_MD5.png](/img/user/_resources/idea-config/3ebac20da1ee1edfecfaabd8101a9863_MD5.png)

菜单栏增加按钮，新 UI 可能有些按钮跟旧 UI 不一致，如果需要显示可以自己自定义添加。如增加一个显示 git stash 的按钮。

![_resources/idea-config/7d57182b1c45741e93816569e21656e3_MD5.png](/img/user/_resources/idea-config/7d57182b1c45741e93816569e21656e3_MD5.png)


# 插件

1. GitToolBox： 显示 git 上次提交信息
2. Gitfox： git commit 提交规范、开源协议生成
3. JavaBean to Json：java bean 转成 json 
4. maven-search：maven 仓库搜索并生成依赖
5. MybatisX：与 MybatisCodeHelperPro 冲突
6. MybatisCodeHelperPro
7. String Mainpulation：各自变量命名风格
8. RestfulTool：自动生成 springboot 访问路由地址并可以模拟请求，类似 apifox
9. jrebel：热加载工具，可以注册免费试用 14 天，可以一直换临时邮箱注册
10. Auto filling Java call arguments：补全参数
