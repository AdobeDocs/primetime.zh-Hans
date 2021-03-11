---
description: MediaPlayer提供一个notifyClick()函数，用于在播放可单击的广告时调度与广告相关的事件。 这些事件提供您的应用程序可用来提供点进功能的广告和广告中断信息。
title: 处理可点击广告
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# 处理可点击广告{#handle-clickable-ads}

MediaPlayer提供一个notifyClick()函数，用于在播放可单击的广告时调度与广告相关的事件。 这些事件提供您的应用程序可用来提供点进功能的广告和广告中断信息。

播放可单击广告时，MediaPlayer将触发以下事件:

* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_CLICKED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

`AdClickedEvent`包含处理点进函数所需的信息。

1. 在播放器中提供一个控件，供用户单击可点击的广告。

   这可以是用于捕获用户单击的按钮或任何其他元素。
1. 为用户的广告单击事件添加事件侦听器。

   例如：

   ```
   document.getElementById([ 
   <i>your_click_control_id</i>]).addEventListener("click", onAdClick);
   ```

1. 为用户的单击事件添加一个处理程序。

   此处理函数需要提示MediaPlayer触发`AdClicked`事件。

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

1. 为MediaPlayer广告开始、已点击广告和已完成广告通知添加事件侦听器。

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

   b.处理已点击的广告事件。
在此示例中，我们从事件获取广告信息，并使用该信息打开新的浏览器窗口：

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

   c.处理广告完成的事件。

   ```
   onAdCompleted = function (event) { 
       if (clickAddButton) { 
           clickAddButton.setAttribute('hidden', 'true'); 
       } 
   }
   ```
