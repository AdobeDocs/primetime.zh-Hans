---
description: SEES参考服务器向您显示如何使用ExpressPlay启用设备绑定授权服务。
title: 参考服务设备绑定授权
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# 参考服务：设备绑定授权{#reference-service-device-binding-entitlement}

SEES参考服务器向您显示如何使用ExpressPlay启用设备绑定授权服务。

>[!NOTE]
>
>设备绑定的授权服务也可以是限时的或提供租用持续时间。

要引导`device_id`信息，请播放虚拟M3U8内容。 然后，您可以在ExpressPlay令牌中嵌入一个Cookie，生成一个SPC（包含`device_id`），并将`getToken`发送到ExpressPlay服务器。

![](assets/fees-device-binding.png)

序列通过播放虚拟M3U8开始。 将Cookie发送到SEES服务器以获取ExpressPlay令牌URL。 接收到绑定Cookie的ExpressPlay令牌URL后，下一步是生成SPC并将其发送到ExpressPlay服务器。 ExpressPlay服务器从SPC中提取`device_id`，从ExpressPlay令牌URL提取Cookie，并将Cookie和`device_id`放在事务日志中。

客户端向发送相同Cookie的SEES发出真实的许可证请求。 SEES使用cookie从ExpressPlay服务器检索`device_id`。

SEES请求设备绑定的和时间绑定的ExpressPlay令牌，并将该令牌返回给客户端。

客户端使用ExpressPlay令牌发出许可证请求。

ExpressPlay服务器将SPC中的`device_id`与ExpressPlay令牌中的`device_id`进行比较。 只有两个`device_id`值匹配时，ExpressPlay服务器才会发出许可证。
