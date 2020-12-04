---
seo-title: 使用输出保护策略
title: 使用输出保护策略
uuid: f00d2a97-0036-41a6-ab44-391cc40b146e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# 使用输出保护策略{#using-output-protection-policies}

**Widevine输出保护策略**

Widevine本机支持模拟和数字输出保护限制。 请参阅Widevine服务提供商中有关如何将这些策略附加到生成的许可证的文档。

如果使用Expressplay作为Widevine服务提供商，则通过hdcpOutputControl标志在令牌生成时附加数字输出保护策略：
允许的值为0、1、2，其中0 = HDCP_NONE,1 = HDCP_V1,2 = HDCP_V2。 HDCP_V1和HDCP_V2分别强制使用HDCP版本1.X和2.X。

Expressplay当前不支持附加模拟输出限制

**播放就绪输出保护策略**

PlayReady本身还支持模拟和数字输出保护限制。 可设置的输出保护级别值。 页面[输出保护级别](https://msdn.microsoft.com/en-us/library/dn468831.aspx)将您可以设置的值及其预期的客户端行为文档起来。

如果使用Expressplay，则通过compressedDigitalAudioOPL、uncompressedDigitalAudioOPL、compressedDigitalVideoOPL、uncompressedDigitalVideoOPL和unknownOutputBehavior标志在令牌生成时附加输出保护级别值。 这些请求在[PlayReady许可证令牌请求](https://www.expressplay.com/developer/restapi/#playready-license-token-request)中有说明
