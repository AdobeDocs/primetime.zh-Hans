---
description: 当当前播放时间与开始时间匹配时，可以使用TimedMetadata。
title: 使用定时元数据
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 1%

---


# 使用定时元数据{#use-timed-metadata}

当当前播放时间与开始时间匹配时，可以使用TimedMetadata。

要在播放期间使用这些保存的`TimedMetadata`对象，请在调度](../../ad-insertion/custom-tags-configure/android-1.4-timed-metadata-store.md)时使用从[存储timed-metadata对象保存的`ArrayList`。

1. 运行计时器并重复查询当前播放时间。
1. 查找所有开始时间与当前播放时间匹配的`TimedMetadata`对象。

   您可以使用这些对象完成各种操作。

   >[!IMPORTANT]
   >
   >检查当前播放时间是否与任何`TimedMetadata`对象匹配时，将`shouldTriggerSubscribedTagEvent`作为条件。

   时间轴可能会因各种广告行为而改变。 例如，一个或多个广告分页可能从其在时间轴上的原始位置移动，但`shouldTriggerSubscribedTagEvent`可确保`TimeMetadata`对象的开始时间与当前播放时间匹配。

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

1. 定期刷新列表中的陈旧`TimedMetadata`实例，以防止内存持续增长。