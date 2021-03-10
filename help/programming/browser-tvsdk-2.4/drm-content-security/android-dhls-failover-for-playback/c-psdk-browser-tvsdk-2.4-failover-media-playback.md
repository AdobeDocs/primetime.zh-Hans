---
description: 对于实时和VOD媒体，浏览器TVSDK通过下载与中分辨率比特率相关联的播放列表，然后下载由播放列表定义的中分辨率比特率媒体的段来播放开始。
title: 媒体播放
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---


# 媒体播放{#media-playback}

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
