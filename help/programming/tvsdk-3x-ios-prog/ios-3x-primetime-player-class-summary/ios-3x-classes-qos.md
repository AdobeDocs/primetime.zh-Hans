---
description: 这些类提供的信息可以帮助您确定播放器的性能。
title: QoS类
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# QoS类{#qos-classes}

这些类提供的信息可以帮助您确定播放器的性能。

<table frame="all" colsep="1" rowsep="1" id="table_2893EFF9755149159A4F94E781C76B6E"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b>名称</b></th> 
   <th colname="2" class="entry"><b>说明</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTDeviceInformation.html" format="html" scope="external"> PTDeviceInformation</a> </td> 
   <td colname="2">提供有关TVSDK运行的平台和操作系统的信息： 
    <ul id="ul_0DE69F3B38E84964AB98DCCD11E5E123"> 
     <li id="li_19B2D1889FCA4B0F8FCB0EE8F87353B2">平台OS的版本 </li> 
     <li id="li_CA35F4A48FD34555AC7D7832D5997AD4">TVSDK库的版本号 </li> 
     <li id="li_30D38320C2A3440E92C0A477FFFBF9A0">设备的型号名称 </li> 
     <li id="li_2D15164B987E405685B96A900EBF041D">设备制造商的名称 </li> 
     <li id="li_B78485CB9580444DB9694404706BA191">设置UUID </li> 
     <li id="li_841EA77499B44F0692192F9DE1A798E4">设备屏幕的宽度/高度 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTPlaybackInformation.html" format="html" scope="external"> PTPlaybackInformation</a> </td> 
   <td colname="2"> 提供有关播放的执行方式的信息。 这包括帧速率、用户档案位速率、缓冲所用的总时间、缓冲尝试次数、从第一个视频片段获取第一个字节所花的时间、呈现第一个帧所花的时间、当前缓冲的长度和缓冲时间。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTQoSProvider.html" format="html" scope="external"> PTQoSProvider</a> </td> 
   <td colname="2">
    <pre>
      为播放和设备提供基本的QoS指标。
    </pre>
    <pre>
      QOS信息提供者类。
    </pre> </td> 
  </tr> 
 </tbody> 
</table>