---
{"dg-publish":true,"permalink":"/Blog/软件使用/clash-subconverter/","title":"Clash订阅转换","noteIcon":""}
---


# Subconverter

[GitHub - tindy2013/subconverter: Utility to convert between various subscription format](https://github.com/tindy2013/subconverter)

我的在线服务地址：http://ssh.caoayu.top:25500/sub?target=&url=&config=

参数用法：

![../../Attachment/clash-subconverter-20230523004944259.png](/img/user/Attachment/clash-subconverter-20230523004944259.png)

多条订阅：
1. 使用 | 拼接
2. 使用 urlencode 编码
3. 
例子：

```
You have 2 subscriptions and you want to merge them and generate a Clash subscription:
1. https://dler.cloud/subscribe/ABCDE?clash=vmess
2. https://rich.cloud/subscribe/ABCDE?clash=vmess

First use '|' to separate 2 subscriptions:
https://dler.cloud/subscribe/ABCDE?clash=vmess|https://rich.cloud/subscribe/ABCDE?clash=vmess

Then process it with URLEncode to get %URL%:
https%3A%2F%2Fdler.cloud%2Fsubscribe%2FABCDE%3Fclash%3Dvmess%7Chttps%3A%2F%2Frich.cloud%2Fsubscribe%2FABCDE%3Fclash%3Dvmess

Then fill %TARGET% and %URL% in Access Interface with actual values:
http://127.0.0.1:25500/sub?target=clash&url=https%3A%2F%2Fdler.cloud%2Fsubscribe%2FABCDE%3Fclash%3Dvmess%7Chttps%3A%2F%2Frich.cloud%2Fsubscribe%2FABCDE%3Fclash%3Dvmess

Finally subscribe this link in Clash and you are done!
```

# 进阶中文文档

[subconverter/README-cn.md at master · tindy2013/subconverter · GitHub](https://github.com/tindy2013/subconverter/blob/master/README-cn.md#%E8%BF%9B%E9%98%B6%E7%94%A8%E6%B3%95)


