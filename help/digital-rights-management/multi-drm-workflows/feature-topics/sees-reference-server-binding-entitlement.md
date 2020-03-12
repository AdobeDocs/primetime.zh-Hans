---
description: SEES参考服务器向您展示如何使用ExpressPlay启用设备绑定授权服务。
seo-description: SEES参考服务器向您展示如何使用ExpressPlay启用设备绑定授权服务。
seo-title: 参考服务设备绑定授权
title: 参考服务设备绑定授权
uuid: 22ce2f8e-1758-4528-8caf-60d209839afe
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 参考服务：设备绑定授权 {#reference-service-device-binding-entitlement}

SEES参考服务器向您展示如何使用ExpressPlay启用设备绑定授权服务。

>[!NOTE]
>
>设备绑定授权服务也可以是限时的或提供租用持续时间。

要引导信 `device_id` 息，请播放虚拟M3U8内容。 然后，您可以在ExpressPlay令牌中嵌入cookie，生成SPC(其中包含 `device_id`)，并将cookie发送到ExpressPlay `getToken` 服务器。

![](assets/fees-device-binding.png)

序列通过播放虚拟M3U8开始。 Cookie将发送到SEES服务器以获取ExpressPlay令牌URL。 在收到绑定了cookie的ExpressPlay令牌URL后，下一步是生成SPC并将其发送到ExpressPlay服务器。 ExpressPlay服务器从SPC `device_id` 中提取cookie，从ExpressPlay令牌URL中提取cookie，并将cookie和 `device_id` 放入事务日志中。

客户端向SEES发送相同的Cookie发出真实的许可证请求。 SEES使用cookie从ExpressPlay服 `device_id` 务器检索。

SEES请求设备绑定和时间绑定的ExpressPlay令牌，并将该令牌返回给客户端。

客户端使用ExpressPlay令牌发出许可证请求。

ExpressPlay服务器将SPC `device_id` 中的与ExpressPlay令牌 `device_id` 中的进行比较。 ExpressPlay服务器仅在两个值匹配时发 `device_id` 行许可证。
