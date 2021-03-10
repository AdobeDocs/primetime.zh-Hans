---
description: AES-128加密方法加密包括头在内的整个传输流(TS)容器，而SAMPLE-AES加密仅加密音频和部分视频数据。
title: AES加密的HLS流示例
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---


# 示例AES加密的HLS流{#sample-aes-encrypted-hls-streams}

AES-128加密方法加密包括头在内的整个传输流(TS)容器，而SAMPLE-AES加密仅加密音频和部分视频数据。

在加密流中，标识保护块，在该块上完成保护过程。 H.264视频保护块是网络适配层(NAL)单元的类型1和类型5的主体。 受保护的音频块是音频帧，音频必须采用AAC格式。

>[!IMPORTANT]
>
>您必须具有密钥和初始化矢量(IV)。 浏览器TVSDK在播放流之前使用密钥和IV解密流。

每个受保护块包含一个16字节块的整数，这些块使用无填充的AES-128密码块链(CBC)模式加密。 CBC发生在每个受保护块中，并且在每个新受保护块的开始,IV必须重置为其原始值。

支持以下编解码器：

* 对于视频，支持H.264。
* 对于音频，仅AAC支持sample-AES。

