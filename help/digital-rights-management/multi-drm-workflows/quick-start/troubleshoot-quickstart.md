---
description: 测试过程中的常见问题通常涉及ExpressPlay身份验证器、传输协议和所需的服务请求参数。
title: 快速开始疑难解答
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---


# 快速开始疑难解答{#troubleshooting-your-quick-start}

测试过程中的常见问题通常涉及ExpressPlay身份验证器、传输协议和所需的服务请求参数。

如果[!DNL curl]请求ExpressPlay以生成令牌失败，响应主体将包含一条错误消息，说明失败的原因。

如果令牌生成成功，但内容仍不播放，请检查ExpressPlay令牌兑换日志中是否有“过期令牌”等错误。

如果令牌生成成功且兑换没有错误，但视频仍不播放，请检查CEK是否与内容匹配，内容格式是否与目标设备的功能匹配。

此外：

* 检查您在服务请求中是否使用了正确的客户身份验证器。 在您要使用测试身份验证器时，很容易意外使用生产身份验证器。 另外，请确保您使用&#x200B;*您的*&#x200B;身份验证器。 例如，在测试过程中，您可能会借用他人的`curl`命令，然后忘记用您的身份验证器替换他们的。

* 检查您的请求或清单中是否使用了正确的传输协议(`https://`与`https://`，或者对于FairPlay，`skd://`与`https://`与`https://`。

* 确保包括您正在处理的DRM解决方案的所有所需查询参数。 例如，很容易混淆PlayReady和Widevine，因为它们都使用DASH，但所需的请求参数和打包配置不同。
* 确认您的ExpressPlay帐户有足够的令牌信用且尚未用尽。
* 确认发送到TVSDK的DRM数据的三重态正确：ExpressPlay令牌、许可证服务器URL和DRM类型。
* 确认您的所有组件都假设ExpressPlay环境的使用与有两个环境（测试和生产）相同。
* 请注意，不同的浏览器通常只支持DRM内容。
* 自TVSDK 2.4起，仅支持DASH-LIVE打包用户档案。 （DASH-OnDemand支持在路线图中。）
* 由于设备制造商的限制，AndroidTV PlayReady支持是间歇性的。 举个例子，

   * Razer Forge设备存在PlayReady内容问题
   * Amazon FireTV无法使用已加密音轨的DASH内容

* 自TVSDK 2.4起，通常只有AndroidTV设备同时支持PlayReady和Widevine DRM。 所有其他Android设备通常仅支持Widevine。
* 自TVSDK 2.4起，Android TVSDK当前要求PSSH框位于.mpd清单中。 这与DASH标准相反，DASH标准指定PSSH框可以位于任何位置，如内容本身，而不仅仅是.mpd中。

