---
description: TVSDK支持随附的横幅广告，这些广告是线性广告伴随的广告，通常在线性广告结束后保留在页面上。 您的应用程序负责显示随线性广告提供的随附横幅。
title: 伴随横幅广告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '557'
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

PTAdAsset的内容描述随附横幅。

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

此 `PTMediaPlayerAdStartedNotification` 通知返回 `PTAd` 包含 `companionAssets` 属性(数组 `PtAdAsset`)。
每个 `PtAdAsset` 提供了有关显示资产的信息。

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>可用信息</b></th> 
   <th colname="col2" class="entry"><b>描述</b></th> 
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
     <li id="li_76B945007CE842158B5125422765E0B2">静态：数据是静态URL，它是图像的直接URL。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 数据 </td> 
   <td colname="col2"> 由指定的类型的数据 <span class="codeph">resourceType</span> 为这个同伴横幅准备的。 </td> 
  </tr> 
 </tbody> 
</table>

## 显示横幅广告 {#display-banner-ads}

要显示横幅广告，您需要创建横幅实例并允许TVSDK侦听与广告相关的事件。

TVSDK提供了通过关联线性广告的伴随横幅广告列表 `PTMediaPlayerAdPlayStartedNotification` 通知事件。

清单可通过以下方式指定随附横幅广告：

* HTML片段
* iFrame页面的URL
* 静态图像或AdobeFlashSWF文件的URL

对于每个伴随广告，TVSDK会指示您的应用程序可用的类型。

1. 创建 `PTAdBannerView`  页面上每个伴随广告时段的实例。

       确保已提供以下信息：
   
   * 为了防止检索不同大小的伴随广告，请使用指定宽度和高度的横幅实例。
   * 标准横幅大小。

1. 添加观察者 `PTMediaPlayerAdStartedNotification` 此操作如下：
   1. 清除横幅实例中的现有广告。
   1. 从获取伴随广告列表 `Ad.getCompanionAssets` `PTAd.companionAssets`.
   1. 如果伴随广告列表不为空，则对横幅实例列表进行迭代。

      每个横幅实例( a `PTAdAsset`)包含宽度、高度、资源类型（html、iframe或静态）以及显示伴随横幅所需的数据等信息。
   1. 如果视频广告没有使用它预订的伴随广告，则伴随资产列表不包含该视频广告的数据。

      要显示独立显示广告，请将逻辑添加到脚本中，以便在相应的横幅实例中运行正常的DFP(DoubleClick for Publishers)显示广告标记。
   1. 将横幅信息发送到页面上的某个函数，该函数会在适当的位置显示横幅。

      这通常是 `div`，则您的函数会使用 `div ID` 以显示横幅。 例如：

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
