---
title: DRM 5.3.1发行说明
description: DRM 5.3.1发行说明描述了DRM 5.3.1中的新增功能和已知问题。
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---


# DRM 5.3.1发行说明{#drm-release-notes}

DRM 5.3.1发行说明描述了DRM 5.3.1中的新增功能和已知问题。

## 5.3 {#new-features}版中的新增功能

* **安全停止 —** 您可以指定在播放窗口的末尾停止还是继续播放。
* **基于分辨率的输出保护(RBOP)-** 您可以根据像素分辨率指定输出约束。
* **CDM门控 —** 为了支持HTML5,Adobe已更新Adobe Primetime DRM(以前称为Adobe Access DRM)Java SDK附带的参考实施许可证服务器，以便能够在单个URL端点使用所有DRM协议消息。为了符合HTML5 EME（加密媒体扩展）规范，必须对HTTP URL方法进行这种整合，而CDM（内容解密模块）DRM供应商又需要实施该规范。 以前，这些是引用实施许可证服务器公开的唯一URL端点：

   * /flashaccess/i15n/v3（个性化）
   * /flashaccess/license/v5（许可证请求）
   * /flashaccess/licenseRet/v5（许可证退回）
   * /flashaccess/getServerVersion/v5（获取服务器版本）

现在，所有请求（源自HTML5 CDM）都可定向到单个端点：/req

此更改与非CDM平台(如Flash Player、Android、iOS)向后兼容。

* **RBOP缩减缩放 —** 特定于HTML5空间，RBOP包含自动缩减缩放功能，其中，如果比特率超过DRM策略中指定的允许比特率，则内容将缩减到最大允许分辨率。例如，如果1080p流流流式传输到在非HDCP兼容监视器上显示内容的客户端，则DRM策略可能指示最大分辨率应为720p。 Primetime DRM将解码1080p流，然后将其缩小到720p，然后再将其呈现在屏幕上。 如果播放视频的浏览器随后被拖动到支持HDCP的监视器上，Primetime DRM将停止缩放内容，并允许在1080时播放。

## 版本5.3 {#known-issues}中的已知问题

* `Hasher.bat (flashaccess-hasher.jar)` 将日志消息输 `flashaccess-global.log.`出到您必须确 `flashaccess-global.log` 保文件与Hasher.bat位于同一目录中。

* 某些`toJSON()`调用的输出会以独立方式返回`Strings`，这些调用不完全符合JSON或完全符合JSON（即，不合成JSON结构）。

* Xbox密钥服务器接受版本值不等于1的密钥请求。

Xbox密钥服务器应仅支持版本等于1的密钥请求，但目前，服务器接受版本不为1的密钥请求。

* Xbox密钥服务器无法正确验证策略。

Xbox密钥服务器不应接受在有效日期以外的策略，但目前，服务器接受这些策略，无论如何。

* Xbox密钥服务器应拒绝包含使用错误打包程序证书创建的元数据的密钥请求。
* 某些JSON结构的返回值的格式不正确，无法用于与Resolution Output Protection相关的类。

几个类实现一个toJSON()方法，该方法应将该对象的符合JSON的表示形式返回为String，但当前返回的值不完全符合JSON。

## 有用资源{#helpful-resources}

* 请参阅[Adobe Primetime学习和支持](https://helpx.adobe.com/support/primetime.html)页面上的完整帮助文档。
