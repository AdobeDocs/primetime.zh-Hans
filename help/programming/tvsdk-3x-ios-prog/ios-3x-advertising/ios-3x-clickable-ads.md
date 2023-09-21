---
description: TVSDK为您提供信息，以便您对点进广告执行操作。 在创建播放器UI时，您必须决定当用户单击可点击广告时如何响应。
title: 可点击广告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# 可点击广告 {#clickable-ads}

TVSDK为您提供信息，以便您对点进广告执行操作。 在创建播放器UI时，您必须决定当用户单击可点击广告时如何响应。

在适用于iOS的TVSDK中，只有线性广告是可点击的。

## 响应广告点击次数 {#section_537AF2593FDB4257B81AAE2103B0C719}

当用户单击广告、随附横幅广告或相关按钮时，您的应用程序必须做出响应。 TVSDK为您提供有关单击的目标URL的信息。

1. 要为TVSDK设置事件侦听器并提供点进信息，请添加观察者 `PTMediaPlayerAdClickNotification`.

   >[!NOTE]
   >
   >当用户单击广告、伴随横幅广告或相关按钮时，TVSDK会调度此通知，包括有关点击目标的信息。

1. 监控用户对可点击广告的交互。
1. 当用户触摸或单击广告或按钮时，要通知TVSDK，请使用 `[_player notifyClick:_currentAd.primaryAsset];`.
1. 聆听 `PTMediaPlayerAdClickNotification` 事件。
1. 要检索点进URL和相关信息，请使用 `PTMediaPlayerAdClickURLKey` 对象。
1. 暂停视频。
1. 使用点进信息显示广告点进URL和相关信息。

   >[!NOTE]
   >
   >例如，您可以通过以下方式之一显示信息：

   * 在应用程序中通过在浏览器中打开点进URL来实现。

     在桌面平台上，视频广告播放区域用于在用户点击时调用点进URL。
   * 将用户重定向到他们的外部移动Web浏览器。

     在移动设备上，视频广告播放区域用于执行其他功能，例如隐藏和显示控件、暂停播放、展开到全屏等等。 在这些设备上，使用单独的视图（如发起人按钮）来启动点进URL。

1. 关闭显示点进信息的浏览器窗口，然后继续播放视频。

   例如：

   ```
      // Listening for click notification  
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdClick:)  
    name:PTMediaPlayerAdClickNotification object:self.player]; 
   - (void) onMediaPlayerAdClick:(NSNotification *) notification { 
      NSString *url = [notification.userInfo objectForKey:PTMediaPlayerAdClickURLKey];  
      if (url != nil) { 
          [self openBrowser:[NSURL URLWithString:url]]; 
      } 
   } 
   ```
