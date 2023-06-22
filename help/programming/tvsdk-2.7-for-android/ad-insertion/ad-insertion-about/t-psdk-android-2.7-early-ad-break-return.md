---
description: 对于实时流广告插入，您可能需要先退出广告时间，然后再播放广告时间中的所有广告直至结束。
title: 实施提前返回广告时间
exl-id: 3c61f34f-3587-40c2-b480-4734b4cf9aef
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# 实施提前返回广告时间  {#implement-an-early-ad-break-return}

对于实时流广告插入，您可能需要先退出广告时间，然后再播放广告时间中的所有广告直至结束。

例如，某些体育赛事中的广告插播的持续时间可能在插播开始之前未知。 TVSDK提供了默认持续时间，但如果游戏在休息时间结束前恢复，则必须退出广告时间。 另一个示例是在实时流中的广告时间期间的紧急信号。

1. 订阅 `#EXT-X-CUE-OUT`， `#EXT-X-CUE-IN`、和 `#EXT-X-CUE`，即标记中的剪切/剪切。

   有关如何拼接/插入广告标记的详细信息，请参阅 [机会生成器和内容解析器](../../ad-insertion/content-resolver/c-psdk-android-2.7-content-resolver-about.md).

1. 使用自定义 `ContentFactory`.
1. In `retrieveGenerators`，使用 `SpliceInPlacementOpportunityGenerator`.

   例如：

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   有关使用自定义的详细信息 `ContentFactory`，请参阅中的步骤1 [实施自定义机会生成器](../../ad-insertion/content-resolver/t-psdk-android-2.7-opp-detector-impl-android.md).

1. 在同一自定义上 `ContentFactory`，实施 `retrieveResolvers` 并包括 `AuditudeResolver` 和 `SpliceInCustomResolver`.

   例如：

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```
