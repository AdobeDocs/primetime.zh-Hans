---
description: 当用户单击广告或相关按钮时，您的应用程序必须做出响应。 TVSDK为您提供有关单击的目标URL的信息。
title: 响应广告点击次数
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# 响应广告点击次数{#respond-to-clicks-on-ads}

当用户单击广告或相关按钮时，您的应用程序必须做出响应。 TVSDK为您提供有关单击的目标URL的信息。

1. 要为TVSDK设置事件侦听器并提供点进信息，请注册 `AdClickedEventListener.onAdClicked`.

   当用户单击广告或相关按钮时，TVSDK会调度此通知，包括有关点击目标的信息。
1. 监控用户对可点击广告的交互。
1. 当用户触摸或单击广告或按钮时，要通知TVSDK，请调用 `notifyClick` 在 `MediaPlayerView`.
1. 聆听 `onAdClick(AdClickEvent event)` 事件。
1. 要检索点进URL和相关信息，请使用 `AdClickEvent` 实例。
1. 暂停视频。

   有关暂停视频的更多信息，请参阅 [暂停并继续播放。](../../ad-insertion/clickable-ads/android-1.4-pausing-resuming-playback.md).
1. 使用点进信息显示广告点进URL和相关信息。

       例如，您可以通过以下方式之一显示信息：
   
   * 在应用程序中通过在浏览器中打开点进URL来实现。

     在桌面平台上，视频广告播放区域用于在用户点击时调用点进URL。
   * 将用户重定向到他们的外部移动Web浏览器。

     在移动设备上，视频广告播放区域用于执行其他功能，例如隐藏和显示控件、暂停播放、展开到全屏等等。 在这些设备上，使用单独的视图（如发起人按钮）来启动点进URL。

1. 关闭显示点进信息的浏览器窗口，然后继续播放视频。

<!--<a id="example_2D93228E510D438C8AB5559897817A47"></a>-->

例如：

```java
private AdStartedEventListener adStartedEventListener = new AdStartedEventListener() { 
    @Override 
    public void onAdStarted(AdPlaybackEvent adPlaybackEvent) { 
        Ad ad = adPlaybackEvent.getAd(); 
        if (ad == null) { 
            return; 
        } 
 
        _pubOverlay.startAd(adPlaybackEvent.getAdBreak(), ad); 
 
        if (areClickableAdsEnabled() && ad.isClickable()) { 
            _isClickableAdPlaying = true; 
            _playerClickableAdFragment.show(); 
        } 
 
    } 
}; 
 
private AdCompletedEventListener adCompletedEventListener = new AdCompletedEventListener() { 
    @Override 
    public void onAdCompleted(AdPlaybackEvent adPlaybackEvent) { 
        Ad ad = adPlaybackEvent.getAd(); 
        _pubOverlay.stopAd(adPlaybackEvent.getAdBreak(), ad); 
 
        _isClickableAdPlaying = false; 
        if (ad.isClickable()) { 
            _playerClickableAdFragment.hide(); 
        } 
    } 
}; 
 
private AdClickedEventListener adClickedEventListener = new AdClickedEventListener() { 
    @Override 
    public void onAdClicked(AdClickEvent adClickEvent) { 
        AdClick adClick = adClickEvent.getAdClick(); 
        Ad ad = adClickEvent.getAd(); 
 
        String url = adClick.getUrl(); 
        if (url == null || url.trim().equals("")) { 
        } else { 
            Uri uri = Uri.parse(url); 
            Intent intent = new Intent(ACTION_VIEW, uri); 
            try { 
                startActivity(intent); 
            } catch (Exception e) { 
            } 
        } 
 
    } 
}; 
```
