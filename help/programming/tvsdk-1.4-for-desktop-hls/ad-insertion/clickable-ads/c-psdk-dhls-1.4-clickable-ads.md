---
description: TVSDK为您提供信息，以便您对点进广告执行操作。 在创建播放器UI时，您必须决定当用户单击可点击广告时如何响应。
title: 可点击广告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 可点击广告 {#clickable-ads}

TVSDK为您提供信息，以便您对点进广告执行操作。 在创建播放器UI时，您必须决定当用户单击可点击广告时如何响应。

对于Flash运行时的TVSDK，只能单击线性广告。

## 响应广告点击次数 {#respond-to-clicks-on-ads}

当用户单击广告或相关按钮时，您的应用程序负责响应。 TVSDK为您提供有关目标URL的信息。

此示例显示了一种管理广告点击量的可能方式。

1. 每次播放广告时，在媒体播放器顶部显示一个按钮。 单击广告的用户将被重定向到广告URL。 此按钮是 [!DNL ClickableAdsOverlay.xml].

   ```xml
      <?xml version="1.0"?> 
   <s:VGroup xmlns:fx="https://ns.adobe.com/mxml/2009"  
       xmlns:s="library://ns.adobe.com/flex/spark" percentWidth="100" horizontalAlign="center">     
           <fx:Declarations><fx:String id="text"/></fx:Declarations> 
           <s:Label text="{text}"  backgroundAlpha="0.75" backgroundColor="#DEDEDE"  
               color="#000000" paddingBottom="5" paddingRight="5" paddingLeft="5"  
               paddingTop="5"/> 
   </s:VGroup>
   ```

1. 将此叠加图包含到我们的媒体播放器示例中， [!DNL psdkdemo.xml].

   ```xml
      <psdk:ClickableAdsOverlay id="clickableAdsOverlay"  
       visible="false"   top="10" right="0" left="0"  
       text="Click here for more information"   
       click="onAdsOverlayClicked()" 
   </psdk:ClickableAdsOverlay
   ```

1. 要使视图仅在播放广告时可见，请聆听 `onAdStart` 和 `onAdComplete` 由调度的事件。

   ```
   _player.addEventListener(AdPlaybackEvent.AD_STARTED, onAdStarted); 
   _player.addEventListener(AdPlaybackEvent.AD_COMPLETED, onAdCompleted); 
   ```

   ```
      private function onAdStarted(event:AdPlaybackEvent):void { 
       var primaryAsset:AdAsset = event.ad.primaryAsset; 
       if (primaryAsset.adClick != null) { 
           clickableAdsOverlay.visible = true;  
       } 
   } 
   private function onAdCompleted(event:AdPlaybackEvent):void { 
       clickableAdsOverlay.visible = false; 
   }
   ```

1. 监控用户对可点击广告的交互。 当用户触摸或单击广告或按钮时，通知TVSDK `notifyClick`.

   ```
   private function onAdsOverlayClicked():void {     
       _mediaPlayer.view.notifyClick(); 
   }
   ```

1. 聆听 `AdclickEvent.AD_CLICK` 事件。

   如果广告正在播放，TVSDK会调度 `AdClickEvent.AD_CLICK` 事件，从中可检索点进URL和相关信息。

   ```
      _player.addEventListener(AdClickEvent.AD_CLICK, onAdClick);
   ```

1. 在将用户定向到广告URL时暂停媒体播放器。

   ```
   private function onAdClick(event:AdClickEvent):void { 
       _logger.info("#onAdClick Ad clicked. Target url is {0}", event.adClick.url);  
       _player.pause(); 
       var adRequest:URLRequest = new URLRequest(event.adClick.url); 
       navigateToURL(adRequest, event.adClick.title); 
   }
   ```

1. 显示广告点进URL和任何相关信息。

       例如，您可以通过以下方式之一显示它：
   
   * 在应用程序内的浏览器中打开点进URL。

     在桌面平台上，视频广告播放区域通常用于在用户单击时调用点进URL。
   * 将用户重定向到外部移动Web浏览器。

     在移动设备上，视频广告播放区域用于执行其他功能，例如隐藏和显示控件、暂停播放、展开到全屏等等。 因此，在移动设备上，通常会向用户显示一个单独的视图（例如发起人按钮），作为启动点进URL的一种方式。

1. 关闭显示点进信息的浏览器窗口，然后继续播放视频。
