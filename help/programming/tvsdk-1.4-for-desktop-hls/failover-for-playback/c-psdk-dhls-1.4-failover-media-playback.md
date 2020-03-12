---
description: 对于实时和视频点播(VOD)媒体，TVSDK通过下载与中分辨率比特率相关联的播放列表开始播放并下载由该播放列表定义的媒体段。 它快速选择高分辨率比特率播放列表及其相关媒体并继续下载过程。
seo-description: 对于实时和视频点播(VOD)媒体，TVSDK通过下载与中分辨率比特率相关联的播放列表开始播放并下载由该播放列表定义的媒体段。 它快速选择高分辨率比特率播放列表及其相关媒体并继续下载过程。
seo-title: 媒体播放和故障转移
title: 媒体播放和故障转移
uuid: 197a6ee0-f1ff-40ac-bd49-eafeae6167d4
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 媒体播放和故障转移{#media-playback-and-failover}

对于实时和视频点播(VOD)媒体，TVSDK通过下载与中分辨率比特率相关联的播放列表开始播放并下载由该播放列表定义的媒体段。 它快速选择高分辨率比特率播放列表及其相关媒体并继续下载过程。

## 缺少播放列表故障转移 {#section_E6B6A15930894F56A0A8501577B35E7F}

例如，当缺少整个播放列表时，如果顶级清单文件中指定的M3U8文件不下载，TVSDK将尝试恢复。 如果无法恢复，则应用程序将决定下一步。

如果缺少与中间分辨率比特率关联的播放列表，则TVSDK将搜索以相同分辨率的变体播放列表。 如果它找到相同的分辨率，则开始从匹配位置下载变体播放列表和段。 如果TVSDK找不到相同的分辨率播放列表，它将尝试循环播放其他比特率播放列表及其变体。 立即降低的比特率是第一个选择，然后是其变体，依此类推。 如果在尝试查找有效的播放列表时所有较低比特率的播放列表及其变体都已用尽，TVSDK将转到最高比特率并从那里向下计数。 如果找不到有效的播放列表，则进程将失败，并且播放器将移至ERROR状态。

您的应用程序可以确定如何处理这种情况。 例如，您可能希望关闭播放器活动并将用户定向到目录活动。 感兴趣的事件是事 `STATUS_CHANGED` 件，相应的回调是方 `onStatusChange` 法。 以下代码监视播放器是否将其内部状态更改为ERROR:

有关详细信息，请参阅 `PSDKDemo` 文件。 事件监听器已附加到MediaPlayer实例。

```
case MediaPlayerStatus.ERROR: 
Alert.show(event.error.toString(), “Error occurred”); 
break;
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

## 缺少细分故障转移 {#section_ED8CF666289042D39E9914D42BDD9BA4}

当某个区段缺失时（例如，当某个特定区段无法下载时）,TVSDK会尝试通过各种故障转移尝试进行恢复。 如果它无法恢复，则会发出错误。

如果因为（例如，清单文件不存在）、区段无法下载等原因导致服务器上缺少区段，TVSDK会尝试通过以下选项来失败：

1. 尝试在变体文件中以相同位速率故障转移到同一段。
1. 在同一文件中切换到备用位速率（ABR开关）。
1. 循环查看每个可用变体中的每个可用位速率。
1. 跳过区段并发出警告。

当TVSDK无法获取替代段时，它会触发错误 `CONTENT_ERROR` 通知。 此通知包含包含代码的内部通 `DOWNLOAD_ERROR` 知。 如果存在问题的流是替代音轨，则TVSDK会生成错误 `AUDIO_TRACK_ERROR` 通知。

如果视频引擎连续无法获取区段，则会将连续区段跳转限制为5，然后停止播放，TVSDK会发出代 `NATIVE_ERROR` 码5的问题。

>[!NOTE]
>
>当故障转移发生时，不考虑自适应比特率(ABR)控制参数。 这是因为故障转移机制设计为将任何当前可用的播放列表用作备份流，而不管其比特率配置文件如何。
>
>在故障转移操作过程中，可以有一个配置文件交换机。 如果在下载其中一个播放列表段期间发生错误，则忽略ABR控制参数，如最小／最大允许位速率。

