---
description: 要添加VPAID 2.0支持，请添加自定义广告视图和相应的监听器。
seo-description: 要添加VPAID 2.0支持，请添加自定义广告视图和相应的监听器。
seo-title: 实施VPAID 2.0集成
title: 实施VPAID 2.0集成
uuid: fa5b9cdd-e684-4656-91b7-50781dc59e23
translation-type: tm+mt
source-git-commit: 25f97c8d296f71deddc8f9d12b97007ddf73f603
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 2%

---


# 实施VPAID 2.0集成{#implement-vpaid-integration}

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

1. 创建监听器并处理事件监听器中描述的事件。

   >[!IMPORTANT]
   >
   >在VPAID 2.0工作流程中，对于自定义广告视图，在`AdBreak`开始(事件`AD_BREAK_START`)和`AdBreak`完成(事件`AD_BREAK_COMPLETE`)之间维护您的`CustomAdView`实例非常重要，从创建自定义广告视图到处置自定义广告实例。 也就是说，不要在每个广告中断开始上创建自定义广告视图，并在每个广告中断完成处理。
   >
   >
   >此外，您只应在播放器处于PREPARED状态时创建自定义广告视图,
   >
   >
   >调用重置时仅处置自定义广告视图。 例如：
   >
   >
   ```
   >// on reset 
   >if (_mediaPlayer != null) { 
   >       _mediaPlayer.disposeCustomAdView(); 
   >       ... 
   >} 
   >```
   >
   >最后，在处理自定义广告视图之前，必须将其从`FrameLayout`中删除。 例如：
   >
   >
   ```
   >if (_playerFrame != null) 
   >       _playerFrame.removeAllViews(); 
   >```
