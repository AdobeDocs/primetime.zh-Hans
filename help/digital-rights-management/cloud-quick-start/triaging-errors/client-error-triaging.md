---
description: 有时，内容无法播放。 任何数量的情况都可能导致此问题，包括浏览器网络栈栈、传输层、操作系统、Flash Player运行时或Primetime DRM系统中的错误。
title: 分类错误概述
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# 分类错误 {#triaging-errors}

有时，内容无法播放。 任何数量的情况都可能导致此问题，包括浏览器网络栈栈、传输层、操作系统、Flash Player运行时或Primetime DRM系统中的错误。

第一个诊断步骤是确定问题是否在没有将DRM加密引入方程式的情况下显现出来。 尝试打包内容，但指示打包程序不要加密内容。 如果问题仍然存在，则可能是编码或打包内容或者网络基础架构中的某个位置有问题。 如果在未加密的情况下打包内容时问题消失，则播放失败可能是由于DRM问题导致的，您应该进行客户端/服务器分级。

Primetime DRM（Primetime Cloud DRM之外）已在市场销售了几年。 因此，在故障排除和配置Primetime DRM方面，提供了丰富的社区来源信息。 Adobe为Primetime DRM(以前称为Adobe访问)用户提供了一个论坛，以汇总和共享问题和解决方案。 要确定以前是否讨论过您的问题，请检查： [https://forums.adobe.com/community/adobe_access](https://forums.adobe.com/community/adobe_access)

## 客户端错误分级 {#section_D0EBAEB0C27F4B01BD44124DEE62F6BA}

如果内容未播放，请检查示例视频播放器的右侧面板，其中将记录任何 `DRMErrorEvent` 就会发生。 如果存在错误事件，则它将与以下某个Flash Player运行时错误相关联：

* [DRM客户端错误消息参考](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)；或
* [AS3Flash运行时错误](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html) （DRM问题开始于3300）
