---
description: 从创建MediaPlayer实例的那一刻到其终止的那一刻，此实例会从一个状态转换到下一个状态。
title: MediaPlayer对象的生命周期和状态
exl-id: 26cad982-ef85-42fb-aaa7-e5d494088766
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---

# MediaPlayer对象的生命周期和状态{#life-cycle-and-states-of-the-mediaplayer-object}

从创建MediaPlayer实例的那一刻到其终止的那一刻，此实例会从一个状态转换到下一个状态。

下面是可能的状态：

* **空闲**： `MediaPlayerStatus.IDLE`

* **正在初始化**： `MediaPlayerStatus.INITIALIZING`

* **已初始化**： `MediaPlayerStatus.INITIALIZED`

* **正在准备**： `MediaPlayerStatus.PREPARING`

* **已准备**： `MediaPlayerStatus.PREPARED`

* **正在播放**： `MediaPlayerStatus.PLAYING`

* **已暂停**： `MediaPlayerStatus.PAUSED`

* **搜寻**： `MediaPlayerStatus.SEEKING`

* **完成**： `MediaPlayerStatus.COMPLETE`

* **错误**： `MediaPlayerStatus.ERROR`

* **已发布**： `MediaPlayerStatus.RELEASED`

状态的完整列表定义于 `MediaPlayerStatus`.

了解播放器的状态很有用，因为某些操作只有在播放器处于特定状态时才被允许。 例如， `play` 当处于“空闲”状态时，无法调用。 它必须在达到PREPARED状态之后调用。 ERROR状态还会更改后续发生的情况。

加载和播放媒体资源时，播放器会以下列方式过渡：

1. 初始状态为IDLE。
1. 应用程序调用 `MediaPlayer.replaceCurrentResource`，会将播放器移动到INITIALIZING状态。
1. 如果浏览器TVSDK成功加载资源，则状态将更改为INITIALIZED。
1. 应用程序调用 `MediaPlayer.prepareToPlay`，则状态将更改为“正在准备”。
1. 浏览器TVSDK可准备媒体流并启动广告解析和广告插入（如果已启用）。

   完成此步骤后，会在时间轴中插入广告，或者广告过程失败，并且播放器状态将更改为“已准备”。
1. 当应用程序播放和暂停媒体时，状态在“正在播放”和“已暂停”之间移动。

   >[!TIP]
   >
   >在播放或暂停时，当您离开播放、关闭设备或切换应用程序时，状态将更改为“已暂停”，并释放资源。 要继续，请恢复媒体播放器。

1. 当播放器到达流结尾时，状态将变为COMPLETE。
1. 当应用程序释放媒体播放器时，状态将更改为“已发布”。
1. 如果在处理过程中发生错误，则状态将更改为ERROR。

以下是MediaPlayer实例的生命周期插图：

<!--<a id="fig_DD3DAE7507C549C8A4720A26DFCFFCCB"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

您可以使用状态向用户提供对进程的反馈（例如，在等待下一个状态更改时进行微调），或者在播放媒体时执行后续步骤，例如，在调用下一个方法之前等待适当的状态。

例如：

```js
function onStateChanged(state) { 
    switch(state) { 
        // It is recommended that you call prepareToPlay()  
        // after receiving the INITIALIZED state             
        case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
            mediaPlayer.prepareToPlay(); 
            break; 
    } 
} 
```
