---
description: 在使用MediaPlayer视图播放视频后，您可以使用TVSDK方法或手动隐藏该视图并再次显示。
title: 隐藏视频视图
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# 隐藏视频视图{#hide-a-video-view}

在使用MediaPlayer视图播放视频后，您可以使用TVSDK方法或手动隐藏该视图并再次显示。

在清除视频或将其从显示区中移动之前，必须暂停视频。
* 选项1：通过清除视频帧 `MediaPlayer.clearVideo`并&#x200B;稍后更换框架。
   * 暂停要隐藏的视频。
   * 通过调用删除显示的视频帧 `MediaPlayer.clearVideo`.
   * 要重置 `MediaPlayer` 以便能再次播放，呼叫 `replaceCurrentResource` 或 `replaceCurrentItem`.
* 选项2：移动 `MediaPlayer` 从屏幕中观看，稍后再移回来，无需更换屏幕。
   * 暂停要隐藏的视频。
   * 将视图移出舞台。 例如：

     ```
     view.x = -300; 
     view.y = -300;
     ```

   * 要再次显示视频，请将视图移回舞台。
