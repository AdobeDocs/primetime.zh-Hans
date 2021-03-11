---
title: 使用输出保护策略
description: 使用输出保护策略
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# 使用输出保护策略{#using-output-protection-policies}

**Widevine输出保护策略**

Widevine本身支持模拟和数字输出保护限制。 请参阅您的Widevine服务提供商关于如何将这些策略附加到生成的许可证的文档。

如果使用Expressplay作为Widevine服务提供商，则通过hdcpOutputControl标志在令牌生成时附加数字输出保护策略：
允许的值为0、1、2，其中0 = HDCP_NONE，1 = HDCP_V1,2 = HDCP_V2。 HDCP_V1和HDCP_V2分别强制使用HDCP版本1.X和2.X。

Expressplay当前不支持附加模拟输出限制

**播放就绪输出保护策略**

PlayReady本身也支持模拟和数字输出保护限制。 可以设置的输出保护级别值。 页面[输出保护级别](https://msdn.microsoft.com/en-us/library/dn468831.aspx)将文档您可以设置的值及其预期的客户端行为。

如果您使用Expressplay，则通过compressedDigitalAudioOPL、uncompressedDigitalAudioOPL、compressedDigitalVideoOPL、uncompressedDigitalVideoOPL和unknownOutputBehavior标志在令牌生成时附加输出保护级别值。 这些文档记录在[PlayReady许可证令牌请求](https://www.expressplay.com/developer/restapi/#playready-license-token-request)
