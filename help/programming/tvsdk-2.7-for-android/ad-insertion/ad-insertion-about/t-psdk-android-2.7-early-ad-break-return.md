---
description: 对于实时流广告插入，您可能需要先退出广告中断，然后再播放中断中的所有广告以完成。
title: 实施提前广告分时段退货
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 2%

---


# 实施早期广告中断返回{#implement-an-early-ad-break-return}

对于实时流广告插入，您可能需要先退出广告中断，然后再播放中断中的所有广告以完成。

例如，在某些体育事件中，广告中断的持续时间在中断开始之前可能不为人知。 TVSDK提供默认持续时间，但如果游戏在中断结束前恢复，则必须退出广告中断。 另一个示例是实时流中广告中断期间的紧急信号。

1. 订阅`#EXT-X-CUE-OUT`、`#EXT-X-CUE-IN`和`#EXT-X-CUE`，它们是标记中的splice out/splice。

   有关如何拼接广告标记的详细信息，请参阅[机会生成器和内容解析器](../../ad-insertion/content-resolver/c-psdk-android-2.7-content-resolver-about.md)。

1. 使用自定义`ContentFactory`。
1. 在`retrieveGenerators`中，使用`SpliceInPlacementOpportunityGenerator`。

   例如：

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   有关使用自定义`ContentFactory`的详细信息，请参见[实施自定义机会gerenator](../../ad-insertion/content-resolver/t-psdk-android-2.7-opp-detector-impl-android.md)中的步骤1。

1. 在同一个自定义`ContentFactory`上，实现`retrieveResolvers`并包括`AuditudeResolver`和`SpliceInCustomResolver`。

   例如：

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```

