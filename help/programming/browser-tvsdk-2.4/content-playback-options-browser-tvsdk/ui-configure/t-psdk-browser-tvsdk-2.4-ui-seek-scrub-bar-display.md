---
description: 在浏览器TVSDK中，您可以搜索流中的特定位置（时间）。 流可以是滑动窗口播放列表或视频点播(VOD)内容。
seo-description: 在浏览器TVSDK中，您可以搜索流中的特定位置（时间）。 流可以是滑动窗口播放列表或视频点播(VOD)内容。
seo-title: 使用搜索栏时处理搜索
title: 使用搜索栏时处理搜索
uuid: a7c74141-581f-40a3-9d28-ce56ba56773c
translation-type: tm+mt
source-git-commit: 1985694f99c548284aad6e6b4e070bece230bdf4
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---


# 使用搜索栏{#handle-seek-when-using-the-seek-bar}时处理搜索

在浏览器TVSDK中，您可以搜索流中的特定位置（时间）。 流可以是滑动窗口播放列表或视频点播(VOD)内容。

>[!IMPORTANT]
>
>在实时流中搜索仅允许DVR。

1. 等待浏览器TVSDK处于有效状态进行搜索。

   有效状态包括PREPARED、COMPLETE、PAUSED和PLAYING。 处于有效状态可确保媒体资源已成功加载。 如果播放器未处于有效可搜索状态，则尝试调用以下方法将引发`IllegalStateException`。

   例如，您可以等待浏览器TVSDK以`event.status``AdobePSDK.MediaPlayerStatus.PREPARED`触发`AdobePSDK.MediaPlayerStatusChangeEvent`。

1. 将请求的搜索位置作为参数传递给`MediaPlayer.seek`方法（以毫秒为单位）。

   这会将播放头移动到流中的不同位置。

   >[!TIP]
   >
   >请求的搜索位置可能与实际计算位置不一致。

   ```js
   void seek(long position) throws IllegalStateException;
   ```

1. 等待浏览器TVSDK触发`AdobePSDK.PSDKEventType.SEEK_END`事件，该事件返回该的`actualPosition`属性中调整的位置：

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.SEEK_END, onSeekComplete); 
   onSeekComplete = function (event) {
       // event.actualPosition
   }
   ```

   这很重要，因为搜索后的实际开始位置可能与请求的位置不同。 以下一些规则可能适用：

   * 如果搜索或其他重新定位在广告中断的中间结束或跳过广告中断，则播放行为会受到影响。
   * 您只能在资产的可搜索持续时间内进行搜索。 对于VOD，即从0到资产的持续时间。

1. 对于在上面的示例中创建的搜索栏，请侦听`setPositionChangeListener()`以查看用户何时正在擦洗：

   ```js
   seekBar.setPositionChangeListener(function (pos) { 
                   var range = player.seekableRange; 
                   if (range) { 
                       var duration = range.duration; 
                       var time = duration * pos; // seek bar range is [0,1] 
                       player.seek(time); 
   
                       console.log("seek to " + time + " / " + duration); 
                   } 
   
               }); 
   ```

1. 设置事件监听器回调以在用户的搜索活动中进行更改。

       搜索操作是异步的，因此Browser TVSDK将调度与搜索相关的以下事件:
   
   * `AdobePSDK.PSDKEventType.SEEK_BEGIN` 表示正在开始搜索。
   * `AdobePSDK.PSDKEventType.SEEK_END` 表示搜索成功。
   * `AdobePSDK.PSDKEventType.SEEK_POSITION_ADJUSTED` 以指示媒体播放器已调整由用户提供的搜索位置。

