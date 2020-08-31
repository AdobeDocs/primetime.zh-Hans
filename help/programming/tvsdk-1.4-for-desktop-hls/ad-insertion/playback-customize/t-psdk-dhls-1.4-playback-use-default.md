---
description: 您可以选择使用默认广告行为。
seo-description: 您可以选择使用默认广告行为。
seo-title: 使用默认播放行为
title: 使用默认播放行为
uuid: 7139384c-167a-4cab-816a-c02fb723a5cb
translation-type: tm+mt
source-git-commit: 1985694f99c548284aad6e6b4e070bece230bdf4
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# 使用默认播放行为{#use-the-default-playback-behavior}

您可以选择使用默认广告行为。

要使用默认行为：

* 如果您实现自己 `ContentFactory` 的类，则返回实 `DefaultAdPolicySelector` 现中的新实例 `doRetrieveAdPolicySelector`。

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

* 如果没有类的自定义实现， `ContentFactory` TVSDK将使用 `DefaultAdPolicySelector`。