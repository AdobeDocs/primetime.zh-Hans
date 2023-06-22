---
description: 这些类提供的信息可帮助您确定播放器的运行情况。
title: QoS类
exl-id: ecbeddc6-b5f3-4ee1-a22c-5beec42df5ab
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# QoS类 {#qos-classes}

这些类提供的信息可帮助您确定播放器的运行情况。

<table frame="all" colsep="1" rowsep="1" id="table_2893EFF9755149159A4F94E781C76B6E"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b>名称</b></th> 
   <th colname="2" class="entry"><b>描述</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTDeviceInformation.html" format="html" scope="external"> ptdeviceInformation</a> </td> 
   <td colname="2">提供有关TVSDK运行的平台和操作系统的信息： 
    <ul id="ul_0DE69F3B38E84964AB98DCCD11E5E123"> 
     <li id="li_19B2D1889FCA4B0F8FCB0EE8F87353B2">平台操作系统的版本 </li> 
     <li id="li_CA35F4A48FD34555AC7D7832D5997AD4">TVSDK库的版本号 </li> 
     <li id="li_30D38320C2A3440E92C0A477FFFBF9A0">设备的型号名称 </li> 
     <li id="li_2D15164B987E405685B96A900EBF041D">设备制造商名称 </li> 
     <li id="li_B78485CB9580444DB9694404706BA191">设备UUID </li> 
     <li id="li_841EA77499B44F0692192F9DE1A798E4">设备屏幕的宽度/高度 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTPlaybackInformation.html" format="html" scope="external"> PTPlayback信息</a> </td> 
   <td colname="2"> 提供有关播放效果的信息。 这包括帧速率、配置文件比特率、缓冲所花费的总时间、缓冲尝试次数、从第一个视频片段获取第一个字节所需的时间、渲染第一个帧所需的时间、当前缓冲的长度以及缓冲时间。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTQoSProvider.html" format="html" scope="external"> PTQoProvider</a> </td> 
   <td colname="2">
    <pre>
      为播放和设备提供基本的QoS量度。
    </pre>
    <pre>
      QOS信息提供程序类。
    </pre> </td> 
  </tr> 
 </tbody> 
</table>
