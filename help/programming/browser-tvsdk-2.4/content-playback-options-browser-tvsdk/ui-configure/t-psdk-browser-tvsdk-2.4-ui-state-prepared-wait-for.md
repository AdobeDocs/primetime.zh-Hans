---
description: 在使用大多数浏览器TVSDK播放器方法之前，播放器必须处于有效状态。
seo-description: 在使用大多数浏览器TVSDK播放器方法之前，播放器必须处于有效状态。
seo-title: 等待有效状态
title: 等待有效状态
uuid: 0add29a8-fbd8-483a-8c99-e4bc6de9e3d3
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---


# 等待有效状态{#wait-for-a-valid-state}

在使用大多数浏览器TVSDK播放器方法之前，播放器必须处于有效状态。

玩家在各种状态中移动。 等待播放器处于正确状态可确保媒体资源已成功加载。 如果播放器至少不处于所需状态，许多播放器方法会抛出`IllegalStateException`。

所需的状态通常为PREPARED。

1. 要确认状态为PREPARED:

   播放器初始化时，请等待浏览器TVSDK以`event.status``MediaPlayerStatus.PREPARED`的形式调度`AdobePSDK.MediaPlayerStatusChangeEvent`事件。

   检查MediaPlayer对象的当前状态是否至少为PREPARED。

   ```
   <readonly> status :AdobePSDK.MediaPlayerStatus
   ```

