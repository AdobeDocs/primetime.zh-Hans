---
description: 在使用MediaPlayer视图播放视频后，您可以使用TVSDK方法或手动隐藏该视图并再次显示它。
title: 隐藏视频视图
exl-id: 92354cd3-f0ed-4434-a7af-a3545e0e2460
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# 隐藏视频视图{#hide-a-video-view}

在使用MediaPlayer视图播放视频后，您可以使用TVSDK方法或手动隐藏该视图并再次显示它。

在清除视频或将其从显示区中移动之前，必须暂停视频。
* 选项1：通过清除视频帧 `MediaPlayer.clearVideo`并&#x200B;稍后更换框架。
   * 暂停要隐藏的视频。
   * 通过调用删除显示的视频帧 `MediaPlayer.clearVideo`.
   * 要重置 `MediaPlayer` 以便能再次播放，呼叫 `replaceCurrentResource` 或 `replaceCurrentItem`.
* 选项2：移动 `MediaPlayer` 从屏幕上查看，稍后再移回来，无需更换。
   * 暂停要隐藏的视频。
   * 将视图移出舞台。 例如：

      ```
      view.x = -300; 
      view.y = -300;
      ```

   * 要再次显示视频，请将视图移回舞台。
