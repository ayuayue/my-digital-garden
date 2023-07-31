---
{"dg-publish":true,"permalink":"/Blog/软件使用/server-update/","title":"服务升级优化","noteIcon":"1","created":"2023-05-28T13:40:53+08:00","updated":""}
---


# 关于服务

![](https://s3.caoayu.eu.org/2023/05/29/20230529001507.png)

在之前的时间里，大部分应用都是通过服务器部署，有一小部分静态页面前端项目是使用 vercel 部署的。经过两天的折腾，终于把所有的服务基本都迁移到免费的第三方，实现白嫖到底的原则。

由于是在腾讯云购买的域名，所以之前都是用的 dnspods 解析域名的，自从使用了 vercel 后，就把域名的 dns 解析服务器换成了 vercel 的，今天更彻底，直接换成了 cloudflare ，主要是有免费的流量分析、cdn 加速、ddos 拦截等功能，实在是太香了。

而对于一些简单的服务，都使用 vercel 的 serverless function 进行部署，并且在 vercel 配置了  cloudflare 的 dns servername 后，直接使用 vercel 配置的域名解析记录，也是可以直接生效的，具体的迁移步骤可以查看 [[Blog/软件使用/vercel-cf\|vercel-cf]] 这篇文章。

而 serveless function 支持 nodejs，php，go，python 环境，已经基本可以满足我日常的使用了，除非一些需要 docker 部署的东西才可能用到自己的服务器，但是后期可能也会找一些容器部署的平台来实现。

对于域名，自己又申请了一个 eu.org 的免费域名，配合 cloudflare 可以不用备案就可以解析使用。

关于对象存储，之前可能使用的是 bilibili、github 的免费图床，但是稳定性和访问速度不太好，这次直接上了 cloudflare 的 R 2 服务，有免费的额度，并且超额使用了费用也是非常低的，自己博客用是完全够用的。