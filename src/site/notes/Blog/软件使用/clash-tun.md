---
tags: []
title: Clash Tun Mixed设置
date: 2023-05-28T13:40:53+08:00
lastmod: 2023-05-28T13:40:59+08:00
dg-publish: true
dg-pinned: false
dg-hide: false
dg-hide-in-graph: false
---
# TUN 模式

Clash 的 TUN 模式是一种虚拟网络接口，它可以拦截操作系统的三层流量，从而扩展 Clash 的入口转发能力。TUN 模式可以提高 Clash 处理 UDP 流量的能力，可以劫持任何三层流量，实现 DNS 劫持也是轻而易举，并且它与部分操作系统的网络栈结合也非常好，可以提升利用 iptables 等组件的能力。

对于不遵循系统代理的软件，TUN 模式可以接管其流量并交由 CFW 处理，在 Windows 中，TUN 模式性能比 TAP 模式好。

# 设置


```
dns:
  enable: true
  ipv6: false
  listen: 0.0.0.0:53
  enhanced-mode: redir-host
  fake-ip-range: 198.18.0.1/16
  fake-ip-filter:
    - "*.lan"
    - localhost.ptlogin2.qq.com
  nameserver:
    - 223.5.5.5
    - 180.76.76.76
    - 119.29.29.29
    - 117.50.11.11
    - 117.50.10.10
    - 114.114.114.114
  fallback:
    - 8.8.8.8
    - 1.1.1.1
    - tls://dns.rubyfish.cn:853
    - tls://1.0.0.1:853
    - tls://dns.google:853
    - https://dns.rubyfish.cn/dns-query
    - https://cloudflare-dns.com/dns-query
    - https://dns.google/dns-query
  fallback-filter:
    geoip: true
    ipcidr:
      - 240.0.0.0/4

```
