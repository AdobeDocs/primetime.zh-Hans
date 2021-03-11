---
description: 当用户单击广告或相关按钮时，您的应用程序必须做出响应。 TVSDK为您提供有关点击的目标URL的信息。
title: 对广告点击做出响应
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# 对广告点击做出响应{#respond-to-clicks-on-ads}

当用户单击广告或相关按钮时，您的应用程序必须做出响应。 TVSDK为您提供有关点击的目标URL的信息。

1. 要设置TVSDK的事件侦听器并提供点进信息，请注册`AdClickedEventListener.onAdClicked`。

   当用户单击广告或相关按钮时，TVSDK将调度此通知，包括有关点击目标的信息。
1. 在可点击的广告中监控用户互动。
1. 当用户触摸或单击广告或按钮时，要通知TVSDK，请在`MediaPlayerView`上调用`notifyClick`。
1. 监听TVSDK的`onAdClick(AdClickEvent event)`事件。
1. 要检索点进URL和相关信息，请使用`AdClickEvent`实例的getter方法。
1. 暂停视频。

   有关暂停视频的详细信息，请参阅[暂停并继续播放。](../../ad-insertion/clickable-ads/android-1.4-pausing-resuming-playback.md)。
1. 使用点进信息显示广告点进URL及相关信息。

       例如，您可以通过以下方式之一显示信息：
   
   * 通过在浏览器中打开点进URL，在您的应用程序中。

      在桌面平台上，视频广告播放区域用于在用户单击时调用点进URL。
   * 将用户重定向到其外部移动Web浏览器。

      在移动设备上，视频广告播放区域用于其他功能，如隐藏和显示控件、暂停播放、扩展到全屏等。 在这些设备上，会使用单独的视图（如赞助商按钮）启动点进URL。

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

