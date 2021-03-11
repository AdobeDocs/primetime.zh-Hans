---
description: 在支持GPU（硬件）加速的设备上，您可以使用flash.media.StageVideo对象直接在设备硬件上处理视频。
title: StageVideo最低要求
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# StageVideo最低要求{#stagevideo-minimum-requirements}

在支持GPU（硬件）加速的设备上，您可以使用flash.media.StageVideo对象直接在设备硬件上处理视频。

<!--<a id="section_64DDAA8DB215493E8A7CA6636819D350"></a>-->

不同因素的组合决定了何时以及如何使用`StageVideo`。 下表显示了与使用StageVideo相关的某些要求和限制的快照。 这些要求和限制可能会发生变化。

<table id="table_882F4462A5AE47E28A60A39D112164A7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 平台 </th> 
   <th colname="col2" class="entry"> Windows和Mac OS </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Flash播放器 </td> 
   <td colname="col2"> 
    <ul id="ul_s42_lm2_jp"> 
     <li id="li_308FA9EC206B437A9EE04C29F9480B73">至少Flash 10.1或更高版本 </li> 
     <li id="li_5898EDB0D12A43389076BCC7F4A27A0A">对于回退到软件功能，Flash 15和更高版本 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">浏览器和<span class="codeph"> wmode</span>设置 </td> 
   <td colname="col2"> <p><b>在Flash 15上</b>，将 <span class="codeph"> wmode=</span> opaqueso设置为可使用HTML叠加。 </p> <p>以下浏览器当前不支持硬件加速： 
     <ul id="ul_frv_ykf_jp"> 
      <li id="li_3D407A61FEE042A9B85A6EFACA6D7719">Microsoft Windows上的Mozilla Firefox </li> 
      <li id="li_39B85AC352564DA8B86EA826638F1F4B">Google Chrome 26之前版本以及Windows XP和Vista上的任何版本的Chrome </li> 
      <li id="li_0042BA6070C849E6B7C4B4BF4333F712">Microsoft Internet Explorer（所有版本） </li> 
     </ul>其他浏览器/操作系统组合可能会阻止访问硬件加速。 在这些情况下， <span class="codeph"> StageVideo</span>会回退到软件，对性能产生负面影响。 </p> <p><b>在Flash 14及更早版本</b>，如果浏览器不支持硬件加速，则Flash播放器可以直接渲染到GPU，但设置 <span class="codeph"> wmode</span> =direct以启用此渲染。 <p>提示： 2009年以前的GPU驱动程序可能需要更新，因为这些驱动程序可能不支持硬件加速。 </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> NetStream对象 </td> 
   <td colname="col2">除非将<span class="codeph"> NetStream</span>对象附加到<span class="codeph"> StageVideo</span>对象，否则不调度<span class="codeph"> StageVideoEvent.RENDER_STATE</span>事件。 </td> 
  </tr> 
 </tbody> 
</table>

