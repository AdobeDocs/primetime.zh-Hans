---
description: 要显示横幅广告，您需要创建横幅实例并允许浏览器TVSDK侦听与广告相关的事件。
title: 显示横幅广告
exl-id: 331c10a4-ae31-4d3b-aaca-9497e2970ecf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# 显示横幅广告 {#display-banner-ads}

要显示横幅广告，您需要创建横幅实例并允许浏览器TVSDK侦听与广告相关的事件。

浏览器TVSDK提供了通过关联线性广告的随附横幅广告列表 `AdobePSDK.PSDKEventType.AD_STARTED` 事件。

清单可通过以下方式指定随附横幅广告：

* HTML片段
* iFrame页面的URL
* 静态图像或AdobeFlashSWF文件的URL

对于每个伴随广告，浏览器TVSDK会指示您的应用程序可用的类型。

为事件添加侦听器 `AdobePSDK.PSDKEventType.AD_STARTED` 此操作如下：
1. 清除横幅实例中的现有广告。
1. 从获取伴随广告列表 `Ad.getCompanionAssets`.
1. 如果伴随广告列表不为空，则对横幅实例的列表进行迭代。

   每个横幅实例(一个 `AdBannerAsset`)包含宽度、高度、资源类型（html、iframe或静态）等信息，以及显示随附横幅所需的数据。
1. 如果视频广告没有使用它预订的伴随广告，则伴随资产列表不包含该视频广告的数据。
1. 将横幅信息发送到页面上的某个函数，该函数会在适当的位置显示横幅。

   这通常是 `div`，而您的函数会使用 `div ID` 以显示横幅。 例如：

   添加事件侦听器：

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   实施侦听器处理程序：

   ```js
   private function onAdStarted(event:AdPlaybackEvent):void 
   { 
       // check if there are any companion banner 
       if (event.ad && event.ad.companionAssets  
                    && event.ad.companionAssets.length > 0) { 
            for each (var banner:AdBannerAsset in event.ad.companionAssets) { 
               if (ExternalInterface.available) { 
                   //-- call the java script that will handle the banner display. 
                   ExternalInterface.call('addBanner', banner.resourceType,  
                       banner.width, banner.height, banner.bannerData); 
                } 
            } 
        }  
        //...        
   }
   ```

   用于处理显示的JavaScript示例：

   ```js
   function displayCompanion (resourceType, width, height, data) { 
       console.log(resourceType + "," +  width + "," +  height); 
       var bannerDiv = document.getElementById('banner' + width + 'x' + height);  
   
       // Assuming that there is an HTML element on the page  
       // with an id of "banner300x250", for example 
       if (bannerDiv !== null) { 
           bannerDiv.innerHTML = data; 
       } 
   }
   ```
