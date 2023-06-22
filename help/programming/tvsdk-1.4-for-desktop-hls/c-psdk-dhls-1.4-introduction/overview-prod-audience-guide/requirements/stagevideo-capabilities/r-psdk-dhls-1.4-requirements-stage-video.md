---
description: 在支持GPU（硬件）加速的设备上，您可以使用flash.media.StageVideo对象直接在设备硬件上处理视频。
title: StageVideo最低要求
exl-id: f401682d-c47d-4284-8832-293515a76581
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# StageVideo最低要求{#stagevideo-minimum-requirements}

在支持GPU（硬件）加速的设备上，您可以使用flash.media.StageVideo对象直接在设备硬件上处理视频。

<!--<a id="section_64DDAA8DB215493E8A7CA6636819D350"></a>-->

不同因素的组合决定了何时以及如何使用 `StageVideo`. 下表概述了与使用StageVideo相关的一些要求和限制。 这些要求和限制可能会有变化。

<table id="table_882F4462A5AE47E28A60A39D112164A7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Platform </th> 
   <th colname="col2" class="entry"> Windows和Mac操作系统 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Flash播放器 </td> 
   <td colname="col2"> 
    <ul id="ul_s42_lm2_jp"> 
     <li id="li_308FA9EC206B437A9EE04C29F9480B73">至少Flash10.1或更高版本 </li> 
     <li id="li_5898EDB0D12A43389076BCC7F4A27A0A">对于回退到软件功能，Flash15及更高版本 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">浏览器和 <span class="codeph"> wmode</span> 设置 </td> 
   <td colname="col2"> <p><b>在Flash15</b>，设置 <span class="codeph"> wmode=opaque</span> 以便使用HTML叠加图。 </p> <p>以下浏览器当前不支持硬件加速： 
     <ul id="ul_frv_ykf_jp"> 
      <li id="li_3D407A61FEE042A9B85A6EFACA6D7719">Microsoft Windows上的Mozilla Firefox </li> 
      <li id="li_39B85AC352564DA8B86EA826638F1F4B">26之前的Google Chrome以及Windows XP和Vista上的任何版本Chrome </li> 
      <li id="li_0042BA6070C849E6B7C4B4BF4333F712">Microsoft Internet Explorer（所有版本） </li> 
     </ul>其他浏览器/操作系统组合可能会阻止对硬件加速的访问。 在这些情况下， <span class="codeph"> StageVideo</span> 回退到对性能有负面影响的软件。 </p> <p><b>在Flash14和更早版本上</b>，如果浏览器不支持硬件加速，则Flash播放器可以直接渲染到GPU，但可以设置 <span class="codeph"> wmode=direct</span> 以启用此渲染。 <p>提示：2009年以前的GPU驱动程序可能需要更新，因为这些驱动程序可能缺乏对硬件加速的支持。 </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> NetStream对象 </td> 
   <td colname="col2">此 <span class="codeph"> StageVideoEvent.RENDER_STATE</span> 除非附加 <span class="codeph"> NetStream</span> 对象 <span class="codeph"> StageVideo</span> 对象。 </td> 
  </tr> 
 </tbody> 
</table>
