---
description: 要添加VPAID 2.0支持，请添加自定义广告视图和适当的侦听器。
title: 实施VPAID 2.0集成
exl-id: a0d9a370-8fb6-4246-b59d-3b7c0b043bed
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# 实施VPAID 2.0集成 {#implement-vpaid-integration}

要添加VPAID 2.0支持，请添加自定义广告视图和适当的侦听器。

1. 当播放器处于“已准备”状态时，将自定义广告视图添加到播放器界面。

   ```java
   ... 
   private FrameLayout _playerFrame; 
       ... 
       case PREPARED: 
           ... 
           addCustomView(); 
   ... 
   private void addCustomView() { 
       ... 
       WebView view = (WebView)_mediaPlayer.getCustomAdView(); 
       ... 
       _playerFrame.addView(view);
   ```

1. 创建侦听器并处理中描述的事件 [事件](../../../../tvsdk-3x-android-prog/android-3x-events-notifications/events-summary/android-3x-events-summary.md).

   >[!IMPORTANT]
   >
   >在VPAID 2.0工作流中，对于自定义广告查看，维护以下内容非常重要： `CustomAdView` 实例跨越 `AdBreak` 开始（事件） `AD_BREAK_START`)和 `AdBreak` 完成(事件 `AD_BREAK_COMPLETE`)，从创建自定义广告视图一直到处理它为止。 也就是说，不要在每个广告时间开始时创建自定义广告视图，并在每个广告时间完成时处理它。
   >
   >
   >此外，仅当播放器处于“已准备”状态时，
   >
   >
   >仅在调用reset时处置自定义广告视图。 例如：
   >
   >
   ```
   >// on reset 
   >if (_mediaPlayer != null) { 
   >       _mediaPlayer.disposeCustomAdView(); 
   >       ... 
   >} 
   >
   >```
   >
   >最后，在处置自定义广告视图之前，您必须将其从 `FrameLayout`. 例如：
   >
   >
   ```
   >if (_playerFrame != null) 
   >       _playerFrame.removeAllViews(); 
   >```
