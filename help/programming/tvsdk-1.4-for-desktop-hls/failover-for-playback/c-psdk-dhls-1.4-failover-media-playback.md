---
description: 对于实时和视频点播(VOD)媒体，TVSDK通过下载与中分辨率比特率相关的播放列表来开始播放，并下载由该播放列表定义的媒体段。 它快速选择高分辨率比特率的播放列表及其相关媒体并继续下载过程。
seo-description: 对于实时和视频点播(VOD)媒体，TVSDK通过下载与中分辨率比特率相关的播放列表来开始播放，并下载由该播放列表定义的媒体段。 它快速选择高分辨率比特率的播放列表及其相关媒体并继续下载过程。
seo-title: 媒体播放和故障转移
title: 媒体播放和故障转移
uuid: 197a6ee0-f1ff-40ac-bd49-eafeae6167d4
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---


# 媒体播放和故障转移{#media-playback-and-failover}

对于实时和视频点播(VOD)媒体，TVSDK通过下载与中分辨率比特率相关的播放列表来开始播放，并下载由该播放列表定义的媒体段。 它快速选择高分辨率比特率的播放列表及其相关媒体并继续下载过程。

## 缺少播放列表故障转移{#section_E6B6A15930894F56A0A8501577B35E7F}

如果缺少整个播放列表，例如，当顶级清单文件中指定的M3U8文件不下载时，TVSDK会尝试恢复。 如果无法恢复，则由应用程序决定下一步。

如果缺少与中分辨率比特率关联的播放列表，则TVSDK将以相同分辨率搜索变体播放列表。 如果找到相同的分辨率，则开始从匹配位置下载变体播放列表和区段。 如果TVSDK找不到相同的分辨率播放列表，它将尝试循环播放其他比特率播放列表及其变体。 立即降低比特率是首选，然后是其变体，依此类推。 如果在尝试查找有效的播放列表时，所有较低比特率的播放列表及其变体都已用尽，则TVSDK将转到最高比特率，并从那里向下计数。 如果找不到有效的播放列表，则进程将失败，并且播放器将移至ERROR状态。

您的应用程序可以确定如何处理这种情况。 例如，您可能希望关闭播放器活动并将用户定向到目录活动。 感兴趣的事件是`STATUS_CHANGED`事件，相应的回调是`onStatusChange`方法。 以下代码监视播放器是否将其内部状态更改为ERROR:

有关详细信息，请参阅`PSDKDemo`文件。 事件监听器已附加到MediaPlayer实例。

```
case MediaPlayerStatus.ERROR: 
Alert.show(event.error.toString(), “Error occurred”); 
break;
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

## 缺少段故障转移{#section_ED8CF666289042D39E9914D42BDD9BA4}

当缺少区段时（例如，当特定区段无法下载时）,TVSDK会尝试通过各种故障转移尝试进行恢复。 如果它无法恢复，则会出错。

如果服务器上缺少区段，例如，清单文件不存在，区段无法下载，等等，TVSDK会尝试通过尝试以下选项来失败：

1. 尝试在变体文件中以相同比特率向同一段进行故障转移。
1. 在同一文件中切换到备用比特率（ABR开关）。
1. 循环查看每个可用变体中的每个可用位速率。
1. 跳过段并发出警告。

当TVSDK无法获取替代段时，它会触发`CONTENT_ERROR`错误通知。 此通知包含代码为`DOWNLOAD_ERROR`的内部通知。 如果存在问题的流是备用音轨，TVSDK将生成`AUDIO_TRACK_ERROR`错误通知。

如果视频引擎连续无法获取区段，它会将连续区段跳转限制为5，然后停止播放，TVSDK将对代码5发出`NATIVE_ERROR`。

>[!NOTE]
>
>在发生故障转移时，不考虑自适应比特率(ABR)控制参数。 这是因为故障转移机制设计为将任何当前可用的播放列表用作备份流，而不管其比特率用户档案如何。
>
>在故障转移操作期间，可以有用户档案交换机。 如果在下载其中一个播放列表段期间发生错误，则忽略ABR控制参数，如最小／最大允许比特率。

