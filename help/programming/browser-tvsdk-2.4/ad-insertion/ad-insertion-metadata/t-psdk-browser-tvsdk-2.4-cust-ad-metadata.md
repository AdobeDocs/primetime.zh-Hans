---
description: 您可以自定义广告插入元数据。
title: 自定义广告插入元数据
exl-id: 4881ace6-e97b-448d-8fb4-64e7b69517f1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# 自定义广告插入元数据{#customize-ad-insertion-metadata}

您可以自定义广告插入元数据。

1. 为未解析的机会设置广告元数据的超时。

   此超时的默认值为20秒。
1. 要将值更改为10秒，请输入以下内容：

   ```js
   auditudeSettings.timeout = 10000; //this value is specified in milliseconds
   ```

   此 `timeout` 属性定义于 `AdvertisingMetadata` 类中，并且可以为从派生的任何自定义广告设置设置此超时。 `AdvertisingMetadata` 类。 例如，如果用户为FreeWheel解析程序定义自定义设置，则可以使用此设置设置默认超时。

1. 创建 `MediaPlayerItemConfig` ，并使用步骤2中的广告设置。

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings;
   ```

1. 调用时使用此配置 `replaceCurrentResource` 日期 `MediaPlayer`.

   ```js
   player.replaceCurrentResource(mediaResource, config);
   ```
