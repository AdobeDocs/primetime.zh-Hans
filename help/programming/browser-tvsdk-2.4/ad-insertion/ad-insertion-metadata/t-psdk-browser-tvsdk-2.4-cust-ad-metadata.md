---
description: 您可以自定义广告插入元数据。
seo-description: 您可以自定义广告插入元数据。
seo-title: 自定义广告插入元数据
title: 自定义广告插入元数据
uuid: 047470d3-45bd-48be-82ce-4e9d9fe6ea10
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 自定义广告插入元数据{#customize-ad-insertion-metadata}

您可以自定义广告插入元数据。

1. 为未解决的机会设置广告元数据超时。

   此超时的默认值为20秒。
1. 要将该值更改为10秒，请输入以下内容：

   ```js
   auditudeSettings.timeout = 10000; //this value is specified in milliseconds
   ```

   该 `timeout` 属性在类中定义， `AdvertisingMetadata` 并且可以为从类派生的任何自定义广告设置设置此超 `AdvertisingMetadata` 时。 例如，如果用户为FreeWheel解析程序定义自定义设置，则可以使用此设置设置默认超时。

1. 使用 `MediaPlayerItemConfig` 步骤2中的广告设置进行创建。

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings;
   ```

1. 在调用时使用此 `replaceCurrentResource` 配置 `MediaPlayer`。

   ```js
   player.replaceCurrentResource(mediaResource, config);
   ```

