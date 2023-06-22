---
description: 您可以选择使用默认广告行为。
title: 使用默认播放行为
exl-id: 0ea3d2bb-b4d4-4090-ab5f-b6c31c1abe32
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# 使用默认播放行为 {#use-the-default-playback-behavior}

您可以选择使用默认广告行为。

1. 要使用默认行为，请完成以下任务之一：

   * 如果您实施自己的 `AdvertisingFactory` 类，返回null `createAdPolicySelector`.

   * 如果您没有的自定义实施 `AdvertisingFactory` 类，TVSDK使用默认广告策略选择器。

## 设置自定义播放 {#set-up-customized-playback}

您可以自定义或覆盖广告行为。

在自定义或覆盖广告行为之前，请先使用注册广告策略实例。
要自定义广告行为，请执行以下操作之一：

* 实施 `AdPolicySelector` 接口及其所有方法。

   如果需要覆盖，建议使用此选项 **所有** 默认广告行为。

* 扩展 `DefaultAdPolicySelector` 类，并仅为那些需要自定义的行为提供实现。

   如果您只需要覆盖，则建议使用此选项 **部分** 缺省行为的URL值。

要自定义广告行为，请执行以下操作：

1. 实施 `AdPolicySelector` 接口及其所有方法。
1. 通过广告工厂分配TVSDK要使用的策略实例。

   >[!NOTE]
   >
   >类CustomContentFactory扩展ContentFactory &amp;lbrace；
   >...
   >@Override
   >公共AdPolicySelector retrieveAdPolicySelector>>(MediaPlayerItem mediaPlayerItem) &amp;lbrace；
   >返回新的CustomAdPolicySelector(mediaPlayerItem)；
   >大括号(&amp;R)；
   >...
   >大括号(&amp;R)；
   >//向媒体播放器注册自定义内容工厂
   >MediaPlayerItemConfig =新MediaPlayerItemConfig()；
   >config.setAdvertisingFactory(new CustomContentFactory())；
   >//加载资源时，稍后应传递此配置
   >mediaPlayer.replaceCurrentResource(resource， config)；

1. 实施您的自定义项。
