---
description: 例如，当缺少整个播放列表时，如果顶级清单文件中指定的M3U8文件不下载，TVSDK将尝试恢复。 如果它无法恢复，则应用程序将决定下一步。
seo-description: 例如，当缺少整个播放列表时，如果顶级清单文件中指定的M3U8文件不下载，TVSDK将尝试恢复。 如果它无法恢复，则应用程序将决定下一步。
seo-title: 缺少播放列表故障转移
title: 缺少播放列表故障转移
uuid: 91a537f3-3e69-4669-8f84-0292c19ac209
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 缺少播放列表故障转移{#missing-playlist-failover}

例如，当缺少整个播放列表时，如果顶级清单文件中指定的M3U8文件不下载，TVSDK将尝试恢复。 如果它无法恢复，则应用程序将决定下一步。

如果缺少与中间分辨率比特率关联的播放列表，则TVSDK将搜索以相同分辨率的变体播放列表。 如果它找到相同的分辨率，则开始从匹配位置下载变体播放列表和段。 如果TVSDK找不到相同的分辨率播放列表，它将尝试循环播放其他比特率播放列表及其变体。 立即降低的比特率是第一个选择，然后是其变体，依此类推。 如果在尝试查找有效的播放列表时所有较低比特率的播放列表及其变体都已用尽，TVSDK将转到最高比特率并从那里向下计数。 如果找不到有效的播放列表，则进程将失败，并且播放器将移至ERROR状态。

您的应用程序可以确定如何处理这种情况。 例如，您可能希望关闭播放器活动并将用户定向到目录活动。 感兴趣的事件是事 `STATE_CHANGED` 件，相应的回调是方 `onStateChanged` 法。 以下代码监视播放器是否将其内部状态更改为ERROR:

```java
case ERROR: 
    getActivity().finish(); // this is where we close the current activity (the Player activity) 
    break;
```

有关详细信息，请参 [!DNL PlayerFragment.java] 阅SDK中的文件：

```
[…]/samples/PrimetimeReference/src/PrimetimeReference/src/com/adobe/primetime/reference/ui/player/
```

如果客户端网络关闭，您可以使用此代码进行验证。

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

API将提供用于验证客户端网络是否关闭的url。 这应该是有效的url，它在http请求上返回http响应代码200。

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

如果未设置setNetworkDownVerificationUrl，则TVSDK默认使用MainManifest URL确定网络是否关闭。
