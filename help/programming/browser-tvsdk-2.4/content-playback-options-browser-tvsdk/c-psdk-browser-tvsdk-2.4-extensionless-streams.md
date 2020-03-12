---
description: 浏览器TVSDK当前支持播放清单和片段不包含扩展的流。
seo-description: 浏览器TVSDK当前支持播放清单和片段不包含扩展的流。
seo-title: 无扩展流
title: 无扩展流
uuid: c69ba62b-a940-4211-920d-2e559849fd6d
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 无扩展流{#extensionless-streams}

浏览器TVSDK当前支持播放清单和片段不包含扩展的流。

## 片段级别 {#section_0E035129501D4A77BBC14192D8A53A86}

浏览器TVSDK会解析响应的前几个字节，以检测无扩展片段的内容类型。 如果未检测到有效的内容类型，则浏览器TVSDK将引发错误。

## 清单级别 {#section_AAD9EBAC883D4CC3A0133A45B555EECF}

浏览器TVSDK使用 `mediaResource.resourceType` 方法中传递的参数 `replaceCurrentResource` 来检测清单URL的内容类型。 有关详细信息，请参阅 `AdobePSDK.MediaPlayer` 类。

在UI Framework播放器中，您可以按如下方式在媒体资源中指定资源类型：

```js
var playerWrapper = ptp.videoPlayer('.videoDiv', { 
  player: { 
    mediaResource: { 
      resourceUrl:'Specify Resource Url', 
      resourceType: ‘Specify Resource Type. Refer AdobePSDK.MediaResourceType' 
    } 
  } 
}); 
```

如果 `resourceType` 未提供，则UI框架会根据资源URL扩展确定资源类型，然后将该资源类型传递给 `replaceCurrentResource` 方法。

>[!TIP]
>
>对于无扩展清单，请确 `resourceType` 保在UI框架中加载资源时始终传递。

