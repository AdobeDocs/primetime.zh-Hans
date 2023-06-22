---
description: 您可以选择使用默认广告行为。
title: 使用默认播放行为
exl-id: 8d25e076-4335-49c8-b6b8-f2694b1b9074
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 0%

---

# 使用默认播放行为{#use-the-default-playback-behavior}

您可以选择使用默认广告行为。

要使用默认行为，请执行以下操作：

* 如果您实施自己的 `ContentFactory` 类，返回一个新实例 `DefaultAdPolicySelector` 在您的实施中 `doRetrieveAdPolicySelector`.

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

* 如果您没有的自定义实施 `ContentFactory` 类，TVSDK使用 `DefaultAdPolicySelector`.
