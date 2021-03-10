---
description: 您可以自定义广告插入元数据。
title: 自定义广告插入元数据
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# 自定义广告插入元数据{#customize-ad-insertion-metadata}

您可以自定义广告插入元数据。

1. 为未解决的商机设置广告元数据的超时。

   此超时的默认值为20秒。
1. 要将该值更改为10秒，请输入以下内容：

   ```js
   auditudeSettings.timeout = 10000; //this value is specified in milliseconds
   ```

   `timeout`属性在`AdvertisingMetadata`类中定义，可以为从`AdvertisingMetadata`类派生的任何自定义广告设置设置此超时。 例如，如果用户为FreeWheel解析程序定义自定义设置，则他们可以使用此设置设置默认超时。

1. 使用步骤2中的广告设置创建`MediaPlayerItemConfig`。

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings;
   ```

1. 在`MediaPlayer`上调用`replaceCurrentResource`时使用此配置。

   ```js
   player.replaceCurrentResource(mediaResource, config);
   ```

