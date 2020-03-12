---
description: 'null'
seo-description: 'null'
seo-title: 添加广告
title: 添加广告
uuid: 7762506f-b55e-445d-b8a2-c1208358a370
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 添加广告 {#add-advertising}

1. 定义广告元数据。

   ```js
   var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
     auditudeSettings.domain = "auditude.com"; 
     auditudeSettings.mediaId = "adbe_tearsofsteel2"; 
     auditudeSettings.zoneId = "123869";
   ```

1. 将广告元数据添加到 `MediaResource`。

   ```js
   var mediaResource =  
     new AdobePSDK.MediaResource(resourceUrl, resourceType, auditudeSettings, false);
   ```

1. 将设置添加到配置并添加分析 `SpliceOut` 器工厂。

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings; 
   config.advertisingFactory = new ExtCueOutContentFactory(auditudeSettings);
   ```

1. 将其添 `ExtCueOutContentFactory` 加到库部分。
1. 从库部 `ExtCueOutContentFactory.js` 分下载并将其放在工作文件夹中。

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script> 
   <script src= "ExtCueOutContentFactory.js"></script>
   ```

1. 测试配置。
