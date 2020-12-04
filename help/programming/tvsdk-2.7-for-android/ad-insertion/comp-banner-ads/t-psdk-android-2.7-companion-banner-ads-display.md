---
description: 要显示横幅广告，您需要创建横幅实例并允许TVSDK监听广告相关事件。
seo-description: 要显示横幅广告，您需要创建横幅实例并允许TVSDK监听广告相关事件。
seo-title: 显示横幅广告
title: 显示横幅广告
uuid: 7246dfab-860f-4b55-9554-49738a483406
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# 显示横幅广告{#display-banner-ads}

要显示横幅广告，您需要创建横幅实例并允许TVSDK监听广告相关事件。

TVSDK通过`AdPlaybackEventListener.onAdBreakStart`列表提供与线性广告相关的配套横幅广告事件。

清单可以通过以下方式指定配套横幅广告：

* HTML片段
* iFrame页面的URL
* 静态图像或AdobeFlashSWF文件的URL

对于每个配套广告，TVSDK会指示哪些类型可用于您的应用程序。

1. 为`AdPlaybackEventListener.onAdBreakStart`事件添加一个侦听器，它执行以下操作：

   * 清除横幅实例中的现有广告。
   * 从`Ad.getCompanionAssets`获取伴侣广告的列表。
   * 如果配套广告的列表不为空，则在横幅实例的列表上迭代。

      每个横幅实例(`AdAsset`)都包含宽度、高度、资源类型（html、iframe或static）以及显示配套横幅所需的数据等信息。
   * 如果视频广告中未预订配套广告，则配套资产的列表不包含该视频广告的数据。
   * 要显示独立的显示广告，请向脚本添加逻辑以在相应的横幅实例中运行普通DFP（发布者双击）显示广告标记。
   * 将横幅信息发送到页面上显示相应位置横幅的函数。

      这通常是`div`，您的函数使用`div ID`显示横幅。

