---
description: 要显示横幅广告，您需要创建横幅实例并允许浏览器TVSDK侦听广告相关事件。
title: 显示横幅广告
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# 显示横幅广告{#display-banner-ads}

要显示横幅广告，您需要创建横幅实例并允许浏览器TVSDK侦听广告相关事件。

浏览器TVSDK通过`AdobePSDK.PSDKEventType.AD_STARTED`事件提供与线性广告关联的附属横幅广告的列表。

清单可以通过以下方式指定配套横幅广告：

* HTML片段
* iFrame页面的URL
* 静态图像或Adobe Flash SWF文件的URL

对于每个配套广告，浏览器TVSDK会指示哪些类型可用于您的应用程序。

为事件`AdobePSDK.PSDKEventType.AD_STARTED`添加一个侦听器，它执行以下操作：
1. 清除横幅实例中的现有广告。
1. 从`Ad.getCompanionAssets`获取伴侣广告的列表。
1. 如果附属广告的列表不是空的，请在横幅实例的列表上迭代。

   每个横幅实例(`AdBannerAsset`)都包含宽度、高度、资源类型（html、iframe或static）等信息以及显示配套横幅所需的数据。
1. 如果视频广告没有随其预订的配套广告，则配套资产的列表不包含该视频广告的数据。
1. 将横幅信息发送到页面上显示横幅的相应位置的函数。

   这通常是`div`，您的函数使用`div ID`显示横幅。 例如：

   添加事件侦听器：

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   实现监听器处理函数：

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

   处理显示的JavaScript示例：

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

