---
description: SEES引用服务器向您显示如何使用ExpressPlay启用设备绑定授权服务。
seo-description: SEES引用服务器向您显示如何使用ExpressPlay启用设备绑定授权服务。
seo-title: 引用服务设备绑定授权
title: 引用服务设备绑定授权
uuid: 22ce2f8e-1758-4528-8caf-60d209839afe
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# 参考服务：设备绑定授权{#reference-service-device-binding-entitlement}

SEES引用服务器向您显示如何使用ExpressPlay启用设备绑定授权服务。

>[!NOTE]
>
>设备绑定授权服务也可以是限时的或提供租用持续时间。

要引导`device_id`信息，请播放虚拟M3U8内容。 然后，您可以在ExpressPlay令牌中嵌入cookie，生成SPC（包含`device_id`），并将`getToken`发送到ExpressPlay服务器。

![](assets/fees-device-binding.png)

序列通过播放虚拟M3U8开始。 将Cookie发送到SEES服务器以获取ExpressPlay令牌URL。 接收到Cookie绑定的ExpressPlay令牌URL后，下一步是生成SPC并将其发送到ExpressPlay服务器。 ExpressPlay服务器从SPC提取`device_id`，从ExpressPlay令牌URL提取cookie，并将cookie和`device_id`放在事务日志中。

客户端向SEES发送相同的cookie发出真实的许可证请求。 SEES使用cookie从ExpressPlay服务器检索`device_id`。

SEES请求设备绑定的和时间绑定的ExpressPlay令牌，并将该令牌返回给客户端。

客户端使用ExpressPlay令牌发出许可证请求。

ExpressPlay服务器将SPC中的`device_id`与ExpressPlay令牌中的`device_id`进行比较。 仅当两个`device_id`值匹配时，ExpressPlay服务器才颁发许可证。
