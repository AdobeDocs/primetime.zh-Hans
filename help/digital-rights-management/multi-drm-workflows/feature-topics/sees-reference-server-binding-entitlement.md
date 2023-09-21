---
description: SEES参考服务器显示如何使用ExpressPlay启用设备绑定权利服务。
title: 参考服务设备绑定授权
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# 参考服务：设备绑定授权 {#reference-service-device-binding-entitlement}

SEES参考服务器显示如何使用ExpressPlay启用设备绑定权利服务。

>[!NOTE]
>
>设备绑定权利服务也可以是时间绑定或提供租赁期限。

要引导 `device_id` 信息，播放一个虚拟M3U8内容。 然后，您可以在ExpressPlay令牌中嵌入Cookie，并生成SPC(其中包含 `device_id`)，并发送 `getToken` 到ExpressPlay服务器。

![](assets/fees-device-binding.png)

这个序列从播放一个虚拟M3U8开始。 Cookie将发送到SEES服务器以获取ExpressPlay令牌URL。 在收到Cookie绑定的ExpressPlay令牌URL后，下一步是生成SPC并将其发送到ExpressPlay服务器。 ExpressPlay服务器提取 `device_id` 来自SPC的ExpressPlay令牌URL的Cookie，并将Cookie和 `device_id` 在事务日志中。

客户端向SEES发出真正的许可证请求，以发送相同的Cookie。 SEES使用Cookie检索 `device_id` 从ExpressPlay服务器。

SEE请求设备绑定和时间绑定的ExpressPlay令牌，并将该令牌返回给客户端。

客户端使用ExpressPlay令牌发出许可证请求。

ExpressPlay服务器比较 `device_id` 在SPC中 `device_id` 在ExpressPlay令牌中。 ExpressPlay服务器仅在以下情况下颁发许可证： `device_id` 值匹配。
