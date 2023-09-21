---
description: 这些类提供的信息可帮助您确定播放器的运行情况。
title: QoS类
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# QoS类 {#qos-classes}

这些类提供的信息可帮助您确定播放器的运行情况。

包： [com.adobe.mediacore.qos](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/package-summary.html)  包： [com.adobe.mediacore.qos.metrics](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/package-summary.html)

<table frame="all" colsep="1" rowsep="1" id="table_2893EFF9755149159A4F94E781C76B6E"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 名称 </th> 
   <th colname="2" class="entry"> 描述 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">量度。<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/BufferingMetrics.html" format="html" scope="external"> 缓冲量度</a></span></td> 
   <td colname="2"> 提供有关播放器缓冲所花费的时间以及发生缓冲事件的频率的信息。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/DeviceInformation.html" format="html" scope="external"> 设备信息</a> </span></td> 
   <td colname="2">提供有关运行短语的平台和操作系统的信息： 
    <ul id="ul_0DE69F3B38E84964AB98DCCD11E5E123"> 
     <li id="li_19B2D1889FCA4B0F8FCB0EE8F87353B2">平台操作系统的版本 </li> 
     <li id="li_CA35F4A48FD34555AC7D7832D5997AD4">短语库的版本号 </li> 
     <li id="li_30D38320C2A3440E92C0A477FFFBF9A0">设备的型号名称 </li> 
     <li id="li_2D15164B987E405685B96A900EBF041D">设备制造商名称 </li> 
     <li id="li_B78485CB9580444DB9694404706BA191">设备UUID </li> 
     <li id="li_841EA77499B44F0692192F9DE1A798E4">设备屏幕的宽度/高度 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/LoadInfo.html" format="html" scope="external"> LoadInfo</a></span> </td> 
   <td colname="2"> 包含有关加载各种资源（文件、清单或播放列表、片段/区段、磁道等）的各种QoS信息。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/PlaybackInformation.html" format="html" scope="external"> 播放信息</a></span> </td> 
   <td colname="2"> 提供有关播放如何执行的信息。 这包括帧速率、配置文件比特率、缓冲所花费的总时间、缓冲尝试的次数、从第一个视频片段获取第一个字节所需的时间、渲染第一个帧所需的时间、当前缓冲的长度以及缓冲时间。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">量度。<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/PlaybackLoadMetrics.html" format="html" scope="external"> PlaybackLoadMetrics</a></span> </td> 
   <td colname="2"> 提供有关加载媒体花费了多少时间、播放器渲染第一帧或在出错时失败花费了多少时间的信息。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">量度。<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/PlaybackLoadMetrics.html" format="html" scope="external"> PlaybackMetrics</a> </span></td> 
   <td colname="2"> 提供有关播放行为的信息。 这包括帧速率、比特率、缓冲区长度等。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph">量度。<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/metrics/PlaybackSessionMetrics.html" format="html" scope="external"> PlaybackSessionMetrics</a></span> </td> 
   <td colname="2"> 提供有关播放器实际播放了多少秒以及视频实际在屏幕上显示的时间的信息。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/qos/QOSProvider.html" format="html" scope="external"> QOSProviser</a></span></td> 
   <td colname="2">为播放和设备提供基本的QoS量度。 QOS信息提供程序类。</td> 
  </tr> 
 </tbody> 
</table>
