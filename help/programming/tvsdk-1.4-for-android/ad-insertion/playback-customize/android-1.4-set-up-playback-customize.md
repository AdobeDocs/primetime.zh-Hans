---
description: 您可以自定义或覆盖广告行为。
seo-description: 您可以自定义或覆盖广告行为。
seo-title: 设置自定义播放
title: 设置自定义播放
uuid: 9cbf0bcf-7932-409e-a690-e79f284eaf74
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 设置自定义播放 {#cset-up-customized-playback}

您可以通过向TVSDK注册广告策略实例来自定义或覆盖广告行为。

要自定义广告行为，请执行以下操作之一：

* 实现接 `AdPolicySelector` 口及其所有方法。
如果您需要覆盖所有默认广告行为，则建议使用此选项。

* 扩展类 `DefaultAdPolicySelector` 并仅为那些需要自定义的行为提供实现。
如果只需要覆盖某些默认行为，则建议使用此选项。

对于这两个选项，请完成以下任务：

自定义广告行为：

1. 实现AdPolicySelector接口及其所有方法。

1. 指定TVSDK通过广告工厂使用的策略实例。

>[!ATTENTION]
>
>当MediaPlayer实例>deallocated时，会清除在>playback开始处注册的自定义广告策略。每次创建新的播放会话时，您的应用程序必须注册一个策略>选择器实例。

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

1. 实施您的自定义。