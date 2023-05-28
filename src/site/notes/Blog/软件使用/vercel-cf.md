---
{"dg-publish":true,"permalink":"/Blog/软件使用/vercel-cf/","title":"使用 vercel + cloudflare 管理域名","noteIcon":"1"}
---


## 首先注册 vercel 跟 cloudflare

[Cloudflare | Web Performance & Security](https://dash.cloudflare.com/)

[https://vercel.com/login?next=%2Fdashboard](https://vercel.com/dashboard)

## 添加域名到 cloudflare 

需要按照说明，把域名服务器的 dns 设置成 cloudflare 的服务器。如：

对于使用腾讯云购买的域名，转到：[登录 - 腾讯云](https://console.cloud.tencent.com/domain/all-domain) 进行修改域名服务器

![../../Attachment/vercel-cf-20230527121939226.png](/img/user/Attachment/vercel-cf-20230527121939226.png)

## cloudflare 配置 ssl

如果以前是用 vercel 进行解析配置域名的，那么在添加完 cf 后会自动把所有的解析记录给添加进来，但是可能会有的域名访问提示**重定向次数过多**，响应码是：308。需要在 ssl 配置中更改为完全或严格模式。

![../../Attachment/vercel-cf-20230527122248067.png](/img/user/Attachment/vercel-cf-20230527122248067.png)

之后就可以直接在这里添加 dns 域名解析记录了。
# vercel 项目配置域名

vercel 支持在部署后自定义自己的域名解析，如下：

![../../Attachment/vercel-cf-20230527122445920.png](/img/user/Attachment/vercel-cf-20230527122445920.png)


只需要在 cf 中添加两条 dns 解析记录即可，如果是从 vercel 转过去的则不需要手动添加默认会复制过来。其中一个即可，有一个是国内访问加速的，但是使用了 cf 后理论上也会有加速。


```
76.76.21.93
76.76.21.123
```


![../../Attachment/vercel-cf-20230527122644737.png](/img/user/Attachment/vercel-cf-20230527122644737.png)

