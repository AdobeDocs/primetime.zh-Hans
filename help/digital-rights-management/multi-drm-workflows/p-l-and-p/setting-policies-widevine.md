---
title: 使用输出保护策略
description: 使用输出保护策略
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# 使用输出保护策略{#using-output-protection-policies}

**Widevine输出保护策略**

Widevine本机支持模拟和数字输出保护限制。 请参阅Widevine服务提供商提供的文档，了解如何将这些策略附加到生成的许可证。

如果您使用Expressplay作为Widevine服务提供商，则通过hdcpOutputControl标志在令牌生成时附加数字输出保护策略：允许值为0、1、2，其中0 = HDCP_NONE、1 = HDCP_V1、2 = HDCP_V2。 HDCP_V1和HDCP_V2分别强制执行HDCP版本1.X和2.X。

Expressplay当前不支持附加模拟输出限制

**PlayReady输出保护策略**

PlayReady本身也支持模拟和数字输出保护限制。 可设置的输出保护级别值。 页面 [输出保护级别](https://msdn.microsoft.com/en-us/library/dn468831.aspx) 记录您可以设置的值及其预期客户端行为。

如果您使用Expressplay，则在令牌生成时通过compressedDigitalAudioOPL、uncompressedDigitalAudioOPL、compressedDigitalVideoOPL、uncompressedDigitalVideoOPL和unknownOutputBehavior标志附加输出保护级别值。 这些文档位于 [PlayReady许可证令牌请求](https://www.expressplay.com/developer/restapi/#playready-license-token-request)
