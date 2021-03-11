---
description: 您可以自定义或覆盖广告行为。
title: 设置自定义播放
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 1%

---


# 设置自定义播放{#cset-up-customized-playback}

您可以通过向TVSDK注册广告策略实例来自定义或覆盖广告行为。

要自定义广告行为，请执行以下操作之一：

* 实现`AdPolicySelector`接口及其所有方法。
如果您需要覆盖所有默认广告行为，建议使用此选项。

* 扩展`DefaultAdPolicySelector`类并仅为那些需要
自定义。
如果只需要覆盖某些默认行为，则建议使用此选项。

对于这两个选项，请完成以下任务:

自定义广告行为：

1. 实现AdPolicySelector接口及其所有方法。

1. 指定TVSDK通过广告工厂使用的策略实例。

>[!IMPORTANT]
>
>当MediaPlayer实例>deallocated时，将清除在>playback开头注册的自定义广告策略。每次创建新的播放会话时，您的应用程序必须注册一个策略>selector实例。

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