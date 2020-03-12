---
description: 对于实时和VOD媒体，浏览器TVSDK通过下载与中分辨率比特率相关联的播放列表，然后下载由播放列表定义的中分辨率比特率媒体的段来开始播放。
seo-description: 对于实时和VOD媒体，浏览器TVSDK通过下载与中分辨率比特率相关联的播放列表，然后下载由播放列表定义的中分辨率比特率媒体的段来开始播放。
seo-title: 媒体播放
title: 媒体播放
uuid: 454f84fe-8077-4f37-8e62-1d6ba0fcde27
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 媒体播放 {#media-playback}

对于实时和VOD媒体，浏览器TVSDK通过下载与中分辨率比特率相关联的播放列表，然后下载由播放列表定义的中分辨率比特率媒体的段来开始播放。

浏览器TVSDK快速选择高分辨率比特率播放列表及其相关媒体并继续下载过程。

## 缺少播放列表故障转移 {#section_81A5822C108449E1A0E94A6E25DE9E8E}

例如，当缺少整个播放列表时（例如，在顶级清单文件中指定的M3U8文件不下载时）,Browser TVSDK会尝试恢复。 如果无法恢复，则应用程序将决定下一步。

如果缺少与中间分辨率位速率关联的播放列表，则Browser TVSDK将搜索以相同分辨率的变体播放列表。 如果它找到相同的分辨率，则开始从匹配位置下载变体播放列表和段。 如果Browser TVSDK找不到相同的分辨率播放列表，它将尝试循环播放其他比特率播放列表及其变体。 立即降低的比特率是第一个选择，然后是其变体，依此类推。 如果在尝试查找有效的播放列表时所有较低比特率的播放列表及其变体都已用尽，则浏览器TVSDK将转到最高比特率，并从那里向下计数。 如果找不到有效的播放列表，则进程将失败，并且播放器将移至ERROR状态。

您的应用程序可以确定如何处理这种情况。 例如，您可能希望关闭播放器活动并将用户定向到目录活动。 感兴趣的事件是状态或状态更改事件，相应的回调是状态更改的方法。 以下代码监视播放器是否将其内部状态更改为ERROR:

```js
case AdobePSDK.MediaPlayerStatus.ERROR:  
var errorDesc = event.metadata.getValue('DESCRIPTION'); 
console.log(errorDesc); 
break; 
```
