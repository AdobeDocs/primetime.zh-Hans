---
description: 可以设置隐藏式字幕文本的格式，如字体、大小、颜色、边缘和不透明度。
title: 设置隐藏式字幕样式
exl-id: 7ece68ce-0dc5-4899-9834-39940bbd0332
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# 设置隐藏式字幕样式{#set-closed-caption-styles}

可以设置隐藏式字幕文本的格式，如字体、大小、颜色、边缘和不透明度。

1. 等待 `MediaPlayer` 至少处于“已准备”状态。

   有关状态的更多信息，请参阅 [等待有效的状态](../../../content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-state-prepared-wait-for.md).
1. 创建 `TextFormat` 实例。

   您可以现在提供所有隐藏式字幕样式参数，也可以稍后设置它们。

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

1. （可选）使用以下方式获取当前隐藏式字幕样式设置 `MediaPlayer.ccStyle`.

   返回值是 `TextFormat` 界面。

   如果以前未设置任何样式，则它会返回一个TextFormat对象，并为每个属性设置默认值：

   ```js
   ccStyle :AdobePSDK.TextFormat
   ```

1. 要更改样式设置，请使用 `MediaPlayer.ccStyle`，传递的实例 `TextFormat` 界面。

   即使当前媒体流没有隐藏式字幕，您也可以使用此方法。

   ```js
   ccStyle :AdobePSDK.TextFormat 
   ```

   >[!TIP]
   >
   >隐藏式字幕样式的设置是异步的，因此更改可能需要几秒钟才能显示在屏幕上。
