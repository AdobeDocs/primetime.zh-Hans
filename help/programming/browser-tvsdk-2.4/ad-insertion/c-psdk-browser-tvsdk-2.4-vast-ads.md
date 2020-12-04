---
description: 当浏览器TVSDK请求的广告不在主广告服务器上时，播放器需要从辅助服务器请求该广告。 视频广告服务模板(VAST)设置广告服务器与视频播放器之间通信的标准，是次要广告服务器在请求广告时发送的响应。
seo-description: 当浏览器TVSDK请求的广告不在主广告服务器上时，播放器需要从辅助服务器请求该广告。 视频广告服务模板(VAST)设置广告服务器与视频播放器之间通信的标准，是次要广告服务器在请求广告时发送的响应。
seo-title: 广告
title: 广告
uuid: 052dae0c-2425-456c-aebe-531f68bb5aa8
translation-type: tm+mt
source-git-commit: 23a48208ac1d3625ae7d925ab6bfba8f2a980766
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# 广告{#vast-ads}

当浏览器TVSDK请求的广告不在主广告服务器上时，播放器需要从辅助服务器请求该广告。 视频广告服务模板(VAST)设置广告服务器与视频播放器之间通信的标准，是次要广告服务器在请求广告时发送的响应。

有关VAST的详细信息，请参阅[数字视频广告投放模板(VAST)3.0](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf)。

浏览器TVSDK支持以下VAST广告元素：

## 包装器和内联广告{#section_11B8A1A8F52F4F77981C6AAC02185087}

支持以下元素：

* **`wrapper`** 当播放器需要联系辅助广告服务器来请求广告时，包装器元素提供重定向信息。一个包装器元素可以指向几个包装器，这些包装器最终指向一个VAST广告。

* **`inline`** 支持以下必需元素：

* `AdSystem`
* `AdTitle`
* `Impression`

   支持以下可选元素：

* `Description`
* `Survey`
* `Error`

## 创意{#section_0121F948CB074E49A8132D202786CAA4}

此元素是VAST广告的一部分，并包含一个`creative`元素，该元素可支持线性广告、非线性广告或配套广告。 在`creative`元素中，支持`id`、`sequence`和`adId`元素。

以下是有关广告类型的更多信息：

* **线性** 广告支持以下元素：

   * `TrackingEvent`，其中包含 `Tracking` 元素。
      * `Duration`
      * `AdParameters`
      * `VideoClicks`，包括：

      * `ClickThrough`
      * `ClickTracking`
      * `CustomClick`

      * `MediaFiles`

      * `MediaFile`

         >[!TIP]
         >
         >在此元素中，支持`id`、`bitrate`、`delivery`、`width`、`height`、`scalable`、`maintainAspectRatio`、`apiFramework`和`type`属性。

* **非线性广** 告支持以下元素：

   * `Non-linear`

      >[!TIP]
      >
      >在此元素中，支持`id`、`width`、`height`、`apiFramework`、`expandedWidth`、`expandedHeight`、`scalable`、`maintainAspectRatio`和`minSuggestedDuration`属性。

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `NonLinearClickThrough`
      * `AdParameters`

* **配套** 广告支持以下元素：

   * `Companion`

      >[!TIP]
      >
      >在此元素中，支持`id`、`width`、`height`、`apiFramework`、`expandedWidth`和`expandedHeight`属性。

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `TrackingEvents`

## 扩展{#section_17401C75F419453BAE83637EEB6E1E60}

>[!TIP]
>
>仅支持特定于Auditude的扩展。

* `Extension`
