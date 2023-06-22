---
title: DRM 5.3.1发行说明
description: DRM 5.3.1发行说明介绍了DRM 5.3.1中的新功能和已知问题。
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: e4e0a933-cfc6-4713-ae13-5df11cfc1aad
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# DRM 5.3.1发行说明 {#drm-release-notes}

DRM 5.3.1发行说明介绍了DRM 5.3.1中的新功能和已知问题。

## 版本5.3中的新增功能 {#new-features}

* **安全停止 —** 您可以指定在播放窗口结束时是停止播放还是继续播放。
* **基于分辨率的输出保护(RBOP) -** 可根据像素分辨率指定输出约束。
* **CDM选通 —** 为了支持HTML5，Adobe更新了Adobe Primetime DRM(以前称为Adobe访问DRM) Java SDK随附的参考实施许可证服务器，以便能够在单个URL端点使用所有DRM协议消息。 为了符合CDM(HTML解密模块)DRM供应商需要实现的EME（加密媒体扩展）规范，必须整合HTTP URL方法。 以前，它们是参考实施许可证服务器公开的唯一一个URL端点：

   * /flashaccess/i15n/v3（个性化）
   * /flashaccess/license/v5 （许可证请求）
   * /flashaccess/licenseRet/v5 （许可证返回）
   * /flashaccess/getServerVersion/v5 （获取服务器版本）

现在，所有请求(来自HTML5 CDM)都可以定向到单个端点：/req

这一变化向后兼容非CDM平台，如Flash Player、Android、iOS。

* **RBOP缩放 —** 特定于HTML5空间，RBOP包含自动缩减缩放功能，其中，如果比特率超过DRM策略中指定的允许比特率，则内容将被缩减到允许的最大分辨率。 例如，如果将1080p流流式传输到在非HDCP兼容监视器上显示内容的客户端，则DRM策略可能指示最大分辨率应为720p。 Primetime DRM将解码1080p流，然后将其缩小到720p，然后再将其呈现在屏幕上。 如果播放视频的浏览器随后被拖到支持HDCP的监视器上，Primetime DRM将停止缩减内容缩放并允许1080播放该内容。

## 版本5.3中的已知问题 {#known-issues}

* `Hasher.bat (flashaccess-hasher.jar)` 将日志消息输出到 `flashaccess-global.log.`您必须确保 `flashaccess-global.log` 文件与Hasher.bat位于同一目录中。

* 某些 `toJSON()`呼叫返回 `Strings` 以独立方式（即没有JSON结构的组合）不完全符合JSON规范或完全符合规范。

* Xbox密钥服务器接受版本值不等于1的密钥请求。

Xbox密钥服务器应仅支持版本等于1的密钥请求，但当前，服务器接受版本不是1的密钥请求。

* Xbox密钥服务器无法正确验证策略。

Xbox密钥服务器不应接受超出有效期的策略，但当前服务器接受这些策略，无论如何都接受。

* Xbox密钥服务器应拒绝包含使用错误的打包程序证书创建的元数据的密钥请求。
* 对于基于分辨率的输出保护相关类，某些JSON结构的返回值格式不正确。

多个类实施了一个toJSON()方法，该方法应以String的形式返回该对象的JSON兼容表示形式，但当前返回的值不完全符合JSON。

## 有用资源 {#helpful-resources}

* 请参阅完整的帮助文档，网址为 [Adobe Primetime学习与支持](https://helpx.adobe.com/support/primetime.html) 页面。
