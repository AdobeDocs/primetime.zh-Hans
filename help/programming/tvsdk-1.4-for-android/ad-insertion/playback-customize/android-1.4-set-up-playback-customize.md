---
description: 您可以自定义或覆盖广告行为。
title: 设置自定义播放
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# 设置自定义播放 {#cset-up-customized-playback}

您可以通过在TVSDK中注册广告策略实例来自定义或覆盖广告行为。

要自定义广告行为，请执行以下操作之一：

* 实施 `AdPolicySelector` 接口及其所有方法。
如果需要覆盖所有默认的广告行为，建议使用此选项。

* 扩展 `DefaultAdPolicySelector` 类，并仅为那些需要自定义的行为提供实现。
如果您只需要覆盖某些默认行为，则建议使用此选项。

对于这两个选项，请完成以下任务：

要自定义广告行为，请执行以下操作：

1. 实施AdPolicySelector接口及其所有方法。

1. 通过广告工厂分配TVSDK要使用的策略实例。

>[!IMPORTANT]
>
>取消分配MediaPlayer实例时，将清除在开始播放时注册的自定义广告策略。每次创建新播放会话时，您的应用程序都必须注册一个策略选择器实例。

例如：

```
    class CustomContentFactory extends ContentFactory {
     ...
    @Override
    public AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem mediaPlayerItem) {
    return new CustomAdPolicySelector(mediaPlayerItem);
    }
     ...
    }
    TVSDK 1.4 for Android Programmer's Guide 46
    // register the custom content factory with media player
    MediaPlayerItemConfig config = new MediaPlayerItemConfig();
    config.setAdvertisingFactory(new CustomContentFactory());
    // this config will should be later passed while loading the resource
    mediaPlayer.replaceCurrentResource(resource, config);
```

1. 实施您的自定义项。
