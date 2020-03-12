---
description: PTMediaPlayer对象表示您的媒体播放器。 PTMediaPlayerItem表示播放器上的音频或视频。
seo-description: PTMediaPlayer对象表示您的媒体播放器。 PTMediaPlayerItem表示播放器上的音频或视频。
seo-title: 使用MediaPlayer对象
title: 使用MediaPlayer对象
uuid: eba26ad7-8c9a-4703-af32-1dfb928f6b67
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 使用MediaPlayer对象{#work-with-mediaplayer-objects}

PTMediaPlayer对象表示您的媒体播放器。 PTMediaPlayerItem表示播放器上的音频或视频。

## 关于MediaPlayerItem类 {#section_B6F36C0462644F5C932C8AA2F6827071}

成功加载媒体资源后，TVSDK会创建类的一个实例以 `PTMediaPlayerItem` 提供对该资源的访问。

解 `PTMediaPlayer` 析媒体资源，加载关联的清单文件，并分析清单。 这是资源加载过程的异步部分。 该实 `PTMediaPlayerItem` 例是在资源解析后生成的，该实例是媒体资源的已解析版本。 TVSDK提供对新创建实例的访 `PTMediaPlayerItem` 问权限 `PTMediaPlayer.currentItem`。

>[!TIP]
>
>您必须等待资源成功加载后，才能访问媒体播放器项。

## MediaPlayer对象生命周期 {#section_D87EF7FBC7B442BDBE825156DC2C1CCF}

从创建实例到终止（重用或删除）实 `PTMediaPlayer` 例，该实例将完成一系列从一个状态到另一个状态的过渡。

某些操作仅在播放器处于特定状态时才允许。 例如，不允许 `play` 调用 `PTMediaPlayerStatusCreated` 登录。 只有在播放器达到状态后，才可调用此状 `PTMediaPlayerStatusReady` 态。

要使用状态，请执行以下操作：

* 您可以使用检索MediaPlayer对象的当前状态 `PTMediaPlayer.status`。
* 状态列表在中定义 `PTMediaPlayerStatus`。

MediaPlayer实例生命周期的状态转换图：
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-ios2_web.png)

下表提供了更多详细信息：

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> PTMediaPlayerStatus </th> 
   <th colname="col2" class="entry"> 在 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCreated</span> </p> </td> 
   <td colname="col2"> <p>应用程序通过调用playerWithMediaPlayerItem请求新的媒 <span class="codeph"> 体播放器</span>。 新创建的播放器正在等待您指定媒体播放器项目。 这是媒体播放器的初始状态。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusInitializing</span> </p> </td> 
   <td colname="col2"> <p>您的应用程 <span class="codeph"> 序调用PTMediaPlayer.replaceCurrentItemWithPlayerItem</span>，并且媒体播放器正在加载。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusInitialized</span> </p> </td> 
   <td colname="col2"> <p>TVSDK成功设置媒体播放器项。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusReady</span> </p> </td> 
   <td colname="col2"> <p>内容已准备好，广告已插入时间轴中，或广告过程失败。 缓冲或回放可以开始。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPlaying</span> </p> </td> 
   <td colname="col2"> <p>您的应用程序已 <span class="codeph"> 调用play</span>，因此TVSDK正尝试播放视频。 在视频实际播放之前可能会发生一些缓冲。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPaused</span> </p> </td> 
   <td colname="col2"> <p>当应用程序播放和暂停媒体时，媒体播放器会在此状态和 <span class="codeph"> PTMediaPlayerStatusPlaying之间移动</span>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCompleted</span> </p> </td> 
   <td colname="col2"> <p>播放器到达流的末尾，播放已停止。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusStopped</span> </p> </td> 
   <td colname="col2"> <p>您的应用程序已发布媒体播放器，该播放器也会释放任何相关资源。 您不能再使用此实例 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusError</span> </p> </td> 
   <td colname="col2"> <p>进程中出现错误。 错误也可能影响应用程序下一步的操作。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>您可以使用状态来提供有关该过程的反馈（例如，在等待下一个状态更改时使用微调框）或在播放媒体时采取下一步，例如在调用下一个方法之前等待适当的状态。

