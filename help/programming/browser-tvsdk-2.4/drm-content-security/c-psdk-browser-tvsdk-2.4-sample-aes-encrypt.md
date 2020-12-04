---
description: AES-128加密方法加密包括头在内的整个传输流(TS)容器时，SAMPLE-AES加密仅加密音频和部分视频数据。
seo-description: AES-128加密方法加密包括头在内的整个传输流(TS)容器时，SAMPLE-AES加密仅加密音频和部分视频数据。
seo-title: 范例AES加密的HLS流
title: 范例AES加密的HLS流
uuid: 32c1f87b-eb81-4e1c-92ea-ec37260a7ecb
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# 示例AES加密的HLS流{#sample-aes-encrypted-hls-streams}

AES-128加密方法加密包括头在内的整个传输流(TS)容器时，SAMPLE-AES加密仅加密音频和部分视频数据。

在加密流中，标识保护块，在该块上完成保护过程。 H.264视频保护块是网络适配层(NAL)单元的类型1和类型5的主体。 受保护的音频块是音频帧，音频必须采用AAC格式。

>[!IMPORTANT]
>
>您必须具有密钥和初始化矢量(IV)。 浏览器TVSDK在播放流之前使用密钥和IV解密该流。

每个受保护块包含一个16字节块的整数，这些块使用AES-128密码块链(CBC)模式加密，无填充。 CBC发生在每个受保护块中，并且在每个新保护块的开始,IV必须重置为其原始值。

支持以下编解码器：

* 对于视频，支持H.264。
* 对于音频，仅AAC支持sample-AES。

