---
description: 创意重新打包服务(CRS)可确保非HLS广告创意可在HLS流中正确回放。 清单服务器在遇到非HLS广告时调用CRS。
seo-description: 创意重新打包服务(CRS)可确保非HLS广告创意可在HLS流中正确回放。 清单服务器在遇到非HLS广告时调用CRS。
seo-title: CRS概述
title: CRS概述
uuid: 3ae75fa7-397f-47ba-8e3d-50543ca25458
translation-type: tm+mt
source-git-commit: 4788a8de8ba47d7f448967066e1bd0fb73fdb7a8

---


# CRS概述 {#overview-of-crs}

创意重新打包服务(CRS)可确保非HLS广告创意可在HLS流中正确回放。 清单服务器在遇到非HLS广告时调用CRS。

>[!NOTE]
>
>默认情况下，CRS处于禁用状态。 要为您的帐户启用CRS，请与您的Adobe技术客户经理联系。
>
>有关在TVSDK应用程序中启用CRS的信息，请参阅您的平台的《程序员指南》中的 *“在TVSDK应用程序中启用CRS* ”主题。 例如，对于Android 3.4，请参阅在TVSDK应 [用程序中启用CRS](../../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-transcoding/android-3x-ad-transcoding.md)

CRS为内容流准备HTTP实时流(HLS)和创意，并为客户端广告跟踪注入ID3数据包。 它将从第三方广告服务器、广告网络和代理服务器接收的MP4、FLV和WebM文件转码为HLS格式。

当Adobe Primetime广告插入遇到非HLS广告创意时，它会将其发送到CRS以重新打包，通常不超过三分钟。 CRS将转码广告创意发送到CDN服务器以供将来使用。 这叫做 **`just-in-time (JIT) repackaging`**。 您还可以使用重新打包API在需要广告创意之前转 [码广告](../../dynamic-ad-insertion/creative-repackaging-service/api-repackage.md) 。 这叫做 *`asynchronous repackaging`*。

如果您的Adobe技术客户经理还可以更改某些CRS默认行为（如果其他行为更适合您的应用程序）。 这些是：

* 广告创意格式的优先级。

   VAST/ `MediaFiles` VMAP响应的部分可包含不同类型的创意 `MediaFile` 人员。 默认情况下，清单服务器根据一组固定的优先级(、、、、) `application/x-mpegURL`选择 `application/vnd.apple.mpegURL`一 `video/mp4`个清单服 `video/x-flv,video/webm`务器。 Adobe可以更改帐户的优先级。
* 广告目标持续时间。

   清单服务器从内容播放列表检测目标广告持续时间并将其发送到CRS。 Adobe可以更改此行为，以便CRS始终使用您为帐户指定的固定持续时间。
