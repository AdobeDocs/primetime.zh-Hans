---
description: 对于实时流广告插入，您可能需要先从广告时间退出，然后才会播放广告时间中的所有广告直至结束。
title: 实施提前返回广告时间
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---

# 实施提前返回广告时间 {#implement-an-early-ad-break-return}

对于实时流广告插入，您可能需要先从广告时间退出，然后才会播放广告时间中的所有广告直至结束。

例如，某些体育赛事中的广告插播时长可能在插播开始之前未知。 TVSDK提供了默认持续时间，但如果游戏在休息时间结束前恢复，则必须退出广告时间。 另一个示例是在实时流中的广告时间期间的紧急信号。

1. 订阅广告插播/插入标记( `#EXT-X-CUE-OUT`， `#EXT-X-CUE-IN`、和 `#EXT-X-CUE`)。

   有关如何拆分/插入广告标记的详细信息，请参阅 [机会生成器和内容解析器](../../../tvsdk-1.4-for-android/content-resolver/android-1.4-content-resolver-about.md).
1. 使用自定义 `ContentFactory`.
1. 在 `retrieveGenerators()`，使用 `SpliceInPlacementOpportunityGenerator`.

   例如：

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   有关使用自定义的详细信息 `ContentFactory`，请参阅中的步骤1 [实施自定义机会检测器](../../../tvsdk-1.4-for-android/content-resolver/android-1.4-opp-detector-impl.md) .

1. 在同一自定义上 `ContentFactory`，实施 `retrieveResolvers` 并包括 `AuditudeResolver` 和 `SpliceInCustomResolver`.

   例如：

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```
