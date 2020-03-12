---
description: 在支持GPU（硬件）加速的设备上，可以使用flash.media.StageVideo对象直接在设备硬件上处理视频。
seo-description: 在支持GPU（硬件）加速的设备上，可以使用flash.media.StageVideo对象直接在设备硬件上处理视频。
seo-title: StageVideo最低要求
title: StageVideo最低要求
uuid: 8916dbac-33e0-4efd-8105-9ddbc85f0a3f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# StageVideo最低要求{#stagevideo-minimum-requirements}

在支持GPU（硬件）加速的设备上，可以使用flash.media.StageVideo对象直接在设备硬件上处理视频。

<!--<a id="section_64DDAA8DB215493E8A7CA6636819D350"></a>-->

不同因素的组合决定了您何时以及如何使用 `StageVideo`。 下表显示了与使用StageVideo相关的某些要求和限制的快照。 这些要求和限制可能会发生变化。

<table id="table_882F4462A5AE47E28A60A39D112164A7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 平台 </th> 
   <th colname="col2" class="entry"> Windows和Mac OS </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Flash Player </td> 
   <td colname="col2"> 
    <ul id="ul_s42_lm2_jp"> 
     <li id="li_308FA9EC206B437A9EE04C29F9480B73">至少Flash 10.1或更高版本 </li> 
     <li id="li_5898EDB0D12A43389076BCC7F4A27A0A">对于回退到软件功能，Flash 15和更高版本 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">浏览器和 <span class="codeph"> Wmode设置</span> </td> 
   <td colname="col2"> <p><b>在Flash 15上</b>，将 <span class="codeph"> wmode=opaque</span> ，这样您就可以使用HTML叠加。 </p> <p>以下浏览器当前不支持硬件加速： 
     <ul id="ul_frv_ykf_jp"> 
      <li id="li_3D407A61FEE042A9B85A6EFACA6D7719">Microsoft Windows上的Mozilla Firefox </li> 
      <li id="li_39B85AC352564DA8B86EA826638F1F4B">Google Chrome 26之前版本以及Windows XP和Vista上的任何版本的Chrome </li> 
      <li id="li_0042BA6070C849E6B7C4B4BF4333F712">Microsoft Internet Explorer（所有版本） </li> 
     </ul>其他浏览器／操作系统组合可能会阻止访问硬件加速。 在这些情况下， <span class="codeph"> StageVideo</span> 会回退到软件，对性能产生负面影响。 </p> <p><b>在Flash 14及早期版本中</b>，如果浏览器不支持硬件加速，则Flash播放器可以直接渲染到GPU，但设置 <span class="codeph"> wmode=direct</span> ，以启用此渲染。 <p>提示： 早于2009的GPU驱动程序可能需要更新，因为这些驱动程序可能缺乏硬件加速支持。 </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> NetStream对象 </td> 
   <td colname="col2">除非 <span class="codeph"> 将NetStream对象附加到StageVideo对象，否则不调度StageVideoEvent.RENDER_STATE</span> 事件 <span class="codeph"></span><span class="codeph"></span> 。 </td> 
  </tr> 
 </tbody> 
</table>

