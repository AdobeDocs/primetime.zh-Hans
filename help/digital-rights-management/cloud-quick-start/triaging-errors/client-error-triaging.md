---
description: 有时，有时内容无法回放。 任何情况都可能导致这种情况，包括浏览器网络堆栈、传输层、操作系统、Flash Player运行时或Primetime DRM系统中的错误。
seo-description: 有时，有时内容无法回放。 任何情况都可能导致这种情况，包括浏览器网络堆栈、传输层、操作系统、Flash Player运行时或Primetime DRM系统中的错误。
seo-title: 查找错误概述
title: 查找错误概述
uuid: 44b4ab0e-5f08-44b0-bcb5-a869f6add69b
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---


# 查找错误{#triaging-errors}

有时，有时内容无法回放。 任何情况都可能导致这种情况，包括浏览器网络堆栈、传输层、操作系统、Flash Player运行时或Primetime DRM系统中的错误。

第一个诊断步骤是确定问题是否在未将DRM加密引入等式的情况下显现。 尝试打包内容，但指示打包程序不加密内容。 如果问题仍然存在，则可能是对内容进行编码或打包的问题，或者是网络基础架构中的某个位置。 如果在未加密的情况下打包内容时问题消失，则播放失败可能是由于DRM问题造成的，您应进行客户端／服务器试用。

Primetime DRM（Primetime Cloud DRM之外）已进入市场多年。 因此，有大量关于Primetime DRM故障排除和配置的社区来源信息。 Adobe为Primetime DRM(以前称为“Adobe访问”)用户提供了论坛，让他们能够聚合并分享问题和解决办法。 要确定之前是否讨论过您的问题，请检查：[https://forums.adobe.com/community/adobe_access](https://forums.adobe.com/community/adobe_access)

## 客户端错误检测{#section_D0EBAEB0C27F4B01BD44124DEE62F6BA}

如果内容不播放，请检查示例视频播放器的右侧面板，该面板将记录出现的任何`DRMErrorEvent`。 如果存在错误事件，则它将与Flash Player运行时错误之一相关：

* [DRM客户端错误消息引用](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages);或
* [AS3Flash运行时错误](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html) (DRM发出开始,3300)

