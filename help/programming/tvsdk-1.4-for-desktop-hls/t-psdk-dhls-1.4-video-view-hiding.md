---
description: 在使用MediaPlayer视图播放视频后，您可以隐藏视频，然后使用TVSDK方法或手动再次显示它。
seo-description: 在使用MediaPlayer视图播放视频后，您可以隐藏视频，然后使用TVSDK方法或手动再次显示它。
seo-title: 隐藏视频视图
title: 隐藏视频视图
uuid: 7cc02bf4-41ee-4af0-98ba-df070b50b88d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 隐藏视频视图{#hide-a-video-view}

在使用MediaPlayer视图播放视频后，您可以隐藏视频，然后使用TVSDK方法或手动再次显示它。

您必须先暂停视频，然后清除视频或将其从显示屏中移动。
* 选项1:用清除视频帧， `MediaPlayer.clearVideo`稍后替&#x200B;换该帧。
   * 暂停要隐藏的视频。
   * 通过调用删除显示的视频帧 `MediaPlayer.clearVideo`。
   * 要重置 `MediaPlayer` 以便再次播放，请拨叫 `replaceCurrentResource` 或 `replaceCurrentItem`。
* 选项2:将视图 `MediaPlayer` 从屏幕上移开，稍后再移回它，无需替换它。
   * 暂停要隐藏的视频。
   * 将视图移出舞台。 例如：

      ```
      view.x = -300; 
      view.y = -300;
      ```

   * 要再次显示视频，请将视图移回舞台。
