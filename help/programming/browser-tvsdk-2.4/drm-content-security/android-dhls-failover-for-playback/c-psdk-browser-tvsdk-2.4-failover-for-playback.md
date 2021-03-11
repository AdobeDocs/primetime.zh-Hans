---
description: 通过Internet进行流播放需要一个持续稳定的连接才能从远程服务器播放流。 但是，查看器的Internet连接或流播放的可变性意味着远程播放可能无法在本地播放媒体的质量。
title: 播放和故障转移
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---


# 播放和故障转移{#playback-and-failover}

通过Internet进行流播放需要一个持续稳定的连接才能从远程服务器播放流。 但是，查看器的Internet连接或流播放的可变性意味着远程播放可能无法在本地播放媒体的质量。

Primetime无法避免ISP中断或电缆断开等故障。 但是，Primetime流提供故障转移保护，可保护回放免受某些远程服务器故障或操作故障的影响，为观看者提供更好的体验。 浏览器TVSDK实施故障转移保护以最大限度地减少播放中断，并尽管存在传输问题，仍实现无缝播放。 当整个再现或片段不可用时，视频播放器会自动切换到备份媒体集。

## 媒体播放{#media-playback}

对于实时和VOD媒体，浏览器TVSDK通过下载与中分辨率比特率相关联的播放列表，然后下载由播放列表定义的中分辨率比特率媒体的段来播放开始。

浏览器TVSDK快速选择高分辨率比特率的播放列表及其相关媒体并继续下载过程。

## 缺少播放列表故障转移{#section_81A5822C108449E1A0E94A6E25DE9E8E}

当缺少整个播放列表时（例如，在顶级清单文件中指定的M3U8文件不下载时），Browser TVSDK将尝试恢复。 如果无法恢复，则由应用程序决定下一步。

如果缺少与中分辨率位速率关联的播放列表，则Browser TVSDK将搜索相同分辨率的变体播放列表。 如果找到相同的分辨率，则开始从匹配位置下载变体播放列表和区段。 如果Browser TVSDK找不到相同的分辨率播放列表，它将尝试循环播放其他比特率播放列表及其变体。 首先选择的是立即降低的比特率，然后是其变体，依此类推。 如果在尝试查找有效的播放列表时已用尽所有较低比特率的播放列表及其变体，则Browser TVSDK将转到最高比特率，并从那里计数。 如果找不到有效的播放列表，则进程将失败，并且播放器将移动到ERROR状态。

您的应用程序可以确定如何处理这种情况。 例如，您可能希望关闭播放器活动并将用户定向到目录活动。 兴趣事件是状态或状态更改事件，对应的回调是状态更改方法。 以下代码监视播放器是否将其内部状态更改为ERROR:

```js
case AdobePSDK.MediaPlayerStatus.ERROR:  
var errorDesc = event.metadata.getValue('DESCRIPTION'); 
console.log(errorDesc); 
break; 
```
