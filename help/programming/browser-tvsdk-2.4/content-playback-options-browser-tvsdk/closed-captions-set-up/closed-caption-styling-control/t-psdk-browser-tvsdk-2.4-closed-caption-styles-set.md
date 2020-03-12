---
description: 您可以设置字体、大小、颜色、边缘和隐藏式字幕文本的不透明度等格式。
seo-description: 您可以设置字体、大小、颜色、边缘和隐藏式字幕文本的不透明度等格式。
seo-title: 设置隐藏式字幕样式
title: 设置隐藏式字幕样式
uuid: 906ed22c-e673-4211-a14b-d95d176aad21
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 设置隐藏式字幕样式{#set-closed-caption-styles}

您可以设置字体、大小、颜色、边缘和隐藏式字幕文本的不透明度等格式。

1. 等待至 `MediaPlayer` 少处于PREPARED状态。

   有关状态的详细信息，请参 [阅等待有效状态](../../../content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-state-prepared-wait-for.md)。
1. 创建实 `TextFormat` 例。

   您可以立即提供所有隐藏式字幕样式参数，也可以稍后设置。

   ```js
   new TextFormat( 
       font,   
       fontColor,  
       edgeColor,   
       fontEdge,  
       backgroundColor,   
       fillColor,  
       size,   
       fontOpacity,   
       backgroundOpacity,  
       fillOpacity, 
       bottomInset 
       safeArea) → {AdobePSDK.TextFormat}
   ```

1. （可选）获取当前的隐藏式字幕样式设置 `MediaPlayer.ccStyle`。

   返回值是接口的一个实 `TextFormat` 例。

   如果之前未设置样式，则返回一个TextFormat对象，其中每个属性的默认值为：

   ```js
   ccStyle :AdobePSDK.TextFormat
   ```

1. 要更改样式设置，请使 `MediaPlayer.ccStyle`用，传递界面的实 `TextFormat` 例。

   即使当前媒体流没有隐藏式字幕，您也可以使用此方法。

   ```js
   ccStyle :AdobePSDK.TextFormat 
   ```

   >[!TIP]
   >
   >设置隐藏式字幕样式是异步的，因此更改可能需要几秒钟时间才能显示在屏幕上。

