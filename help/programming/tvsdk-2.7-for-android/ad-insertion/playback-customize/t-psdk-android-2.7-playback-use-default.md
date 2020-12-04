---
description: 您可以选择使用默认广告行为。
seo-description: 您可以选择使用默认广告行为。
seo-title: 使用默认播放行为
title: 使用默认播放行为
uuid: 20785251-eb2f-4cc0-b919-1a88c0b1c57c
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---


# 使用默认播放行为{#use-the-default-playback-behavior}

您可以选择使用默认广告行为。

1. 要使用默认行为，请完成以下任务之一：

   * 如果实现自己的`AdvertisingFactory`类，则为`createAdPolicySelector`返回null。

   * 如果您没有`AdvertisingFactory`类的自定义实现，TVSDK将使用默认的广告策略选择器。

## 设置自定义播放{#set-up-customized-playback}

您可以自定义或覆盖广告行为。

在自定义或覆盖广告行为之前，请向TVSDK注册广告策略实例。

* 实现`AdPolicySelector`接口及其所有方法。

   如果需要覆盖&#x200B;**all**&#x200B;默认广告行为，则建议使用此选项。

* 扩展`DefaultAdPolicySelector`类并仅为那些需要自定义的行为提供实现。

   如果只需要覆盖默认行为的&#x200B;**某些**，则建议使用此选项。

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