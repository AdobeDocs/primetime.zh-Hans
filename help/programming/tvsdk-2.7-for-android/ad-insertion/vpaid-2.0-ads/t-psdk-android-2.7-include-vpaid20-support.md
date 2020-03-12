---
description: 要添加VPAID 2.0支持，请添加自定义广告视图和相应的监听器。
seo-description: 要添加VPAID 2.0支持，请添加自定义广告视图和相应的监听器。
seo-title: 实施VPAID 2.0集成
title: 实施VPAID 2.0集成
uuid: fa5b9cdd-e684-4656-91b7-50781dc59e23
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 实施VPAID 2.0集成 {#implement-vpaid-integration}

要添加VPAID 2.0支持，请添加自定义广告视图和相应的监听器。

要添加VPAID 2.0支持，请执行以下操作：

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

1. 创建监听器并处理event-listeners中描述的事件。

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
   >
   ```   >
   >



   >最后，在处理自定义广告视图之前，必须将其从中删除 `FrameLayout`。 例如：   >
   >
   >
   ```>
   if (_playerFrame != null) 
      _playerFrame.removeAllViews(); 
   ```
