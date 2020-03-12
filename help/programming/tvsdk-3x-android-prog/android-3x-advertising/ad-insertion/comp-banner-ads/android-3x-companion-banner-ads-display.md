---
description: 要显示横幅广告，您需要创建横幅实例并允许TVSDK监听广告相关事件。
seo-description: 要显示横幅广告，您需要创建横幅实例并允许TVSDK监听广告相关事件。
seo-title: 显示横幅广告
title: 显示横幅广告
uuid: cfd4b26c-9643-4b60-9aff-bc27dec289f1
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 显示横幅广告 {#display-banner-ads}

要显示横幅广告，您需要创建横幅实例并允许TVSDK监听广告相关事件。

TVSDK提供与活动中的线性广告关联的配套横幅广告列 `AdPlaybackEventListener.onAdBreakStart` 表。

清单可以通过以下方式指定配套横幅广告：

* HTML代码片断
* iFrame页面的URL
* 静态图像或Adobe Flash SWF文件的URL

对于每个配套广告，TVSDK会指示哪些类型可用于您的应用程序。

1. 为执行以下操作 `AdPlaybackEventListener.onAdBreakStart` 的事件添加一个监听器：

   * 清除横幅实例中的现有广告。
   * 从中获取伴侣广告列表 `Ad.getCompanionAssets`。
   * 如果配套广告列表不为空，则在横幅实例的列表上迭代。

      每个横幅实例(a `AdAsset`)都包含宽度、高度、资源类型（html、iframe或static）等信息以及显示配套横幅所需的数据。
   * 如果视频广告中没有随其预订的配套广告，则配套资产列表中不包含该视频广告的数据。
   * 要显示独立的显示广告，请将逻辑添加到脚本中，以在相应的横幅实例中运行正常的DFP（发布者可使用DoubleClick）显示广告标记。
   * 将横幅信息发送到页面上显示相应位置横幅的函数。

      这通常是 `div`，您的函数使用 `div ID` 显示横幅。