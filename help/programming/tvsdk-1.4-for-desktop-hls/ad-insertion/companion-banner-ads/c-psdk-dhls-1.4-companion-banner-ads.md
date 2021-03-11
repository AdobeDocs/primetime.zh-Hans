---
description: TVSDK支持伴侣横幅广告，这些广告是线性广告附带的广告，在线性广告结束后通常保留在页面上。 您的应用程序负责显示随线性广告提供的附属横幅。
title: 伴侣横幅广告
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---


# 配套横幅广告{#companion-banner-ads}

TVSDK支持伴侣横幅广告，这些广告是线性广告附带的广告，在线性广告结束后通常保留在页面上。 您的应用程序负责显示随线性广告提供的附属横幅。

显示配套广告时，请遵循以下建议：

* 尝试展示视频广告的配套横幅广告中的任意多个，以适合您播放器的布局。
* 仅当您的位置与其指定的高度和宽度完全匹配时，才显示配套横幅。

   >[!TIP]
   >
   >不要调整横幅大小。

* 在广告开始后尽快提供配套横幅。
* 请勿将主广告/视频容器与附带横幅叠加。
* 广告结束后继续显示配套横幅。

   标准是显示每个附带横幅，直到您更换了此横幅。

## 配套横幅数据{#companion-banner-data}

AdBannerAsset的内容描述了配套横幅。

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

`AdPlaybackEvent.AD_STARTED`事件返回一个`Ad`实例，该实例包含`companionAssets`属性(`Vector.<AdAsset>`)。
每个`AdAsset`都提供有关显示资产的信息。

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
   <td colname="col1"> 高 </td> 
   <td colname="col2"> 配套横幅的高度（以像素为单位）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 资源类型 </td> 
   <td colname="col2">此配套横幅的资源类型： 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html:数据以HTML代码显示。 </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe:数据是iframe URL(src)。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 横幅数据 </td> 
   <td colname="col2"> 由<span class="codeph"> resourceType</span>为此配套横幅指定的类型的数据。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 静态URL </td> 
   <td colname="col2"> <p>有时，配套横幅还包含一个staticURL，它是指向图像或<span class="filepath"> .swf</span>（flash横幅）的直接URL。 </p> <p>如果您不想使用html或iframe，可以使用指向图像或swf的直接URL来在Flash舞台中显示横幅。 在这种情况下，您可以使用staticURL显示横幅。 </p> <p>重要说明： 您必须检查静态URL是否为有效字符串，因为此属性可能并不总是可用。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 显示横幅广告{#display-banner-ads}

要显示横幅广告，您需要创建横幅实例并允许TVSDK监听广告相关事件。

TVSDK通过`AdPlaybackEvent.AD_STARTED`事件事件提供与线性广告关联的配套横幅广告的列表。

清单可以通过以下方式指定配套横幅广告：

* HTML片段
* iFrame页面的URL
* 静态图像或Adobe Flash SWF文件的URL

对于每个配套广告，TVSDK会指示哪些类型可用于您的应用程序。

为`AdPlaybackEvent.AD_STARTED`事件添加一个侦听器，它执行以下操作：

1. 清除横幅实例中的现有广告。

1. 从`Ad.companionAssets`获取伴侣广告的列表。

1. 如果附属广告的列表不是空的，请在横幅实例的列表上迭代。

   每个横幅实例(`AdBannerAsset`)都包含宽度、高度、资源类型（html、iframe或static）等信息以及显示配套横幅所需的数据。

1. 如果视频广告没有随其预订的配套广告，则配套资产的列表不包含该视频广告的数据。

   要显示独立的显示广告，请向脚本添加逻辑以在相应的横幅实例中运行普通DFP（针对发布者的DoubleClick）显示广告标记。

1. 通过使用`ExternalInterface`将横幅显示在适当位置，将横幅信息发送到页面上的函数（通常为JavaScript）。

   这通常是`div`，您的函数使用`div ID`显示横幅。 例如：

   添加事件侦听器：

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
