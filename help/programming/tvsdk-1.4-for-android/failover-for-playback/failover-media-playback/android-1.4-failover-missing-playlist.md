---
description: 如果缺少整个播放列表，例如，当顶级清单文件中指定的M3U8文件不下载时，TVSDK会尝试恢复。 如果它无法恢复，则由应用程序决定下一步。
seo-description: 如果缺少整个播放列表，例如，当顶级清单文件中指定的M3U8文件不下载时，TVSDK会尝试恢复。 如果它无法恢复，则由应用程序决定下一步。
seo-title: 缺少播放列表故障转移
title: 缺少播放列表故障转移
uuid: 91a537f3-3e69-4669-8f84-0292c19ac209
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# 缺少播放列表故障转移{#missing-playlist-failover}

如果缺少整个播放列表，例如，当顶级清单文件中指定的M3U8文件不下载时，TVSDK会尝试恢复。 如果它无法恢复，则由应用程序决定下一步。

如果缺少与中分辨率比特率关联的播放列表，则TVSDK将以相同分辨率搜索变体播放列表。 如果找到相同的分辨率，则开始从匹配位置下载变体播放列表和区段。 如果TVSDK找不到相同的分辨率播放列表，它将尝试循环播放其他比特率播放列表及其变体。 立即降低比特率是首选，然后是其变体，依此类推。 如果在尝试查找有效的播放列表时，所有较低比特率的播放列表及其变体都已用尽，则TVSDK将转到最高比特率，并从那里向下计数。 如果找不到有效的播放列表，则进程将失败，并且播放器将移至ERROR状态。

您的应用程序可以确定如何处理这种情况。 例如，您可能希望关闭播放器活动并将用户定向到目录活动。 感兴趣的事件是`STATE_CHANGED`事件，相应的回调是`onStateChanged`方法。 以下代码监视播放器是否将其内部状态更改为ERROR:

```java
case ERROR: 
    getActivity().finish(); // this is where we close the current activity (the Player activity) 
    break;
```

有关详细信息，请参阅SDK中的[!DNL PlayerFragment.java]文件：

```
[…]/samples/PrimetimeReference/src/PrimetimeReference/src/com/adobe/primetime/reference/ui/player/
```

如果客户端网络关闭，则可使用此代码进行验证。

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

API将提供用于验证客户端网络是否关闭的url。 这应该是有效的url，在http请求上返回http响应代码200。

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

如果未设置setNetworkDownVerificationUrl，则TVSDK默认使用MainManifest url来确定网络是否关闭。
