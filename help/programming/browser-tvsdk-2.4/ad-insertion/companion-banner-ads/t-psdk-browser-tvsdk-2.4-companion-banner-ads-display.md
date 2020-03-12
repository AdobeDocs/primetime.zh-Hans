---
description: 要显示横幅广告，您需要创建横幅实例并允许浏览器TVSDK监听广告相关事件。
seo-description: 要显示横幅广告，您需要创建横幅实例并允许浏览器TVSDK监听广告相关事件。
seo-title: 显示横幅广告
title: 显示横幅广告
uuid: aabc126e-b3aa-42dd-ab50-a7db8e324c50
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 显示横幅广告 {#display-banner-ads}

要显示横幅广告，您需要创建横幅实例并允许浏览器TVSDK监听广告相关事件。

浏览器TVSDK提供与活动中的线性广告关联的附属横幅广告的列 `AdobePSDK.PSDKEventType.AD_STARTED` 表。

清单可以通过以下方式指定配套横幅广告：

* HTML代码片断
* iFrame页面的URL
* 静态图像或Adobe Flash SWF文件的URL

对于每个配套广告，浏览器TVSDK会指示哪些类型可用于您的应用程序。

为执行以下操作的事 `AdobePSDK.PSDKEventType.AD_STARTED` 件添加监听器：
1. 清除横幅实例中的现有广告。
1. 从中获取伴侣广告列表 `Ad.getCompanionAssets`。
1. 如果配套广告列表不为空，则在横幅实例的列表上迭代。

   每个横幅实例(a `AdBannerAsset`)都包含宽度、高度、资源类型（html、iframe或static）等信息以及显示配套横幅所需的数据。
1. 如果视频广告中没有随其预订的配套广告，则配套资产列表中不包含该视频广告的数据。
1. 将横幅信息发送到页面上显示相应位置横幅的函数。

   这通常是 `div`，您的函数使用 `div ID` 显示横幅。 例如：

   添加事件监听器：

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

