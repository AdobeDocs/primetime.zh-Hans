---
description: 对于实时和视频点播(VOD)媒体，TVSDK通过下载与中分辨率比特率关联的播放列表来开始播放，并下载由该播放列表定义的媒体区段。 它快速选择高分辨率的比特率播放列表及其相关介质，并继续下载过程。
title: 媒体播放和故障切换
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# 媒体播放和故障切换{#media-playback-and-failover}

对于实时和视频点播(VOD)媒体，TVSDK通过下载与中分辨率比特率关联的播放列表来开始播放，并下载由该播放列表定义的媒体区段。 它快速选择高分辨率的比特率播放列表及其相关介质，并继续下载过程。

## 缺少播放列表故障转移 {#section_E6B6A15930894F56A0A8501577B35E7F}

当整个播放列表丢失时，例如当在顶级清单文件中指定的M3U8文件未下载时，TVSDK将尝试恢复。 如果无法恢复，应用程序将决定下一步。

如果缺少与中间分辨率比特率关联的播放列表，则TVSDK将搜索具有相同分辨率的变体播放列表。 如果找到相同分辨率，则开始从匹配位置下载变体播放列表和区段。 如果TVSDK未找到相同分辨率的播放列表，它将尝试循环查看其他比特率播放列表及其变体。 立即降低的比特率是首选，然后是它的变体，依此类推。 如果尝试查找有效播放列表时所有较低比特率的播放列表及其变体已耗尽，则TVSDK将转到最高比特率并从此处开始计数。 如果找不到有效的播放列表，此过程将失败，并且播放器会变为ERROR状态。

您的应用程序可以决定如何处理这种情况。 例如，您可能需要关闭播放器活动并将用户定向到目录活动。 感兴趣的事件是 `STATUS_CHANGED` 事件，相应的回调为 `onStatusChange` 方法。 以下代码用于监视播放器是否将其内部状态更改为“错误”：

欲了解更多信息，请参见 `PSDKDemo` 文件。 事件侦听器附加到MediaPlayer实例。

```
case MediaPlayerStatus.ERROR: 
Alert.show(event.error.toString(), “Error occurred”); 
break;
```

如果客户端网络已关闭，您可以使用此代码进行验证。

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

API将提供用于验证客户端网络是否关闭的URL。 这应为有效的URL，它将在http请求上返回http响应代码200。

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

如果未设置setNetworkDownVerificationUrl，则TVSDK默认使用MainManifest URL来判断网络是否已关闭。

## 缺少区段故障转移 {#section_ED8CF666289042D39E9914D42BDD9BA4}

当缺少某个区段时，例如当某个特定区段下载失败时，TVSDK会尝试通过各种故障转移尝试进行恢复。 如果无法恢复，则会发出错误。

如果服务器上缺少区段，例如，由于清单文件不存在、无法下载区段等，TVSDK将尝试通过尝试以下选项进行故障转移：

1. 尝试在变量文件中以相同的比特率故障转移到同一段。
1. 在同一文件中切换到备用比特率（ABR交换机）。
1. 在每个可用变量中循环访问每个可用比特率。
1. 跳过该区段并发出警告。

当TVSDK无法获取替代区段时，它会触发 `CONTENT_ERROR` 错误通知。 此通知包含带有代码的内部通知 `DOWNLOAD_ERROR` 代码。 如果存在问题的流是备用音轨，TVSDK将生成 `AUDIO_TRACK_ERROR` 错误通知。

如果视频引擎连续无法获取区段，则会将连续区段跳过限制为5，之后播放将停止，并且TVSDK会发出 `NATIVE_ERROR` 代码为5。

>[!NOTE]
>
>在发生故障转移时，不会考虑自适应比特率(ABR)控制参数。 这是因为故障转移机制设计为将任何当前可用的播放列表（无论其比特率配置文件如何）用作备份流。
>
>在故障切换操作期间，可以有一个配置文件交换机。 如果在下载其中一个播放列表段期间发生错误，则会忽略ABR控制参数，例如最小/最大允许比特率。
