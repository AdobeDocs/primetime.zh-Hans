---
description: 在使用大多数浏览器TVSDK播放器方法之前，播放器必须处于有效状态。
seo-description: 在使用大多数浏览器TVSDK播放器方法之前，播放器必须处于有效状态。
seo-title: 等待有效状态
title: 等待有效状态
uuid: 0add29a8-fbd8-483a-8c99-e4bc6de9e3d3
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 等待有效状态 {#wait-for-a-valid-state}

在使用大多数浏览器TVSDK播放器方法之前，播放器必须处于有效状态。

播放器在各种状态中移动。 等待播放器处于正确状态可确保媒体资源已成功加载。 如果播放器不处于至少所需的状态，将引发许多播放器方法 `IllegalStateException`。

所需状态通常为PREPARED。

1. 要确认状态为PREPARED，请执行以下操作：

   播放器初始化时，请等待浏览器TVSDK使用 `AdobePSDK.MediaPlayerStatusChangeEvent` 的事件 `event.status` 调度 `MediaPlayerStatus.PREPARED`。

   检查MediaPlayer对象的当前状态是否至少为PREPARED。

   ```
   <readonly> status :AdobePSDK.MediaPlayerStatus
   ```

