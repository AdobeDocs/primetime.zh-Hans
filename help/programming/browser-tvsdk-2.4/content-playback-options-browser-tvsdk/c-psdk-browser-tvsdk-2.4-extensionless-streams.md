---
description: 浏览器TVSDK当前支持播放清单和片段不包含扩展的流。
title: 无扩展性流
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# 无扩展性流{#extensionless-streams}

浏览器TVSDK当前支持播放清单和片段不包含扩展的流。

## 片段级别 {#section_0E035129501D4A77BBC14192D8A53A86}

浏览器TVSDK解析响应的前几个字节以检测无扩展片段的内容类型。 如果未检测到有效的内容类型，则浏览器TVSDK将引发错误。

## 清单级别 {#section_AAD9EBAC883D4CC3A0133A45B555EECF}

浏览器TVSDK使用 `mediaResource.resourceType` 传入的参数 `replaceCurrentResource` 用于检测清单URL的内容类型的方法。 欲了解更多信息，请参见 `AdobePSDK.MediaPlayer` 类。

在UI Framework播放器中，您可以在媒体资源中指定资源类型，如下所示：

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

如果 `resourceType` 如果未提供，则UI框架会从资源URL扩展确定资源类型，然后将该类型传递到 `replaceCurrentResource` 方法。

>[!TIP]
>
>对于无扩展清单，请确保 `resourceType` 始终在UI Framework中加载资源时传递。
