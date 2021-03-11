---
description: 在使用MediaPlayer视图播放视频后，您可以使用TVSDK方法或手动隐藏视频并再次显示它。
title: 隐藏视频视图
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 1%

---


# 隐藏视频视图{#hide-a-video-view}

在使用MediaPlayer视图播放视频后，您可以使用TVSDK方法或手动隐藏视频并再次显示它。

您必须先暂停视频，然后清除该视频或将其从显示屏中移动。
* 选项1:用`MediaPlayer.clearVideo`清除视频帧，&#x200B;稍后替换该帧。
   * 暂停要隐藏的视频。
   * 通过调用`MediaPlayer.clearVideo`删除显示的视频帧。
   * 要重置`MediaPlayer`以便再次播放，请调用`replaceCurrentResource`或`replaceCurrentItem`。
* 选项2:将`MediaPlayer`视图从屏幕上移开，稍后再移回，无需替换它。
   * 暂停要隐藏的视频。
   * 将视图移出舞台。 例如：

      ```
      view.x = -300; 
      view.y = -300;
      ```

   * 要再次显示视图，请将视频移回舞台。
