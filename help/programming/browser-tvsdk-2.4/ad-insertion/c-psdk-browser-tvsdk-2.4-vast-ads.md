---
description: 当浏览器TVSDK请求的主广告服务器上没有的广告时，播放器需要从辅助服务器请求该广告。 视频广告服务模板(VAST)可设置广告服务器和视频播放器之间的通信标准，以及在请求广告时由辅助广告服务器发送的响应。
title: VAST广告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# VAST广告 {#vast-ads}

当浏览器TVSDK请求的主广告服务器上没有的广告时，播放器需要从辅助服务器请求该广告。 视频广告服务模板(VAST)可设置广告服务器和视频播放器之间的通信标准，以及在请求广告时由辅助广告服务器发送的响应。

有关VAST的详细信息，请参阅 [数字视频广告服务模板(VAST) 3.0](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf).

浏览器TVSDK支持以下VAST广告元素：

## 包装器和内联广告 {#section_11B8A1A8F52F4F77981C6AAC02185087}

支持以下元素：

* **`wrapper`** 当播放器需要联系辅助广告服务器以请求广告时，包装器元素提供重定向信息。 一个包装器元素可以指向多个最终指向VAST广告的包装器。

* **`inline`** 支持以下必需元素：

* `AdSystem`
* `AdTitle`
* `Impression`

  支持以下可选元素：

* `Description`
* `Survey`
* `Error`

## 创意人员 {#section_0121F948CB074E49A8132D202786CAA4}

此元素是一个文件，它是VAST广告的一部分并包含 `creative` 元素，该元素可以支持线性广告、非线性广告或伴随广告。 在 `creative` 元素， `id`， `sequence`、和 `adId` 支持元素。

以下是有关广告类型的更多信息：

* **线性广告** 支持以下元素：

   * `TrackingEvent`，其中包含 `Tracking` 元素。
      * `Duration`
      * `AdParameters`
      * `VideoClicks`，包括以下各项：

      * `ClickThrough`
      * `ClickTracking`
      * `CustomClick`

      * `MediaFiles`

      * `MediaFile`

        >[!TIP]
        >
        >在此元素中， `id`， `bitrate`， `delivery`， `width`， `height`， `scalable`， `maintainAspectRatio`， `apiFramework`、和 `type` 属性受支持。

* **非线性广告** 支持以下元素：

   * `Non-linear`

     >[!TIP]
     >
     >在此元素中， `id`， `width`， `height`， `apiFramework`， `expandedWidth`， `expandedHeight`， `scalable`， `maintainAspectRatio`、和 `minSuggestedDuration` 属性受支持。

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `NonLinearClickThrough`
      * `AdParameters`

* **伴随广告** 支持以下元素：

   * `Companion`

     >[!TIP]
     >
     >在此元素中， `id`， `width`， `height`， `apiFramework`， `expandedWidth`、和 `expandedHeight` 属性受支持。

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `TrackingEvents`

## 扩展 {#section_17401C75F419453BAE83637EEB6E1E60}

>[!TIP]
>
>仅支持特定于Auditude的扩展。

* `Extension`
