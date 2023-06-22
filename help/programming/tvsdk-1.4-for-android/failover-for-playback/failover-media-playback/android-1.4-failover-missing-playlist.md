---
description: 当整个播放列表丢失时，例如，当在顶级清单文件中指定的M3U8文件未下载时，TVSDK将尝试恢复。 如果无法恢复，应用程序将决定下一步。
title: 缺少播放列表故障转移
exl-id: aab2dde3-aee2-4ade-b8f9-91c72df0c747
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# 缺少播放列表故障转移{#missing-playlist-failover}

当整个播放列表丢失时，例如，当在顶级清单文件中指定的M3U8文件未下载时，TVSDK将尝试恢复。 如果无法恢复，应用程序将决定下一步。

如果缺少与中间分辨率比特率关联的播放列表，TVSDK将搜索具有相同分辨率的变体播放列表。 如果找到相同分辨率，则开始从匹配位置下载变体播放列表和区段。 如果TVSDK找不到相同分辨率的播放列表，它将尝试循环查看其他比特率播放列表及其变体。 立即降低比特率是首选，然后是它的变体，依此类推。 如果在尝试查找有效播放列表时耗尽了所有较低比特率的播放列表及其变体，TVSDK将转到最高比特率并从此处开始计数。 如果找不到有效的播放列表，则播放过程将失败，播放器将转为“错误”状态。

您的应用程序可以决定如何处理这种情况。 例如，您可能希望关闭播放器活动并将用户定向到目录活动。 感兴趣的事件是 `STATE_CHANGED` 事件，相应的回调是 `onStateChanged` 方法。 以下代码用于监视播放器是否将其内部状态更改为“错误”：

```java
case ERROR: 
    getActivity().finish(); // this is where we close the current activity (the Player activity) 
    break;
```

欲了解更多信息，请参见 [!DNL PlayerFragment.java] SDK中的文件：

```
[…]/samples/PrimetimeReference/src/PrimetimeReference/src/com/adobe/primetime/reference/ui/player/
```

如果客户端网络已关闭，您可以使用此代码进行验证。

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

API将提供用于验证客户端网络是否关闭的URL。 这应该是一个有效的URL，它将在http请求中返回http响应代码200。

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

如果未设置setNetworkDownVerificationUrl，则TVSDK默认使用MainManifest url来判断网络是否关闭。
