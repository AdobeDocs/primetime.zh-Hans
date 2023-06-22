---
description: 从创建MediaPlayer实例的那一刻到终止（重用或删除）该实例的那一刻，此实例会完成状态之间的一系列过渡。
title: MediaPlayer对象生命周期
exl-id: efb39fea-1050-41e5-93d8-1175a54f81e5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# MediaPlayer对象生命周期{#mediaplayer-object-lifecycle}

从创建MediaPlayer实例的那一刻到终止（重用或删除）该实例的那一刻，此实例会完成状态之间的一系列过渡。

仅当播放器处于特定状态时，才允许执行某些操作。 例如，调用 `play` 在 `IDLE` 不允许。 只有在播放器到达 `PREPARED` 省/州。

要使用状态，请执行以下操作：

* 您可以检索的当前 `MediaPlayer` 对象 `MediaPlayer.getStatus`.

   ```java
   PlayerState getStatus() throws IllegalStateException;
   ```

* 状态列表定义于 `MediaPlayer.PlayerState`.

生命周期的状态转换图 `MediaPlayer` 实例：
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

下表提供了其他详细信息：

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> MediaPlayer.PlayerState </th> 
   <th colname="col2" class="entry"> 发生于 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 空闲 </span> </td> 
   <td colname="col2"> <p>您的应用程序通过调用请求了新媒体播放器 <span class="codeph"> DefaultMediaPlayer.create </span>. 新创建的播放器正在等待您指定媒体播放器项目。 这是媒体播放器的初始状态。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 正在初始化 </span> </td> 
   <td colname="col2"> <p>您的应用程序调用了 <span class="codeph"> MediaPlayer.replaceCurrentItem </span>，并且媒体播放器正在加载。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已初始化 </span> </td> 
   <td colname="col2"> <p>TVSDK已成功设置媒体播放器项目。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 正在准备 </span> </td> 
   <td colname="col2"> <p>您的应用程序调用了 <span class="codeph"> MediaPlayer.prepareToPlay </span>. 媒体播放器正在加载媒体播放器项目和相关资源。 </p> <p>提示：可能会出现主媒体的某种缓冲。 </p> <p>TVSDK正在准备媒体流并尝试执行广告解析和广告插入（如果已启用）。 </p> <p>提示：要将开始时间设置为非零值，请调用 <span class="codeph"> prepareToPlay(startTime) </span> 以毫秒为单位的时间。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已准备 </span> </td> 
   <td colname="col2"> <p>内容已准备好，并且已在时间轴中插入广告，或者广告过程失败。 可以开始缓冲或播放。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 正在播放 </span> </td> 
   <td colname="col2"> <p>您的应用程序已调用 <span class="codeph"> play </span>，因此TVSDK尝试播放视频。 某些缓冲可能会发生在视频实际播放之前。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已暂停 </span> </td> 
   <td colname="col2"> <p>当应用程序播放和暂停媒体时，媒体播放器会在此状态和“正在播放”之间移动。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已暂停 </span> </td> 
   <td colname="col2"> <p>在播放器正在播放或暂停时，您的应用程序从播放器导航离开、关闭设备或切换应用程序。 媒体播放器已暂停，并且已释放资源。 要继续，请恢复媒体播放器。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 完成 </span> </td> 
   <td colname="col2"> <p>播放器到达流结尾，并且播放已停止。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已发布 </span> </td> 
   <td colname="col2"> <p>您的应用程序已发布媒体播放器，该播放器还会发布任何关联的资源。 您无法再使用此实例 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 错误 </span> </td> 
   <td colname="col2"> <p>处理过程中出错。 错误还可能会影响应用程序下一步可以执行的操作。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>您可以使用状态提供对进程的反馈（例如，在等待下一个状态更改时进行微调），或者执行播放媒体的下一个步骤，例如，在调用下一个方法之前等待适当的状态。

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
