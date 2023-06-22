---
description: 测试过程中的常见问题通常涉及您的ExpressPlay身份验证器、传输协议和所需的服务请求参数。
title: 快速入门疑难解答
exl-id: d8908f9c-98f4-4100-a003-d3b990105dee
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# 快速入门疑难解答{#troubleshooting-your-quick-start}

测试过程中的常见问题通常涉及您的ExpressPlay身份验证器、传输协议和所需的服务请求参数。

如果您的 [!DNL curl] 对ExpressPlay生成令牌的请求失败，响应正文将包含一个错误消息，解释失败的原因。

如果令牌生成成功，但内容仍未播放，请检查ExpressPlay令牌赎回日志中是否存在“令牌已过期”等错误。

如果令牌生成成功并且赎回没有错误，但视频仍然没有播放，请检查CEK是否与内容匹配，以及内容格式是否与目标设备的功能匹配。

此外：

* 检查您是否在服务请求中使用了正确的客户验证器。 当您想要使用测试验证器时，很容易意外使用生产验证器。 此外，请确保您使用的是 *您的* 验证者。 例如，在测试过程中，您可能会借用他人的 `curl` 命令，而忘记在验证器中替换他们的验证器。

* 检查您的请求或清单中是否使用了正确的传输协议( `https://` 对比 `https://`或者公平竞争公司， `skd://` 对比 `https://` 对比 `https://`.

* 确保包括您正在使用的DRM解决方案所需的所有查询参数。 例如，很容易混淆PlayReady和Widevine，因为它们都使用DASH，但所需的请求参数和封装配置不同。
* 确认您的ExpressPlay帐户有足够的令牌积分，并且尚未用完。
* 确认发送到TVSDK的三重DRM数据正确：ExpressPlay令牌、许可证服务器URL和DRM类型。
* 确认所有组件对使用哪个ExpressPlay环境所做的假设与对测试环境和生产环境所做的假设相同。
* 请注意，不同的浏览器通常仅支持一个DRM用于DASH内容。
* 从TVSDK 2.4起，仅支持DASH-LIVE打包配置文件。 （DASH-OnDemand支持正在规划中。）
* 由于设备制造商的限制，AndroidTV PlayReady支持会断断续续。 举个例子，

   * razer Forge设备出现PlayReady内容问题
   * Amazon FireTV不能使用已加密音轨的DASH内容

* 从TVSDK 2.4开始，只有AndroidTV设备通常同时支持PlayReady和Widevine DRM。 所有其他Android设备通常仅支持Widevine。
* 截至TVSDK 2.4，Android TVSDK当前要求PSSH框位于.mpd清单中。 这与DASH标准相反，该标准规定PSSH框可以位于任何位置，如内容本身，而不仅仅是.mpd。
