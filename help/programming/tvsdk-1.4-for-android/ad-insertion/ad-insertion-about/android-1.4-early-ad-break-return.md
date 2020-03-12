---
description: 对于实时流广告插入，您可能需要退出广告中断，然后才能播放中断中的所有广告，直到完成。
seo-description: 对于实时流广告插入，您可能需要退出广告中断，然后才能播放中断中的所有广告，直到完成。
seo-title: 实施早期广告分时段退货
title: 实施早期广告分时段退货
uuid: 41b70ee1-290b-4732-899e-32b234ec1d9a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 实施早期广告分时段退货 {#implement-an-early-ad-break-return}

对于实时流广告插入，您可能需要退出广告中断，然后才能播放中断中的所有广告，直到完成。

例如，某些体育赛事中的广告中断的持续时间在中断开始之前可能不知道。 TVSDK提供默认持续时间，但如果游戏在中断结束前恢复，则必须退出广告中断。 另一个示例是实时流中广告中断期间的紧急信号。

1. 订阅剪接／插入广告标记( `#EXT-X-CUE-OUT`、 `#EXT-X-CUE-IN`和 `#EXT-X-CUE`)。

   有关如何拼接广告标记的更多信息，请参阅 [Opportunity生成器和内容解析器](../../../tvsdk-1.4-for-android/content-resolver/android-1.4-content-resolver-about.md)。
1. 使用自定义 `ContentFactory`。
1. 在 `retrieveGenerators()`中，使用 `SpliceInPlacementOpportunityGenerator`。

   例如：

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   有关使用自定义的详细信息， `ContentFactory`请参阅实施自定义机 [会检测器中的步骤1](../../../tvsdk-1.4-for-android/content-resolver/android-1.4-opp-detector-impl.md) 。

1. 在同一个自定义 `ContentFactory`上，实 `retrieveResolvers` 施并包含 `AuditudeResolver` 和 `SpliceInCustomResolver`。

   例如：

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```

