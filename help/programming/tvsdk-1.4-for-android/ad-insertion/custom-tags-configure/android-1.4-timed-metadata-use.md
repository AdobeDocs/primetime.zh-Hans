---
description: 当当前播放时间与开始时间匹配时，可以使用TimedMetadata。
title: 使用定时元数据
exl-id: 7f87cd14-121a-4543-ab0a-a03d829d040b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# 使用定时元数据 {#use-timed-metadata}

当当前播放时间与开始时间匹配时，可以使用TimedMetadata。

要使用这些已保存的内容，请执行以下操作 `TimedMetadata` 播放期间的对象，使用保存的 `ArrayList` 起始日期 [在调度定时元数据对象时存储这些对象](../../ad-insertion/custom-tags-configure/android-1.4-timed-metadata-store.md).

1. 运行计时器并重复查询当前播放时间。
1. 查找所有 `TimedMetadata` 开始时间与当前播放时间匹配的对象。

   您可以使用这些对象完成各种操作。

   >[!IMPORTANT]
   >
   >检查当前播放时间是否与任意播放时间匹配时 `TimedMetadata` 对象，包括 `shouldTriggerSubscribedTagEvent` 作为条件。

   时间轴可能会因各种广告行为而更改。 例如，一个或多个广告时间可能会从它们在时间轴上的原始位置移动，但是 `shouldTriggerSubscribedTagEvent` 确保 `TimeMetadata` 对象的开始时间与当前播放时间匹配。

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

1. 定期刷新陈旧 `TimedMetadata` 防止内存持续增长的实例。
