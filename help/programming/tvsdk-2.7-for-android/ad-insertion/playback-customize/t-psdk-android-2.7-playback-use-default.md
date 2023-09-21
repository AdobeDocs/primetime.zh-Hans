---
description: 您可以选择使用默认广告行为。
title: 使用默认播放行为
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 使用默认播放行为  {#use-the-default-playback-behavior}

您可以选择使用默认广告行为。

1. 要使用默认行为，请完成以下任务之一：

   * 如果您实施自己的 `AdvertisingFactory` 类，返回null `createAdPolicySelector`.

   * 如果您没有针对的自定义实施 `AdvertisingFactory` 类，TVSDK使用默认的ad策略选择器。

## 设置自定义播放 {#set-up-customized-playback}

您可以自定义或覆盖广告行为。

在自定义或覆盖广告行为之前，请使用TVSDK注册广告策略实例。

* 实施 `AdPolicySelector` 接口及其所有方法。

  如果需要覆盖，则建议使用此选项 **所有** 默认广告行为。

* 扩展 `DefaultAdPolicySelector` 类，并仅为那些需要自定义的行为提供实现。

  如果您只需要覆盖，则建议使用此选项 **部分** 缺省行为的URL值。

要自定义广告行为，请执行以下操作：

1. 实施 `AdPolicySelector` 接口及其所有方法。
1. 通过广告工厂分配TVSDK要使用的策略实例。

   >[!NOTE]
   >
   >在播放开始时注册的自定义广告策略在以下情况下清除： `MediaPlayer` 实例已取消分配。 每次创建新播放会话时，您的应用程序都必须注册一个策略选择器实例。

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

1. 实施您的自定义项。
