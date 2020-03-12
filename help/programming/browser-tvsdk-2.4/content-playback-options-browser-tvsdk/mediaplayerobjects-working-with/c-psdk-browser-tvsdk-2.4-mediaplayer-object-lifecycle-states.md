---
description: 从创建MediaPlayer实例到终止实例，该实例从一个状态过渡到下一个状态。
seo-description: 从创建MediaPlayer实例到终止实例，该实例从一个状态过渡到下一个状态。
seo-title: MediaPlayer对象的生命周期和状态
title: MediaPlayer对象的生命周期和状态
uuid: fe76ea80-aaa8-43bc-9b81-85e0551f70dd
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# MediaPlayer对象的生命周期和状态{#life-cycle-and-states-of-the-mediaplayer-object}

从创建MediaPlayer实例到终止实例，该实例从一个状态过渡到下一个状态。

以下是可能的状态：

* **空闲**: `MediaPlayerStatus.IDLE`

* **初始化**: `MediaPlayerStatus.INITIALIZING`

* **已初始化**: `MediaPlayerStatus.INITIALIZED`

* **准备**: `MediaPlayerStatus.PREPARING`

* **准备**: `MediaPlayerStatus.PREPARED`

* **播放**: `MediaPlayerStatus.PLAYING`

* **暂停**: `MediaPlayerStatus.PAUSED`

* **搜索**: `MediaPlayerStatus.SEEKING`

* **完成**: `MediaPlayerStatus.COMPLETE`

* **错误**: `MediaPlayerStatus.ERROR`

* **发布**: `MediaPlayerStatus.RELEASED`

状态的完整列表在中定义 `MediaPlayerStatus`。

了解玩家的状态很有用，因为某些操作仅在玩家处于特定状态时才允许。 例如， `play` 在IDLE状态中无法调用。 必须在达到准备状态后才能进行。 ERROR状态还会更改接下来可能发生的情况。

在加载和播放媒体资源时，播放器会通过以下方式过渡：

1. 初始状态为IDLE。
1. 应用程序调 `MediaPlayer.replaceCurrentResource`用，它将播放器移至INITIALIZING状态。
1. 如果浏览器TVSDK成功加载资源，则状态将更改为INITIALIZED。
1. 应用程序调 `MediaPlayer.prepareToPlay`用后，状态将更改为PREPARING。
1. 浏览器TVSDK准备媒体流并启动广告解析和广告插入（如果启用）。

   当此步骤完成时，广告会插入时间轴或广告过程失败，且播放器状态会更改为PREPARED。
1. 当应用程序播放和暂停媒体时，状态在播放和暂停之间移动。

   >[!TIP]
   >
   >播放或暂停时，当您从播放中导航离开、关闭设备或切换应用程序时，状态将变为SUSPENDED并释放资源。 要继续，请恢复媒体播放器。

1. 当播放器到达流末尾时，状态变为COMPLETE。
1. 当应用程序释放媒体播放器时，状态将变为“已发布”。
1. 如果进程中发生错误，则状态将变为ERROR。

以下是MediaPlayer实例生命周期的图示：

<!--<a id="fig_DD3DAE7507C549C8A4720A26DFCFFCCB"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

您可以使用状态向用户提供进程反馈（例如，等待下一状态更改时的微调框）或在播放媒体时采取后续步骤，如在调用下一个方法之前等待适当的状态。

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

