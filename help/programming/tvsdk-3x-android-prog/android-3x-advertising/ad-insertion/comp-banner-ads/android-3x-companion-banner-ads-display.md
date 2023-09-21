---
description: 要显示横幅广告，您需要创建横幅实例并允许TVSDK侦听与广告相关的事件。
title: 显示横幅广告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# 显示横幅广告 {#display-banner-ads}

要显示横幅广告，您需要创建横幅实例并允许TVSDK侦听与广告相关的事件。

TVSDK提供了通过关联线性广告的伴随横幅广告列表 `AdPlaybackEventListener.onAdBreakStart` 事件。

清单可通过以下方式指定随附横幅广告：

* HTML片段
* iFrame页面的URL
* 静态图像或AdobeFlashSWF文件的URL

对于每个伴随广告，TVSDK会指示您的应用程序可用的类型。

1. 为以下对象添加侦听器 `AdPlaybackEventListener.onAdBreakStart` 发生以下情况的事件：

   * 清除横幅实例中的现有广告。
   * 从获取伴随广告列表 `Ad.getCompanionAssets`.
   * 如果伴随广告列表不为空，则对横幅实例列表进行迭代。

     每个横幅实例(一个 `AdAsset`)包含宽度、高度、资源类型（html、iframe或静态）以及显示伴随横幅所需的数据等信息。
   * 如果视频广告没有使用它预订的伴随广告，则伴随资产列表不包含该视频广告的数据。
   * 要显示独立显示广告，请将逻辑添加到脚本中，以便在相应的横幅实例中运行正常的DFP(DoubleClick for Publishers)显示广告标记。
   * 将横幅信息发送到页面上的某个函数，该函数会在适当的位置显示横幅。

     这通常是 `div`，则您的函数会使用 `div ID` 以显示横幅。
