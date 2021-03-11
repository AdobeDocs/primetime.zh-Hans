---
description: 在您可以使用大多数浏览器TVSDK播放器方法之前，播放器必须处于有效状态。
title: 等待有效状态
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---


# 等待有效状态{#wait-for-a-valid-state}

在您可以使用大多数浏览器TVSDK播放器方法之前，播放器必须处于有效状态。

玩家在各种状态中移动。 等待播放器处于正确状态可确保媒体资源已成功加载。 如果播放器不处于至少所需的状态，则许多播放器方法会抛出`IllegalStateException`。

所需的状态通常为PREPARED。

1. 要确认该状态为PREPARED:

   播放器初始化时，请等待浏览器TVSDK以`event.status`的`MediaPlayerStatus.PREPARED`调度`AdobePSDK.MediaPlayerStatusChangeEvent`事件。

   检查MediaPlayer对象的当前状态是否至少为PREPARED。

   ```
   <readonly> status :AdobePSDK.MediaPlayerStatus
   ```

