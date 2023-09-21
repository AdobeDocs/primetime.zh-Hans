---
description: MediaPlayer提供了一个notifyClick()函数，可在可点击广告播放时调度与广告相关的事件。 这些事件可提供广告和广告时间信息，您的应用程序可使用这些信息来提供点进功能。
title: 处理可点击的广告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# 处理可点击的广告 {#handle-clickable-ads}

MediaPlayer提供了一个notifyClick()函数，可在可点击广告播放时调度与广告相关的事件。 这些事件可提供广告和广告时间信息，您的应用程序可使用这些信息来提供点进功能。

当可点击广告播放时，MediaPlayer会触发以下事件：

* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_CLICKED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

此 `AdClickedEvent` 包含处理点进功能所需的信息。

1. 在播放器中提供控件，以便用户单击可点击广告。

   这可能是用于捕获用户点击的按钮或任何其他元素。
1. 为用户的广告点击事件添加事件侦听器。

   例如：

   ```
   document.getElementById([ 
   <i>your_click_control_id</i>]).addEventListener("click", onAdClick);
   ```

1. 为用户的点击事件添加处理程序。

   此处理程序需要提示MediaPlayer触发 `AdClicked` 事件。

   ```
   onAdClick = function (event) { 
       // Get a reference to your player 
       var player = getPlayer(); 
       if (player) { 
           // Call the MediaPlayer's notifyClick function 
           // which gets MediaPlayer to fire AdClicked 
           player.notifyClick(); 
       } 
   } 
   ```

1. 为MediaPlayer广告开始、广告点击和广告结束通知添加事件侦听器。

   ```
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted);
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_CLICKED, onAdClickedEvent);
   ```

1. 添加事件处理程序。
a.处理广告开始事件。
这可以执行任何操作，例如为用户设置UI。

   ```
   onAdStarted = function (event) { 
       if (clickAddButton && event && event.ad) { 
           var adClick = event.ad.primaryAsset && event.ad.primaryAsset.adClick; 
           if (adClick && adClick.isValid) { 
               // Do some initial processing  
               // when the ad starts, prior 
               // to the user's click. 
           } 
       } 
   }
   ```

   b.处理广告点击事件。
在本例中，我们从事件中获取广告信息，然后使用该信息打开一个新的浏览器窗口：

   ```
   onAdClickedEvent = function (event) { 
       if (event && event.ad) { 
           var adClick = event.adClick; 
           if (!(adClick && adClick.isValid)) { 
               adClick = event.ad.primaryAsset && event.ad.primaryAsset.adClick; 
           } 
           if (adClick && adClick.isValid) 
           { 
               // Do something with the currently playing ad 
               window.open(adClick.url); 
           } 
       } 
   }
   ```

   c.处理广告完成事件。

   ```
   onAdCompleted = function (event) { 
       if (clickAddButton) { 
           clickAddButton.setAttribute('hidden', 'true'); 
       } 
   }
   ```
