---
description: 要添加VPAID 2.0支持，请添加自定义广告视图和相应的监听器。
seo-description: 要添加VPAID 2.0支持，请添加自定义广告视图和相应的监听器。
seo-title: 实施VPAID 2.0集成
title: 实施VPAID 2.0集成
uuid: d512fb5b-001c-4a7a-a553-d5962002bb30
translation-type: tm+mt
source-git-commit: 1034a0520590777cc0930d2f732741202bc3bc04

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
   >在VPAID 2.0工作流程中，对于自定义广告视图，从创建自定义广告视图到处理自定义广告视图，跨开始(事件 `CustomAdView` )和完成 `AdBreak` (事件 `AD_BREAK_START``AdBreak``AD_BREAK_COMPLETE`)维护实例非常重要。 也就是说，不要在每个广告中断开始时创建自定义广告视图并在每个广告中断完成时处理它。
   >
   >
   >此外，您只应当在播放器处于PREPARED状态时创建自定义广告视图，
   >
   >
   >仅在调用重置时处理自定义广告视图。 例如：   >
   >
   >
   ```>
   >// on reset 
   >if (_mediaPlayer != null) { 
   >       _mediaPlayer.disposeCustomAdView(); 
   >       ... 
   >} 
   >
   >```

   最后，在处理自定义广告视图之前，必须将其从中删除 `FrameLayout`。 例如：
   >```
   >if (_playerFrame != null) 
      _playerFrame.removeAllViews(); 
   ```
