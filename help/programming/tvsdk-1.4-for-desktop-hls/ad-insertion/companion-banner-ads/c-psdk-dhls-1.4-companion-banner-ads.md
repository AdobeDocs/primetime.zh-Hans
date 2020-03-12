---
description: TVSDK支持伴侣横幅广告，这些广告是线性广告附带的广告，通常在线性广告结束后保留在页面上。 您的应用程序负责显示随线性广告提供的配套横幅。
seo-description: TVSDK支持伴侣横幅广告，这些广告是线性广告附带的广告，通常在线性广告结束后保留在页面上。 您的应用程序负责显示随线性广告提供的配套横幅。
seo-title: 配套横幅广告
title: 配套横幅广告
uuid: 388a1683-342c-4f3b-97c8-cfcb6c5cfee1
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# 配套横幅广告 {#companion-banner-ads}

TVSDK支持伴侣横幅广告，这些广告是线性广告附带的广告，通常在线性广告结束后保留在页面上。 您的应用程序负责显示随线性广告提供的配套横幅。

显示配套广告时，请遵循以下建议：

* 尝试展示视频广告的配套横幅广告的数量与播放器布局中的相同。
* 仅当您的位置与其指定的高度和宽度完全匹配时，才显示配套横幅。

   >[!TIP]
   >
   >请勿调整横幅大小。

* 在广告开始后，尽快提供配套横幅。
* 请勿将主广告／视频容器与配套横幅叠加。
* 在广告结束后继续显示配套横幅。

   标准是显示每个配套横幅，直到您更换了此横幅。

## 配套横幅数据 {#companion-banner-data}

AdBannerAsset的内容描述一个配套横幅。

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

该事 `AdPlaybackEvent.AD_STARTED` 件返回一 `Ad` 个包含属性( `companionAssets` )的实 `Vector.<AdAsset>`例。
每个组 `AdAsset` 件都提供有关显示资产的信息。

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 可用信息 </th> 
   <th colname="col2" class="entry"> 说明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 宽度 </td> 
   <td colname="col2"> 配套横幅的宽度（以像素为单位）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 高度 </td> 
   <td colname="col2"> 配套横幅的高度（以像素为单位）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 资源类型 </td> 
   <td colname="col2">此配套横幅的资源类型： 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html:数据采用HTML代码。 </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe:数据是iframe URL(src)。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 横幅数据 </td> 
   <td colname="col2"> 由此配套横幅的resourceType指定 <span class="codeph"> 的类</span> 型数据。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 静态URL </td> 
   <td colname="col2"> <p>有时，配套横幅还有一个staticURL，它是指向图像或。swf <span class="filepath"></span> （flash横幅）的直接URL。 </p> <p>如果不想使用html或iframe，可以使用指向图像或swf的直接URL来显示Flash舞台中的横幅。 在这种情况下，您可以使用staticURL显示横幅。 </p> <p>重要说明： 您必须检查静态URL是否为有效字符串，因为此属性可能并不总是可用的。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 显示横幅广告 {#display-banner-ads}

要显示横幅广告，您需要创建横幅实例并允许TVSDK监听广告相关事件。

TVSDK提供与通过事件事件的线性广告关联的配套横幅广 `AdPlaybackEvent.AD_STARTED` 告列表。

清单可以通过以下方式指定配套横幅广告：

* HTML代码片断
* iFrame页面的URL
* 静态图像或Adobe Flash SWF文件的URL

对于每个配套广告，TVSDK会指示哪些类型可用于您的应用程序。

为执行以下操作 `AdPlaybackEvent.AD_STARTED` 的事件添加一个监听器：

1. 清除横幅实例中的现有广告。

1. 从中获取伴侣广告列表 `Ad.companionAssets`。

1. 如果配套广告列表不为空，则在横幅实例的列表上迭代。

   每个横幅实例(a `AdBannerAsset`)都包含宽度、高度、资源类型（html、iframe或static）等信息以及显示配套横幅所需的数据。

1. 如果视频广告中没有随其预订的配套广告，则配套资产列表中不包含该视频广告的数据。

   要显示独立的显示广告，请将逻辑添加到脚本中，以在相应的横幅实例中运行正常的DFP（发布者可使用DoubleClick）显示广告标记。

1. 将横幅信息发送到页面上的函数（通常为JavaScript），该函 `ExternalInterface`数使用将横幅显示在适当的位置。

   这通常是 `div`，您的函数使用 `div ID` 显示横幅。 例如：

   添加事件监听器：

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   实现监听器处理函数：

   ```js
   private function onAdStarted(event:AdPlaybackEvent):void { 
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
   function addBanner(resourceType, width, height, data) { 
       console.log(resourceType + "," +  width + "," +  height); 
   
   //Assume an html element on the page with id like 'banner300x250' 
       var bannerDiv = document.getElementById('banner' + width +  
           'x' + height);  
       if (bannerDiv != null) { 
           if (resourceType == "html") { // for html resource 
               bannerDiv.innerHTML = data; 
           } 
           else if (resourceType == "iframe") { // for iframe resource 
               bannerDiv.innerHTML = "<iframe src='" + data +  
                   "' width='100%' height='100%'></iframe>"; 
           } 
       } 
   }
   ```
