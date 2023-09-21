---
description: 在当前播放时间与开始时间匹配时，可以使用TimedMetadata。
title: 使用定时元数据
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# 使用定时元数据 {#use-timed-metadata}

在当前播放时间与开始时间匹配时，可以使用TimedMetadata。

要使用这些已保存的 `TimedMetadata` 播放期间的对象，使用保存的 `ArrayList` 从 [在调度定时元数据对象时存储这些对象](../../ad-insertion/custom-tags-configure/android-1.4-timed-metadata-store.md).

1. 运行计时器并重复查询当前播放时间。
1. 查找所有 `TimedMetadata` 开始时间与当前播放时间匹配的对象。

   您可以使用这些对象完成各种操作。

   >[!IMPORTANT]
   >
   >检查当前播放时间是否与任意播放时间匹配时 `TimedMetadata` 对象，包括 `shouldTriggerSubscribedTagEvent` 作为条件。

   时间线可能会因各种广告行为而更改。 例如，一个或多个广告时间可能会从它们在时间轴上的原始位置移动，但是 `shouldTriggerSubscribedTagEvent` 确保 `TimeMetadata` 对象的开始时间与当前播放时间匹配。

   例如：

   ```java
    _playbackClockEventListener = new Clock.ClockEventListener() {
       @Override
       public void onTick(String name) {
           getActivity().runOnUiThread(new Runnable() {
               @Override
               public void run() {
                   /* handle timedmetadata object list  */ 
                   if (_mediaPlayer != null && _timedMetadataList != null && _timedMetadataList.size() > 0) {
                       if (_lastKnownStatus == MediaPlayer.PlayerState.PLAYING) {
                           long localTime = _mediaPlayer.getLocalTime();
                           Iterator<TimedMetadata> iterator = _timedMetadataList.iterator(); 
                           while (iterator.hasNext()) {
                               TimedMetadata timedMetadata = iterator.next();
                               long diff = localTime - timedMetadata.getTime();
                               if (diff >= 0 &&
                                   diff <= PLAYBACK_CLOCK_INTERVAL &&
                                   _mediaPlayer.shouldTriggerSubscribedTagEvent()) {
                                   // use timed metadata object
                               }
                           }
                       }
                   }
               }
           });
       }
   };
   _playbackClock.addClockEventListener(_playbackClockEventListener);
   ```

1. 定期刷新过时 `TimedMetadata` 从列表中删除实例，以防止内存持续增长。
