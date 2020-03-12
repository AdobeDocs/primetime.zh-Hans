---
description: 媒体播放器的状态决定哪些操作是合法的。
seo-description: 媒体播放器的状态决定哪些操作是合法的。
seo-title: MediaPlayer对象的生命周期和状态
title: MediaPlayer对象的生命周期和状态
uuid: a2866f84-a722-46ed-b4cb-36664db5be82
translation-type: tm+mt
source-git-commit: 56dc79e5b4df11ff730d7d8f23dea8d0f4712077

---


# MediaPlayer对象的生命周期和状态{#lifecycle-and-statuses-of-the-mediaplayer-object}

媒体播放器的状态决定哪些操作是合法的。

对于使用媒体播放器状态：

* 您可以检索对象的当 `MediaPlayer` 前状态 `MediaPlayer.getStatus()`。

* 状态列表在 [MediaPlayerStatus枚举中定义](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.5/com/adobe/mediacore/MediaPlayerStatus.html) 。

实例生命周期的状态转换图 `MediaPlayer` 表：

<!--<a id="fig_A6425F24C7734DC681D992859D2A6743"></a>-->

![](assets/media_player_statuses.png)

下表提供了有关媒体播放器的生命周期和状态的详细信息：

<table id="table_82757A0043EB4AACA474E6B30326A6B7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 状态 </th> 
   <th colname="col2" class="entry"> 在 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 空闲 </td> 
   <td colname="col2"> <p>媒体播放器的初始状态。 播放器已创建，并且正在等待您指定媒体播放器项目。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 初始化 </td> 
   <td colname="col2"> <p>您的应用程 <span class="codeph"> 序调用MediaPlayer.replaceCurrentItem() </span>。 </p> <p>正在加载媒体播放器项目。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 已初始化 </td> 
   <td colname="col2"> <p>TVSDK成功设置媒体播放器项。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 准备 </td> 
   <td colname="col2"> <p>您的应用 <span class="codeph"> 程序调用MediaPlayer.prepareToPlay() </span>。 媒体播放器正在加载媒体播放器项目和任何相关资源。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 准备好 </td> 
   <td colname="col2"> <p>TVSDK已准备好媒体流，并尝试执行广告解析和广告插入（如果启用）。 准备内容并将广告插入时间轴中，或广告过程失败。 </p> <p>缓冲或回放可以开始。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 播放／暂停 </td> 
   <td colname="col2"> <p>当应用程序播放和暂停媒体时，媒体播放器会在这些状态之间移动。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 已暂停 </td> 
   <td colname="col2"> <p>如果应用程序在播放器播放或暂停时导航离开播放、关闭设备或切换应用程序，则媒体播放器将暂停并释放资源。 </p> <p>调 <span class="codeph"> 用MediaPlayer.restore()会将播放器 </span> 返回到播放器在暂停前处于的状态。 但是，如果在调用暂停时播放器为SEEKING，则播放器为PAUSED，然后为SUSPENDED。 </p> <p>重要说明：  <p>请记住以下信息： 
      <ul id="ul_1B21668994D1474AAA0BE839E0D69B00"> 
       <li id="li_08459A3AB03C45588D73FA162C27A56C">仅当MediaPlayerView <span class="codeph"> 所使用的 </span> 表面对象被破坏时，MediaPlayer才会自动调用 <span class="codeph"> 暂停 </span><span class="codeph"></span> 操作。 </li> 
       <li id="li_B9926AA2E7B9441490F37D24AE2678A1">仅当创建 <span class="codeph"> MediaPlayerView使用的 </span> 新表面对象时，MediaPlayer才会自动调用restore() <span class="codeph"></span><span class="codeph"></span> 。 </li> 
      </ul> </p> </p> <p>如果您始终希望在恢复MediaPlayer时暂停播放，请让应用程序在Android活动的 <span class="codeph"> onPause()方法中调用 </span> MediaPlayer.pause() <span class="codeph"></span> 。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 完成 </td> 
   <td colname="col2"> <p>播放器已到达流的末尾，且播放已停止。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 已发布 </td> 
   <td colname="col2"> <p>您的应用程序发布了媒体播放器，该播放器也会释放任何相关资源。 您不能再使用此实例。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 错误 </td> 
   <td colname="col2"> <p>进程中出现错误。 错误也可能影响应用程序下一步的操作。 有关详细信息，请参 <a href="../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/android-3x-error-handling-set-up.md" format="dita" scope="local"> 阅设置错误处理 </a>。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>您可以使用状态来提供有关该过程的反馈，或者例如，在等待下一个状态更改时提供一个微调框，或者在播放媒体时采取下一步骤，例如在调用下一个方法之前等待适当的状态。

例如：

```java
mediaPlayer.addEventListener(MediaPlayerEvent STATUS_CHANGED, new StatusChangeEventListener() { 
    @Override  
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        switch(event.getStatus()) { 
            case INITIALIZED: 
                mediaPlayer.prepareToPlay(); 
                break; 
            case PREPARING: 
                showBufferingSpinner(); 
                break; 
            case PREPARED: 
                hideBufferingSpinner(); 
                mediaPlayer.play(); 
                break; 
            ...                
        } 
        ... 
    } 
}); 
```
