---
description: TVSDK可以设置多个初始PlacementInformation。
seo-description: TVSDK可以设置多个初始PlacementInformation。
seo-title: 多个初始放置信息
title: 多个初始放置信息
uuid: e0f549d7-3092-45e9-bd67-ee41d01075b5
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 多个初始放置信息{#multiple-initial-placementinformations}

TVSDK可以设置多个初始PlacementInformation。

```java
ArrayList<PlacementInformation> placementInformations = new ArrayList<PlacementInformation>(); 
CustomRangeHelper customRangeHelper = new CustomRangeHelper(mediaPlayerItem.getResource().getMetadata()); 
  
if (customRangeHelper.hasRanges() == null) { 
    if (adSignalingMode == AdSignalingMode.SERVER_MAP) { 
        placementInformations.add(new PlacementInformation(Type.SERVER_MAP, PlacementInformation.UNKNOWN_DURATION, 0)); 
    } else if (adSignalingMode == AdSignalingMode.MANIFEST_CUES) { 
        placementInformations.add(new PlacementInformation(Type.PRE_ROLL, timeMapping.getTime(), PlacementInformation.UNKNOWN_DURATION)); 
    } 
} 
else if (customRangeHelper.hasRanges() == CustomRangeHelper.MARK_RANGE) { 
    placementInformations.add(new PlacementInformation(Type.CUSTOM_TIME_RANGES,  
      PlacementInformation.Mode.MARK, PlacementInformation.UNKNOWN_DURATION, 0)); 
} 
else if (customRangeHelper.hasRanges() == CustomRangeHelper.DELETE_RANGE) { 
    placementInformations.add(new PlacementInformation(Type.CUSTOM_TIME_RANGES,  
      PlacementInformation.Mode.DELETE, PlacementInformation.UNKNOWN_DURATION, 0)); 
    if (adSignalingMode == AdSignalingMode.SERVER_MAP) { 
        placementInformations.add(new PlacementInformation(Type.SERVER_MAP,  
          PlacementInformation.UNKNOWN_DURATION, 0)); 
    } else if (adSignalingMode == AdSignalingMode.MANIFEST_CUES) { 
        placementInformations.add(new PlacementInformation(Type.PRE_ROLL,  
          timeMapping.getTime(), PlacementInformation.UNKNOWN_DURATION)); 
    } 
} 
else if (customRangeHelper.hasRanges() == CustomRangeHelper.REPLACE_RANGE) { 
    placementInformations.add(new PlacementInformation(Type.CUSTOM_TIME_RANGES,  
      PlacementInformation.Mode.DELETE, PlacementInformation.UNKNOWN_DURATION, 0)); 
    placementInformations.add(new PlacementInformation(Type.CUSTOM_TIME_RANGES,  
      PlacementInformation.Mode.REPLACE, PlacementInformation.UNKNOWN_DURATION, 0)); 
} 
return  placementInformations;
```

