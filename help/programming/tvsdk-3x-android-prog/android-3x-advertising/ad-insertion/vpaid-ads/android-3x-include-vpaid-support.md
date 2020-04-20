---
description: 要添加VPAID 2.0支持，请添加自定义广告视图和相应的监听器。
seo-description: 要添加VPAID 2.0支持，请添加自定义广告视图和相应的监听器。
seo-title: 实施VPAID 2.0集成
title: 实施VPAID 2.0集成
uuid: d512fb5b-001c-4a7a-a553-d5962002bb30
translation-type: tm+mt
source-git-commit: 83df68905f74931355264661aed6cff43b802d3f

---


# 实施VPAID 2.0集成 {#implement-vpaid-integration}

要添加VPAID 2.0支持，请添加自定义广告视图和相应的监听器。

1. 当播放器处于PREPARED状态时，将自定义广告视图添加到播放器界面。

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

1. 创建监听器并处理事件中描述的 [事件](../../../../tvsdk-3x-android-prog/android-3x-events-notifications/events-summary/android-3x-events-summary.md)。

   >[!IMPORTANT]
   >
   >在VPAID 2.0工作流程中，对于自定义广告视图，在创建自定义广告开始到处理自定义广告视图之间跨 `CustomAdView` (事件 `AdBreak` )和完成(事件 `AD_BREAK_START``AdBreak``AD_BREAK_COMPLETE`)维护实例非常重要。 也就是说，不要在每个广告分时段开始上创建自定义广告视图，并在每个广告分时段完成时处理它。
   >
   >
   >此外，您只应当在播放器处于PREPARED状态时创建自定义广告视图,
   >
   >
   >仅在调用reset时处理自定义广告视图。 例如：
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
   >最后，在处理自定义广告视图之前，必须将其从中删除 `FrameLayout`。 例如：
   >
   >
   ```
   >if (_playerFrame != null) 
   >       _playerFrame.removeAllViews(); 
   >```
