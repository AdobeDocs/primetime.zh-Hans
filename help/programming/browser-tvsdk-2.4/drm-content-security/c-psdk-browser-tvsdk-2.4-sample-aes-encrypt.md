---
description: 虽然AES-128加密方法对整个传输流(TS)容器（包括报头）进行加密，但SAMPLE-AES加密仅对音频和部分视频数据进行加密。
title: AES加密HLS流示例
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# AES加密HLS流示例{#sample-aes-encrypted-hls-streams}

虽然AES-128加密方法对整个传输流(TS)容器（包括报头）进行加密，但SAMPLE-AES加密仅对音频和部分视频数据进行加密。

在加密的流中，识别保护过程在其上完成的受保护块。 H.264视频保护块是网络适配层(NAL)单元类型1和5的主体。 音频的受保护块是音频帧，音频必须采用AAC格式。

>[!IMPORTANT]
>
>您必须具有密钥和初始化矢量(IV)。 浏览器TVSDK在播放流之前使用键和IV对其进行解密。

每个受保护的块都包含一个16字节块的整数，这些块使用AES-128加密块链(CBC)模式进行加密而不使用任何填充。 CBC发生在每个受保护块中，并且在每个新的受保护块开始时，IV必须重置为其原始值。

支持以下编解码器：

* 对于视频，支持H.264。
* 对于音频，仅支持AAC的sample-AES。
