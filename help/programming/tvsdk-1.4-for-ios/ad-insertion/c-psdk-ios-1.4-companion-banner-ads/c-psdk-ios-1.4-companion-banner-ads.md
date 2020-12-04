---
description: TVSDK支持伴侣横幅广告，这些广告是线性广告的附带广告，通常在线性广告结束后保留在页面上。 您的应用程序负责显示随线性广告提供的配套横幅。
seo-description: TVSDK支持伴侣横幅广告，这些广告是线性广告的附带广告，通常在线性广告结束后保留在页面上。 您的应用程序负责显示随线性广告提供的配套横幅。
seo-title: 配套横幅广告
title: 配套横幅广告
uuid: 6f38f6ec-bc8b-4ea1-845f-90031b3d8a00
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---


# 配套横幅广告{#companion-banner-ads}

TVSDK支持伴侣横幅广告，这些广告是线性广告的附带广告，通常在线性广告结束后保留在页面上。 您的应用程序负责显示随线性广告提供的配套横幅。

显示配套广告时，请遵循以下建议：

* 尝试展示视频广告的配套横幅广告的数量，以符合您的播放器布局。
* 仅当您的位置与其指定的高度和宽度完全匹配时，才显示配套横幅。

   >[!TIP]
   >
   >不要调整横幅大小。

* 在广告开始后尽快提供配套横幅。
* 请勿将主广告／视频容器与配套横幅叠加。
* 广告结束后继续显示配套横幅。

   标准是显示每个附属横幅，直到您有此横幅的替换品。

## 配套横幅数据{#companion-banner-data}

PTAdAsset的内容描述了一个配套的横幅。

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

`PTMediaPlayerAdStartedNotification`通知返回一个`PTAd`实例，该实例包含`companionAssets`属性（`PtAdAsset`的数组）。
每个`PtAdAsset`都提供有关显示资产的信息。

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
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html:数据以HTML代码显示。 </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe:数据是iframe URL(src)。 </li> 
     <li id="li_76B945007CE842158B5125422765E0B2">静态：数据是静态URL，它是图像的直接URL。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 数据 </td> 
   <td colname="col2"> 由<span class="codeph"> resourceType</span>为此配套横幅指定的类型的数据。 </td> 
  </tr> 
 </tbody> 
</table>

## 显示横幅广告{#display-banner-ads}

要显示横幅广告，您需要创建横幅实例并允许TVSDK监听广告相关事件。

TVSDK通过`PTMediaPlayerAdPlayStartedNotification`通知列表提供与线性广告相关的附属横幅广告的事件。

清单可以通过以下方式指定配套横幅广告：

* HTML片段
* iFrame页面的URL
* 静态图像或AdobeFlashSWF文件的URL

对于每个配套广告，TVSDK会指示哪些类型可用于您的应用程序。

1. 为页面上的每个配套广告插槽创建一个`PTAdBannerView`实例。

       确保已提供以下信息：
   
   * 为防止检索不同大小的附属广告，请使用指定宽度和高度的横幅实例。
   * 标准横幅大小。

1. 为`PTMediaPlayerAdStartedNotification`添加一个观察器，它执行以下操作：
   1. 清除横幅实例中的现有广告。
   1. 从`Ad.getCompanionAssets` `PTAd.companionAssets`获取配套广告的列表。
   1. 如果配套广告的列表不为空，则在横幅实例的列表上迭代。

      每个横幅实例(`PTAdAsset`)都包含宽度、高度、资源类型（html、iframe或static）以及显示配套横幅所需的数据等信息。
   1. 如果视频广告中未预订配套广告，则配套资产的列表不包含该视频广告的数据。

      要显示独立的显示广告，请向脚本添加逻辑以在相应的横幅实例中运行普通DFP（发布者双击）显示广告标记。
   1. 将横幅信息发送到页面上显示相应位置横幅的函数。

      这通常是`div`，您的函数使用`div ID`显示横幅。 例如：

      ```
      - (void) onMediaPlayerAdPlayStarted:(NSNotification *) notification { 
          _currentAd  = [notification.userInfo  objectForKey:PTMediaPlayerAdKey];  
          if (_currentAd != nil) { 
              [self removeAllBanners]; // remove any existing PTAdBannerView views 
      
              // banners 
              if (_currentAd.companionAssets && _currentAd.companionAssets.count > 0) { 
                  PTAdAsset *bannerAsset = [_currentAd.companionAssets objectAtIndex:0]; 
      
                  PTAdBannerView *bannerView = [[PTAdBannerView alloc] initWithAsset:bannerAsset];  
                  bannerView.player = self.player; 
                  bannerView.delegate = self; 
      
                  bannerView.frame = CGRectMake(0.0, 0.0, bannerAsset.width, bannerAsset.height);  
                  [_adBannerView.bannerView addSubview:bannerView]; 
              } 
          } 
      }
      ```
