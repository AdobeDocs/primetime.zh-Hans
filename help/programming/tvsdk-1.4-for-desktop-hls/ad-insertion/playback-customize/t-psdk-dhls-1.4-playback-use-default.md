---
description: 您可以选择使用默认广告行为。
title: 使用默认播放行为
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 0%

---

# 使用默认播放行为{#use-the-default-playback-behavior}

您可以选择使用默认广告行为。

要使用默认行为，请执行以下操作：

* 如果您实施自己的 `ContentFactory` 类，返回的新实例 `DefaultAdPolicySelector` 在您的实施中 `doRetrieveAdPolicySelector`.

  ```
  public class CustomContentFactory extends ContentFactory { 
  
      //... 
      // your custom code for advertising classes 
      //... 
  
      /** 
       * @inheritDoc 
       */ 
      override protected function  
        doRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector { 
          return new DefaultAdPolicySelector(item); 
      } 
  }
  ```

* 如果您没有针对的自定义实施 `ContentFactory` 类，TVSDK使用 `DefaultAdPolicySelector`.
