---
description: 媒体播放器的状态决定哪些操作是合法的。
title: MediaPlayer对象的生命周期和状态
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---


# MediaPlayer对象的生命周期和状态{#lifecycle-and-statuses-of-the-mediaplayer-object}

媒体播放器的状态决定哪些操作是合法的。

对于使用媒体播放器状态：

* 可以检索`MediaPlayer.getStatus()`对象的当前状态。`MediaPlayer`

* 状态列表在[MediaPlayerStatus](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.5/com/adobe/mediacore/MediaPlayerStatus.html)枚举中定义。

`MediaPlayer`实例生命周期的状态过渡图：

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
   <td colname="col2"> <p>媒体播放器的初始状态。 播放器已创建，正在等待您指定媒体播放器项。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 初始化 </td> 
   <td colname="col2"> <p>您的应用程序调用<span class="codeph"> MediaPlayer.replaceCurrentItem()</span>。 </p> <p>媒体播放器项正在加载。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 已初始化 </td> 
   <td colname="col2"> <p>TVSDK成功设置媒体播放器项。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 准备 </td> 
   <td colname="col2"> <p>您的应用程序调用<span class="codeph"> MediaPlayer.prepareToPlay()</span>。 媒体播放器正在加载媒体播放器项目和任何相关资源。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 准备 </td> 
   <td colname="col2"> <p>TVSDK已准备媒体流，并尝试执行广告解析和广告插入（如果已启用）。 准备内容并将广告插入时间轴，或广告过程失败。 </p> <p>可以开始缓冲或播放。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 播放/暂停 </td> 
   <td colname="col2"> <p>当应用程序播放和暂停媒体时，媒体播放器会在这些状态之间移动。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 已挂起 </td> 
   <td colname="col2"> <p>如果应用程序在播放或暂停播放时导航离开播放、关闭设备或切换应用程序，媒体播放器将挂起并释放资源。 </p> <p>调用<span class="codeph"> MediaPlayer.restore()</span>将播放器返回到播放器在挂起前处于的状态。 异常情况是，如果调用暂停时播放器为SEEKING，则播放器为PAUSED，然后为SUSPENDED。 </p> <p>重要说明：  <p>请记住以下信息： 
      <ul id="ul_1B21668994D1474AAA0BE839E0D69B00"> 
       <li id="li_08459A3AB03C45588D73FA162C27A56C">仅当<span class="codeph"> MediaPlayerView </span>使用的surface对象被破坏时，<span class="codeph"> MediaPlayer </span>才会自动调用<span class="codeph">挂起</span>。 </li> 
       <li id="li_B9926AA2E7B9441490F37D24AE2678A1"><span class="codeph"> MediaPlayer </span>仅在创建<span class="codeph"> MediaPlayerView </span>使用的新表面对象时，才会自动调用<span class="codeph"> restore()</span>。 </li> 
      </ul> </p> </p> <p>如果您始终希望在恢复MediaPlayer时暂停播放，请让Android活动的<span class="codeph"> onPause()</span>方法中的应用程序调用<span class="codeph"> MediaPlayer.pause()</span>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 完成 </td> 
   <td colname="col2"> <p>播放器已到达流的末尾，且播放已停止。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 已发布 </td> 
   <td colname="col2"> <p>您的应用程序发布了媒体播放器，该播放器也会发布任何相关资源。 您不能再使用此实例。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 错误 </td> 
   <td colname="col2"> <p>进程期间发生错误。 错误还可能影响应用程序下一步的操作。 有关详细信息，请参阅<a href="../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/android-3x-error-handling-set-up.md" format="dita" scope="local">设置错误处理</a>。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>您可以使用状态来提供有关该过程的反馈，例如，在等待下一个状态更改时提供一个微调框，或者在播放媒体时采取后续步骤，例如在调用下一个方法之前等待适当的状态。

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
