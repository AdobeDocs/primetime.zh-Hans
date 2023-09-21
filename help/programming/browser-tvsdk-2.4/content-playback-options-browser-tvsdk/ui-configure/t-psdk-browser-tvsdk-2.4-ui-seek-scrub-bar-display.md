---
description: 在浏览器TVSDK中，您可以搜索流中的特定位置（时间）。 流可以是滑动窗口播放列表或视频点播(VOD)内容。
title: 使用搜寻栏时处理搜寻
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# 使用搜寻栏时处理搜寻{#handle-seek-when-using-the-seek-bar}

在浏览器TVSDK中，您可以搜索流中的特定位置（时间）。 流可以是滑动窗口播放列表或视频点播(VOD)内容。

>[!IMPORTANT]
>
>仅允许在DVR中进行实时流搜寻。

1. 等待浏览器TVSDK处于有效的状态以进行搜寻。

   有效状态为“已准备”、“完成”、“已暂停”和“正在播放”。 处于有效状态可确保媒体资源已成功加载。 如果播放器未处于有效的可搜索状态，则尝试调用以下方法会引发 `IllegalStateException`.

   例如，您可以等待浏览器TVSDK触发  `AdobePSDK.MediaPlayerStatusChangeEvent`  带有 `event.status` 之 `AdobePSDK.MediaPlayerStatus.PREPARED`.

1. 将请求的搜寻位置传递给 `MediaPlayer.seek` 方法作为参数（以毫秒为单位）。

   这会将播放头移动到流中的不同位置。

   >[!TIP]
   >
   >请求的搜寻位置可能与实际计算位置不一致。

   ```js
   void seek(long position) throws IllegalStateException;
   ```

1. 等待浏览器TVSDK触发  `AdobePSDK.PSDKEventType.SEEK_END`  事件，返回在事件的 `actualPosition` 属性：

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.SEEK_END, onSeekComplete); 
   onSeekComplete = function (event) {
       // event.actualPosition
   }
   ```

   这很重要，因为搜寻之后的实际开始位置可能与请求的位置不同。 以下某些规则可能适用：

   * 如果搜寻或其他重新定位在广告时间中间终止或跳过广告时间，则播放行为会受到影响。
   * 您只能按资产的可搜索持续时间进行搜寻。 对于VOD，该值介于0和资产持续时间之间。

1. 对于上面示例中创建的搜索栏，侦听 `setPositionChangeListener()` 要查看用户何时进行清理，请执行以下操作：

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

1. 设置事件侦听器回调以查找用户搜寻活动中的更改。

       搜寻操作是异步执行的，因此浏览器TVSDK会调度这些与搜寻相关的事件：
   
   * `AdobePSDK.PSDKEventType.SEEK_BEGIN` 表示搜寻正在开始。
   * `AdobePSDK.PSDKEventType.SEEK_END` 表示搜寻成功。
   * `AdobePSDK.PSDKEventType.SEEK_POSITION_ADJUSTED` 指示媒体播放器已重新调整用户提供的搜寻位置。
