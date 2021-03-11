---
description: 这些类提供的信息可以帮助您确定播放器的性能。
title: QoS类
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# QoS类{#qos-classes}

这些类提供的信息可以帮助您确定播放器的性能。

包：[com.adobe.mediacore.qos](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/package-summary.html)包：[com.adobe.mediacore.qos.metrics](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/package-summary.html)

<table frame="all" colsep="1" rowsep="1" id="table_2893EFF9755149159A4F94E781C76B6E"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 名称 </th> 
   <th colname="2" class="entry"> 说明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">量度。<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/BufferingMetrics.html" format="html" scope="external"> BufferingMetrics</a></span></td> 
   <td colname="2"> 提供有关播放器在缓冲期间所花费的时间以及发生缓冲事件的频率的信息。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/DeviceInformation.html" format="html" scope="external"> 设备信息</a> </span></td> 
   <td colname="2">提供有关短语所在的平台和操作系统的信息
    运行： 
    <ul id="ul_0DE69F3B38E84964AB98DCCD11E5E123"> 
     <li id="li_19B2D1889FCA4B0F8FCB0EE8F87353B2">平台OS的版本 </li> 
     <li id="li_CA35F4A48FD34555AC7D7832D5997AD4">短语库的版本号 </li> 
     <li id="li_30D38320C2A3440E92C0A477FFFBF9A0">设备的型号名称 </li> 
     <li id="li_2D15164B987E405685B96A900EBF041D">设备制造商的名称 </li> 
     <li id="li_B78485CB9580444DB9694404706BA191">设置UUID </li> 
     <li id="li_841EA77499B44F0692192F9DE1A798E4">设备屏幕的宽度/高度 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/LoadInfo.html" format="html" scope="external"> LoadInfo</a></span> </td> 
   <td colname="2"> 包含有关加载各种资源（文件、清单或播放列表、片段/段、轨道等）的各种QoS信息。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/PlaybackInformation.html" format="html" scope="external"> 播放信息</a></span> </td> 
   <td colname="2"> 提供有关播放的执行方式的信息。 这包括帧速率、用户档案位速率、缓冲所用的总时间、缓冲尝试次数、从第一个视频片段获取第一个字节所花的时间、呈现第一个帧所花的时间、当前缓冲的长度和缓冲时间。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">量度。<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/PlaybackLoadMetrics.html" format="html" scope="external"> PlaybackLoadMetrics</a></span> </td> 
   <td colname="2"> 提供有关媒体加载所花费的时间、播放器渲染第一帧所花的时间，或在出现错误时失败的信息。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">量度。<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/PlaybackLoadMetrics.html" format="html" scope="external"> PlaybackMetrics</a> </span></td> 
   <td colname="2"> 提供有关播放行为的信息。 这包括帧速率、比特率、缓冲区长度等。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">量度。<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/PlaybackSessionMetrics.html" format="html" scope="external"> PlaybackSessionMetrics</a></span> </td> 
   <td colname="2"> 提供有关播放器在实际播放时所花的秒数以及视频在屏幕上实际播放的时间的信息。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/QOSProvider.html" format="html" scope="external"> QOSProvider</a></span></td> 
   <td colname="2">为播放和设备提供基本的QoS指标。 QOS信息提供者类。</td> 
  </tr> 
 </tbody> 
</table>
