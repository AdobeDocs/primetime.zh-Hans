---
description: 从创建MediaPlayer实例到终止实例的那一刻起，此实例将从一个状态过渡到下一个状态。
title: MediaPlayer对象的生命周期和状态
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# MediaPlayer对象的生命周期和状态{#life-cycle-and-states-of-the-mediaplayer-object}

从创建MediaPlayer实例到终止实例的那一刻起，此实例将从一个状态过渡到下一个状态。

以下是可能的状态：

* **空闲**:  `MediaPlayerStatus.IDLE`

* **初始化**:  `MediaPlayerStatus.INITIALIZING`

* **初始化**:  `MediaPlayerStatus.INITIALIZED`

* **准备**:  `MediaPlayerStatus.PREPARING`

* **准备**:  `MediaPlayerStatus.PREPARED`

* **播放**:  `MediaPlayerStatus.PLAYING`

* **暂停**:  `MediaPlayerStatus.PAUSED`

* **搜索**:  `MediaPlayerStatus.SEEKING`

* **完成**:  `MediaPlayerStatus.COMPLETE`

* **错误**:  `MediaPlayerStatus.ERROR`

* **已发布**:  `MediaPlayerStatus.RELEASED`

状态的完整列表在`MediaPlayerStatus`中定义。

了解玩家的状态很有用，因为只有当玩家处于特定状态时，才允许某些操作。 例如，在IDLE状态下无法调用`play`。 必须在到达准备状态后发出呼吁。 ERROR状态还会更改接下来可能发生的情况。

加载和播放媒体资源时，播放器会按以下方式过渡:

1. 初始状态为IDLE。
1. 应用程序调用`MediaPlayer.replaceCurrentResource`，将播放器移动到INITIALIZING状态。
1. 如果浏览器TVSDK成功加载资源，则状态将更改为INITIALIZED。
1. 您的应用程序调用`MediaPlayer.prepareToPlay`，并且状态更改为PREPARING。
1. 浏览器TVSDK准备媒体流，并开始广告解析和广告插入（如果启用）。

   完成此步骤后，将在时间轴中插入广告或广告过程失败，且播放器状态更改为PREPARED。
1. 当应用程序播放和暂停媒体时，状态在播放和暂停之间移动。

   >[!TIP]
   >
   >播放或暂停时，当您导航离开播放、关闭设备或切换应用程序时，状态变化为SUSPENDED并释放资源。 要继续，请恢复媒体播放器。

1. 当播放器到达流的末尾时，状态变为COMPLETE。
1. 应用程序释放媒体播放器时，状态将更改为“已释放”。
1. 如果进程期间发生错误，则状态将更改为ERROR。

以下是MediaPlayer实例的生命周期的插图：

<!--<a id="fig_DD3DAE7507C549C8A4720A26DFCFFCCB"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

您可以使用状态向用户提供有关该过程的反馈（例如，在等待下一个状态更改时使用微调框）或在播放媒体时采取后续步骤，例如在调用下一个方法之前等待适当的状态。

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

