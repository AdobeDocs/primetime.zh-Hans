---
description: 浏览器TVSDK当前支持播放清单和片段不包含扩展的流。
title: 无扩展流
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---


# 无扩展流{#extensionless-streams}

浏览器TVSDK当前支持播放清单和片段不包含扩展的流。

## 片段级别{#section_0E035129501D4A77BBC14192D8A53A86}

浏览器TVSDK解析响应的前几个字节以检测无扩展片段的内容类型。 如果未检测到有效的内容类型，则浏览器TVSDK将引发错误。

## 清单级别{#section_AAD9EBAC883D4CC3A0133A45B555EECF}

浏览器TVSDK使用在`replaceCurrentResource`方法中传递的`mediaResource.resourceType`参数来检测清单URL的内容类型。 有关详细信息，请参阅`AdobePSDK.MediaPlayer`类。

在UI Framework播放器中，可以按如下方式在媒体资源中指定资源类型：

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

如果未提供`resourceType`，则UI Framework会根据资源URL扩展确定资源类型，然后将该资源类型传递给`replaceCurrentResource`方法。

>[!TIP]
>
>对于无扩展清单，请确保在UI框架中加载资源时始终传递`resourceType`。

