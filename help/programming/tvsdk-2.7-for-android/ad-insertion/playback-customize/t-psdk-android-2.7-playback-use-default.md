---
description: 您可以选择使用默认广告行为。
seo-description: 您可以选择使用默认广告行为。
seo-title: 使用默认播放行为
title: 使用默认播放行为
uuid: 20785251-eb2f-4cc0-b919-1a88c0b1c57c
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 使用默认播放行为 {#use-the-default-playback-behavior}

您可以选择使用默认广告行为。

1. 要使用默认行为，请完成以下任务之一：

   * 如果实现自己的类， `AdvertisingFactory` 则为返回null `createAdPolicySelector`。

   * 如果没有类的自定义实现，则TVSDK `AdvertisingFactory` 将使用默认的广告策略选择器。

## 设置自定义播放 {#set-up-customized-playback}

您可以自定义或覆盖广告行为。

在自定义或覆盖广告行为之前，请先向TVSDK注册广告策略实例。

* 实现接 `AdPolicySelector` 口及其所有方法。

   如果您需要覆盖所有默认广告 **行为** ，则建议使用此选项。

* 扩展类 `DefaultAdPolicySelector` 并仅为那些需要自定义的行为提供实现。

   如果只需覆盖部分默认行 **为** ，建议使用此选项。

自定义广告行为：

1. 实现接 `AdPolicySelector` 口及其所有方法。
1. 指定TVSDK通过广告工厂使用的策略实例。

   >[!NOTE]
   >
   >取消分配实例时，将在播放开始时注册的自定义广告策 `MediaPlayer` 略将被清除。 每次创建新的播放会话时，应用程序都必须注册一个策略选择器实例。

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