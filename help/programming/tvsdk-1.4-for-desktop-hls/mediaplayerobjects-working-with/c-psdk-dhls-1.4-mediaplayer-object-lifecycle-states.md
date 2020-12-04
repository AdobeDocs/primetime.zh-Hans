---
description: 从您创建MediaPlayer实例到您终止（重用或删除）它，该实例将完成一系列状态之间的过渡。
seo-description: 从您创建MediaPlayer实例到您终止（重用或删除）它，该实例将完成一系列状态之间的过渡。
seo-title: MediaPlayer对象生命周期
title: MediaPlayer对象生命周期
uuid: 1452ae3a-7ce9-439e-951c-9d3db63b1d20
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---


# MediaPlayer对象生命周期{#mediaplayer-object-lifecycle}

从您创建MediaPlayer实例到您终止（重用或删除）它，该实例将完成一系列状态之间的过渡。

某些操作仅在播放器处于特定状态时才允许。 例如，不允许在IDLE中调用`play`。 只有在播放器达到PREPARED状态后，才能调用此状态。

要处理状态，请执行以下操作：

* 可以使用`MediaPlayer.status`属性检索`MediaPlayer`对象的当前状态。

   ```
   function get status():String;
   ```

* 状态列表在`MediaPlayer.PlayerStatus`中定义。

`MediaPlayer`实例生命周期的状态过渡图：
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-flash-1_2_web.png)

下表提供了更多详细信息：

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <span class="codeph"> MediaPlayerStatus  </span> </th> 
   <th colname="col2" class="entry"> 在 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 空闲  </span> </td> 
   <td colname="col2"> <p> 您的应用程序通过实例化<span class="codeph"> MediaPlayer </span>请求了新的媒体播放器。 新创建的播放器正在等待您指定媒体播放器项。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 初始化  </span> </td> 
   <td colname="col2"> <p>您的应用程序名为<span class="codeph"> MediaPlayer.replaceCurrentResource </span>，并且媒体播放器正在加载。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已初始化  </span> </td> 
   <td colname="col2"> <p>TVSDK成功设置媒体播放器项。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 准备  </span> </td> 
   <td colname="col2"> <p>您的应用程序名为<span class="codeph"> MediaPlayer.prepareToPlay </span>。 媒体播放器正在加载媒体播放器项和相关资源。 </p> <p>提示： 可能会对主媒体进行一些缓冲。 </p> <p>TVSDK正在准备媒体流并尝试执行广告解析和广告插入（如果启用）。 </p> <p>提示： 要将开始时间设置为非零值，请调用<span class="codeph"> prepareToPlay(startTime)</span>，以毫秒为单位。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 准备  </span> </td> 
   <td colname="col2"> <p>内容已准备好，广告已插入时间轴，或广告过程失败。 缓冲或播放可以开始。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 播放  </span> </td> 
   <td colname="col2"> <p>您的应用程序已调用<span class="codeph"> play </span>，因此TVSDK正尝试播放视频。 在视频实际播放之前可能会发生一些缓冲。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已暂停  </span> </td> 
   <td colname="col2"> <p>当应用程序播放和暂停媒体时，媒体播放器在此状态和播放之间移动。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 搜索  </span> </td> 
   <td colname="col2"> <p>在暂停或播放时，媒体播放器正在寻找正确的位置。 要确定搜索何时开始或结束，请侦听<span class="codeph"> SeekEvent.SEEK_BEGIN </span>和<span class="codeph"> SeekEvent.SEEK_END </span>事件。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已完成  </span> </td> 
   <td colname="col2"> <p>播放器到达流的末尾，播放已停止。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已发布  </span> </td> 
   <td colname="col2"> <p>您的应用程序已发布媒体播放器，该播放器也会发布任何相关资源。 您不能再使用此实例 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 错误  </span> </td> 
   <td colname="col2"> <p>进程期间出错。 错误还可能影响应用程序下一步的操作。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>您可以使用状态来提供有关该过程的反馈（例如，在等待下一个状态更改时使用微调框）或在播放媒体时采取下一步，如在调用下一个方法之前等待适当的状态。

