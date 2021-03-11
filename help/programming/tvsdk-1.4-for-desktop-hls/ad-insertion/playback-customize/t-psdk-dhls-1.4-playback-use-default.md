---
description: 您可以选择使用默认广告行为。
title: 使用默认播放行为
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 0%

---


# 使用默认播放行为{#use-the-default-playback-behavior}

您可以选择使用默认广告行为。

要使用默认行为：

* 如果实现自己的`ContentFactory`类，则在`doRetrieveAdPolicySelector`的实现中返回一个新的`DefaultAdPolicySelector`实例。

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

* 如果您没有`ContentFactory`类的自定义实现，TVSDK将使用`DefaultAdPolicySelector`。