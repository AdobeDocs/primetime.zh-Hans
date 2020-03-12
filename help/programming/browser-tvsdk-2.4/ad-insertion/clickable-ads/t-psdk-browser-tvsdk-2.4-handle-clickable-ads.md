---
description: MediaPlayer提供了一个notifyClick()函数，该函数在播放可单击的广告时调度与广告相关的事件。 这些事件提供广告和广告中断信息，您的应用程序可以使用这些信息来提供点进功能。
seo-description: MediaPlayer提供了一个notifyClick()函数，该函数在播放可单击的广告时调度与广告相关的事件。 这些事件提供广告和广告中断信息，您的应用程序可以使用这些信息来提供点进功能。
seo-title: 处理可点击广告
title: 处理可点击广告
uuid: 5d3c9d36-60d7-4272-a523-7d1fe0e1615f
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 处理可点击广告 {#handle-clickable-ads}

MediaPlayer提供了一个notifyClick()函数，该函数在播放可单击的广告时调度与广告相关的事件。 这些事件提供广告和广告中断信息，您的应用程序可以使用这些信息来提供点进功能。

播放可单击广告时，MediaPlayer将触发以下事件：

* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_CLICKED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

其中 `AdClickedEvent` 包含处理点进功能所需的信息。

1. 在播放器中为用户提供单击可点击广告的控件。

   这可以是用于捕获用户单击的按钮或任何其他元素。
1. 为用户的广告点击事件添加事件监听器。

   例如：

   ```
   document.getElementById([ 
   <i>your_click_control_id</i>]).addEventListener("click", onAdClick);
   ```

1. 为用户的单击事件添加一个处理函数。

   此处理函数需要提示MediaPlayer触发事 `AdClicked` 件。

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

1. 为MediaPlayer广告开始、已点击广告和已完成广告通知添加事件监听器。

   ```
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted);
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_CLICKED, onAdClickedEvent);
   ```

1. 添加事件处理函数。
a.处理广告开始事件。
这可以执行任何操作，如为用户设置UI。

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

   b.处理已点击广告的事件。
在此示例中，我们从活动中获取广告信息，并使用该信息打开一个新的浏览器窗口：

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
