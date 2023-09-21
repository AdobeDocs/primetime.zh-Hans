---
description: TVSDK支持随附的横幅广告，这些广告是线性广告伴随的广告，通常在线性广告结束后保留在页面上。 您的应用程序负责显示随线性广告提供的随附横幅。
title: 伴随横幅广告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# 伴随横幅广告 {#companion-banner-ads}

TVSDK支持随附的横幅广告，这些广告是线性广告伴随的广告，通常在线性广告结束后保留在页面上。 您的应用程序负责显示随线性广告提供的随附横幅。

在显示配套广告时，请遵循以下建议：

* 尝试在播放器的布局中尽可能多地展示视频广告的伴随横幅广告。
* 仅当您的位置与其指定的高度和宽度完全匹配时，才提供随附横幅。

  >[!TIP]
  >
  >请勿调整横幅的大小。

* 在广告开始后尽快提供随附横幅。
* 请勿用随附横幅覆盖主广告/视频容器。
* 在广告结束后继续显示伴随横幅。

  标准是显示每个随附横幅，直到您有此横幅的替代项为止。

## 随附横幅数据 {#companion-banner-data}

AdBannerAsset的内容描述随附横幅。

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

此 `AdPlaybackEvent.AD_STARTED` 事件返回 `Ad` 包含 `companionAssets` 属性( `Vector.<AdAsset>`)。
每个 `AdAsset` 提供了有关显示资产的信息。

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 可用信息 </th> 
   <th colname="col2" class="entry"> 描述 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 宽度 </td> 
   <td colname="col2"> 伴随横幅的宽度（像素）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 高度 </td> 
   <td colname="col2"> 伴随横幅的高度（以像素为单位）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 资源类型 </td> 
   <td colname="col2">此随附横幅的资源类型： 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html：数据采用HTML代码。 </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe：数据是iframe URL (src)。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 横幅数据 </td> 
   <td colname="col2"> 由指定的类型的数据 <span class="codeph"> resourceType</span> 为这个同伴横幅准备的。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 静态URL </td> 
   <td colname="col2"> <p>有时，随附横幅也会有一个staticURL，它是到图像或的直接URL <span class="filepath"> .swf</span> (flash banner)。 </p> <p>如果您不想使用html或iframe，则可以使用直接指向图像或swf的URL来显示Flash舞台中的横幅。 在这种情况下，您可以使用staticURL显示横幅。 </p> <p>重要信息：您必须检查静态URL是否为有效的字符串，因为此属性可能并不总是可用。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 显示横幅广告 {#display-banner-ads}

要显示横幅广告，您需要创建横幅实例并允许TVSDK侦听与广告相关的事件。

TVSDK提供了通过关联线性广告的伴随横幅广告列表 `AdPlaybackEvent.AD_STARTED` 事件事件。

清单可通过以下方式指定随附横幅广告：

* HTML片段
* iFrame页面的URL
* 静态图像或AdobeFlashSWF文件的URL

对于每个伴随广告，TVSDK会指示您的应用程序可用的类型。

为以下对象添加侦听器 `AdPlaybackEvent.AD_STARTED` 发生以下情况的事件：

1. 清除横幅实例中的现有广告。

1. 从获取伴随广告列表 `Ad.companionAssets`.

1. 如果伴随广告列表不为空，则对横幅实例列表进行迭代。

   每个横幅实例( `AdBannerAsset`)包含宽度、高度、资源类型（html、iframe或静态）以及显示伴随横幅所需的数据等信息。

1. 如果视频广告没有使用它预订的伴随广告，则伴随资产列表不包含该视频广告的数据。

   要显示独立显示广告，请将逻辑添加到脚本中，以便在相应的横幅实例中运行正常的DFP(DoubleClick for Publishers)显示广告标记。

1. 使用将横幅信息发送到页面上的函数（通常是JavaScript） `ExternalInterface`，会在相应的位置显示横幅。

   这通常是 `div`，则您的函数会使用 `div ID` 以显示横幅。 例如：

   添加事件侦听器：

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   实施侦听器处理程序：

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
