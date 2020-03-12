---
description: TVSDK为您提供信息，以便您能够对点进广告采取操作。 在创建播放器UI时，您必须决定当用户单击可单击的广告时如何响应。
seo-description: TVSDK为您提供信息，以便您能够对点进广告采取操作。 在创建播放器UI时，您必须决定当用户单击可单击的广告时如何响应。
seo-title: 可点击广告
title: 可点击广告
uuid: dc02cba7-34ad-4c74-9ceb-2fc1050d54aa
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 可点击广告{#clickable-ads}

TVSDK为您提供信息，以便您能够对点进广告采取操作。 在创建播放器UI时，您必须决定当用户单击可单击的广告时如何响应。

在iOS的TVSDK中，只有线性广告可单击。

## 响应广告点击 {#section_537AF2593FDB4257B81AAE2103B0C719}

当用户单击广告、配套横幅广告或相关按钮时，您的应用程序必须做出响应。 TVSDK会为您提供有关单击的目标URL的信息。

1. 要为TVSDK设置事件监听器并提供点进信息，请为添加观察器 `PTMediaPlayerAdClickNotification`。

   >[!NOTE]
   >
   >当用户单击广告、配套横幅广告或相关按钮时，TVSDK将调度此通知，包括有关单击目标的信息。

1. 通过可点击广告监控用户互动。
1. 当用户触摸或单击广告或按钮时，要通知TVSDK，请使用 `[_player notifyClick:_currentAd.primaryAsset];`。
1. 聆听TVSDK `PTMediaPlayerAdClickNotification` 的活动。
1. 要检索点进URL和相关信息，请使用该对 `PTMediaPlayerAdClickURLKey` 象。
1. 暂停视频。
1. 使用点进信息显示广告点进URL和相关信息。

   >[!NOTE]
   >
   >例如，您可以通过以下方式之一显示信息：

   * 通过在浏览器中打开点进URL，在您的应用程序中。

      在桌面平台上，视频广告播放区域用于在用户单击时调用点进URL。
   * 将用户重定向到其外部移动Web浏览器。

      在移动设备上，视频广告播放区域用于其他功能，如隐藏和显示控件、暂停播放、扩展到全屏等。 在这些设备上，使用单独的视图（如赞助商按钮）启动点进URL。

1. 关闭其中显示点进信息的浏览器窗口并继续播放视频。

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

