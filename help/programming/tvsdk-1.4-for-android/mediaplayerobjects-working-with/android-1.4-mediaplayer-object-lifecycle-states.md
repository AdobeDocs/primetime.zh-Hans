---
description: 从您创建MediaPlayer实例到您终止（重用或删除）它的那一刻，该实例将完成状态之间的一系列过渡。
title: MediaPlayer对象生命周期
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---


# MediaPlayer对象生命周期{#mediaplayer-object-lifecycle}

从您创建MediaPlayer实例到您终止（重用或删除）它的那一刻，该实例将完成状态之间的一系列过渡。

某些操作仅在播放器处于特定状态时才允许。 例如，不允许在`IDLE`中调用`play`。 只有在播放器达到`PREPARED`状态后，才可以调用此状态。

要使用状态，请执行以下操作：

* 可以检索`MediaPlayer.getStatus`对象的当前状态。`MediaPlayer`

   ```java
   PlayerState getStatus() throws IllegalStateException;
   ```

* 状态列表在`MediaPlayer.PlayerState`中定义。

`MediaPlayer`实例生命周期的状态过渡图：
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

下表提供了更多详细信息：

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> MediaPlayer.PlayerState </th> 
   <th colname="col2" class="entry"> 在 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 空闲  </span> </td> 
   <td colname="col2"> <p>您的应用程序通过调用<span class="codeph"> DefaultMediaPlayer.create </span>请求新的媒体播放器。 新创建的播放器正在等待您指定媒体播放器项。 这是媒体播放器的初始状态。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 初始化  </span> </td> 
   <td colname="col2"> <p>您的应用程序名为<span class="codeph"> MediaPlayer.replaceCurrentItem </span>，媒体播放器正在加载。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已初始化  </span> </td> 
   <td colname="col2"> <p>TVSDK成功设置媒体播放器项。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 准备  </span> </td> 
   <td colname="col2"> <p>您的应用程序名为<span class="codeph"> MediaPlayer.prepareToPlay </span>。 媒体播放器正在加载媒体播放器项和相关资源。 </p> <p>提示： 可能会对主媒体进行一些缓冲。 </p> <p>TVSDK正在准备媒体流并尝试执行广告解析和广告插入（如果已启用）。 </p> <p>提示： 要将开始时间设置为非零值，请调用<span class="codeph"> prepareToPlay(startTime)</span>，以毫秒为单位。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 准备  </span> </td> 
   <td colname="col2"> <p>准备内容并将广告插入时间轴，或广告过程失败。 可以开始缓冲或播放。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 播放  </span> </td> 
   <td colname="col2"> <p>您的应用程序已调用<span class="codeph"> play </span>，因此TVSDK正在尝试播放视频。 在视频实际播放之前可能会发生一些缓冲。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已暂停  </span> </td> 
   <td colname="col2"> <p>当应用程序播放和暂停媒体时，媒体播放器会在此状态和播放之间移动。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已挂起  </span> </td> 
   <td colname="col2"> <p>在播放器播放或暂停时，您的应用程序从播放中导航离开，关闭设备或切换应用程序。 媒体播放器已挂起，资源已释放。 要继续，请恢复媒体播放器。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 完成  </span> </td> 
   <td colname="col2"> <p>播放器到达流的末尾，播放已停止。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已发布  </span> </td> 
   <td colname="col2"> <p>您的应用程序已发布媒体播放器，该播放器也会发布任何相关资源。 您不能再使用此实例 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 错误  </span> </td> 
   <td colname="col2"> <p>进程期间发生错误。 错误还可能影响应用程序下一步的操作。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>您可以使用状态来提供对进程的反馈（例如，等待下一个状态更改时的微调框）或在播放媒体时采取下一步，例如在调用下一个方法之前等待适当的状态。

例如：

```java
@Override 
public void onStateChanged(MediaPlayer.PlayerState state,  
                           MediaPlayerNotification notification) { 
   switch (state) { 
      // It is recommended that you call prepareToPlay() after receiving  
      // the INITIALIZED state. 
      case INITIALIZED: 
         _mediaPlayer.prepareToPlay(); 
         break; 
      case PREPARING: 
         showBufferingSpinner(); 
         break; 
      case PREPARED: 
         hideBufferingSpinner(); 
      ..... 
    } 
}
```

