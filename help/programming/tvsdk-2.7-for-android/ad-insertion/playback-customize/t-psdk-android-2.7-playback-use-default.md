---
description: 您可以选择使用默认广告行为。
title: 使用默认播放行为
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# 使用默认播放行为{#use-the-default-playback-behavior}

您可以选择使用默认广告行为。

1. 要使用默认行为，请完成以下任务之一：

   * 如果实现自己的`AdvertisingFactory`类，则为`createAdPolicySelector`返回null。

   * 如果您没有`AdvertisingFactory`类的自定义实现，TVSDK将使用默认的广告策略选择器。

## 设置自定义播放{#set-up-customized-playback}

您可以自定义或覆盖广告行为。

在自定义或覆盖广告行为之前，请使用TVSDK注册广告策略实例。

* 实现`AdPolicySelector`接口及其所有方法。

   如果您需要覆盖&#x200B;**all**&#x200B;默认广告行为，建议使用此选项。

* 扩展`DefaultAdPolicySelector`类并仅为那些需要自定义的行为提供实现。

   如果只需要覆盖默认行为的&#x200B;**some**，则建议使用此选项。

自定义广告行为：

1. 实现`AdPolicySelector`接口及其所有方法。
1. 指定TVSDK通过广告工厂使用的策略实例。

   >[!NOTE]
   >
   >取消分配`MediaPlayer`实例时，将清除在播放开始处注册的自定义广告策略。 每次创建新的播放会话时，应用程序必须注册一个策略选择器实例。

   例如：

   ```java
   class CustomContentFactory extends ContentFactory { 
       ... 
       @Override 
       public AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem mediaPlayerItem) { 
           return new CustomAdPolicySelector(mediaPlayerItem); 
       } 
       ... 
   } 
   
   // register the custom content factory with media player 
   MediaPlayerItemConfig config =  new MediaPlayerItemConfig(); 
   config.setAdvertisingFactory(new CustomContentFactory()); 
   
   // this config will should be later passed while loading the resource 
   mediaPlayer.replaceCurrentResource(resource, config);
   ```

1. 实施您的自定义。