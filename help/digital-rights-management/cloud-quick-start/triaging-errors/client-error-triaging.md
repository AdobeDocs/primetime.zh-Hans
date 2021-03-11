---
description: 有时，有时无法回放内容。 任何情况都可能导致这种情况，包括浏览器网络堆栈、传输层、操作系统、Flash Player运行时或Primetime DRM系统中的错误。
title: 裁切错误概述
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# 裁切错误{#triaging-errors}

有时，有时无法回放内容。 任何情况都可能导致这种情况，包括浏览器网络堆栈、传输层、操作系统、Flash Player运行时或Primetime DRM系统中的错误。

第一个诊断步骤是确定问题是否在未将DRM加密引入公式中的情况下显现。 尝试打包内容，但指示打包程序不加密内容。 如果问题仍然存在，则可能是对内容进行编码或打包的问题，或者是网络基础结构中的某个位置。 如果在未加密的情况下打包内容时问题消失，则播放失败可能是由于DRM问题，您应该参与客户端/服务器试用。

Primetime DRM（Primetime Cloud DRM之外）已进入市场多年。 因此，有大量关于Primetime DRM故障排除和配置的社区信息。 Adobe为Primetime DRM(以前称为Adobe访问)用户提供了一个论坛，用于聚合和共享问题和解决方案。 要确定以前是否讨论过您的问题，请检查：[https://forums.adobe.com/community/adobe_access](https://forums.adobe.com/community/adobe_access)

## 客户端错误检测{#section_D0EBAEB0C27F4B01BD44124DEE62F6BA}

如果内容不播放，请检查示例视频播放器的右侧面板，该面板将记录发生的任何`DRMErrorEvent`。 如果存在错误事件，则它将与以下Flash Player运行时错误之一关联：

* [DRM客户端错误消息引用](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages);或
* [AS3Flash运行时错误](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html) (DRM在3300发出开始)

