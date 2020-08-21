---
description: 您可以选择使用默认广告行为。
seo-description: 您可以选择使用默认广告行为。
seo-title: 使用默认播放行为
title: 使用默认播放行为
uuid: 36f76c42-4c6c-4620-9b47-ec97519a642a
translation-type: tm+mt
source-git-commit: 6da7d597503d98875735c54e9a794f8171ad408b
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# 使用默认播放行为 {#use-the-default-playback-behavior}

您可以选择使用默认广告行为。

1. 要使用默认行为，请完成以下任务之一：

   * 如果实现自己的 `AdvertisingFactory` 类，则返回null `createAdPolicySelector`。

   * 如果您没有类的自定义实现， `AdvertisingFactory` TVSDK将使用默认的广告策略选择器。

## 设置自定义播放 {#set-up-customized-playback}

您可以自定义或覆盖广告行为。

在自定义或覆盖广告行为之前，请先注册广告策略实例。
要自定义广告行为，请执行下列操作之一：

* 实现接 `AdPolicySelector` 口及其所有方法。

   如果您需要覆盖所有默认广告 **行为** ，建议使用此选项。

* 扩展类 `DefaultAdPolicySelector` 并仅为那些需要自定义的行为提供实现。

   如果只需要覆盖部分默认行 **为** ，建议使用此选项。

自定义广告行为：

1. 实现接 `AdPolicySelector` 口及其所有方法。
1. 指定TVSDK通过广告工厂使用的策略实例。

   >[!NOTE]
   >
   >类CustomContentFactory扩展ContentFactory &amp;lbrace;
   >...
   >@覆盖
   >public AdPolicySelector retrieveAdPolicySelector>>(MediaPlayerItem mediaPlayerItem)&amp;lbrace;
   >返回新的CustomAdPolicySelector(mediaPlayerItem);
   >&amp;rbrace;
   >...
   >&amp;rbrace;
   >//使用媒体播放器注册自定义内容工厂
   >MediaPlayerItemConfig = new MediaPlayerItemConfig();
   >config.setAdvertisingFactory(new CustomContentFactory());
   >//此配置应在加载>资源时稍后传递
   >mediaPlayer.replaceCurrentResource(resource, config);

1. 实施您的自定义。
