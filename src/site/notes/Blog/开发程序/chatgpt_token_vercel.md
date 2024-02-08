---
tags: [Blog/vercel]
alias: 使用 vercel serverless 部署 chatgpt 认证接口
title: 使用 vercel serverless 部署 chatgpt 认证接口
date: 2023-05-28T13:40:53+08:00
lastmod: 2023-05-28T13:40:59+08:00
dg-publish: true
dg-pinned: false
dg-hide: false
dg-hide-in-graph: false
---

# 仓库地址 

[chatgpt_token_vercel](https://github.com/ayuayue/chatgpt_token_vercel)

功能：

1. 通过登录跳转地址，获取到 code
2. 通过 code，获取到 access_token | refresh_token
3. 使用 refresh_token 刷新 access_token 的过期时间
4. 撤销 refresh_token, 使 refresh_token 失效

详细说明可以根据网页指引操作。

# 部署

如果担心账号数据问题，可以部署到自己的 vercel 上，不用担心数据泄露问题。

所有功能基于 github codespace + vercel serverless function + go 开发。