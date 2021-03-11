---
description: 检查流和播放列表（清单）的限制和要求。
title: 内容和清单要求
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---


# 内容和清单要求{#content-and-manifest-requirements}

检查流和播放列表（清单）的限制和要求。

<table id="table_D7C38CD3B4D24C3D9A3B55D8CEFE7366"> 
 <tbody> 
  <tr> 
   <td colname="col1"> 内容区段持续时间 </td> 
   <td colname="col2"> 区段的持续时间不得超过在清单文件中指定的目标持续时间。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 内容要求 </td> 
   <td colname="col2"> 每个TS区段都应开始一个关键帧。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> HLS内容 </td> 
   <td colname="col2"> <p>请记住以下事项： 
     <ul id="ul_B226605345EA46F69DA1380E16826117"> 
      <li id="li_6564DC0E879544BB8513DD2D1CFBA8DE">不支持AAC-SSR音频。 </li> 
      <li id="li_B73CAEBE4347406EA4DB25551B444BDA">不支持音频编解码器AC3和增强的AC3。 </li> 
      <li id="li_5986DD33C0FE485D99D4C00E2E6012CA">不支持具有不连续性但不支持不连续性标记的HLS流。 </li> 
      <li id="li_FED8686372DF4A39BAABC531BA4EB137">HLS Live不支持时间戳滚动。 </li> 
      <li id="li_565CFBEAD9874BA48F6E25B0893BF131">未解析HLS实时流的DVR窗口中的广告。 </li> 
      <li id="li_7D22EA32C94240D79EDDA96D9E72FE8F">AES-128加密内容不支持字节范围。 </li> 
     </ul></p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 虚线内容 </td> 
   <td colname="col2"> <p>请记住以下事项： 
     <ul id="ul_9D33C2418F9F49DEAE0E642301726F89"> 
      <li id="li_74C69A21A7BD4831B92F0D57900E1CB1">对于实时流 — 支持动态类型的实时用户档案。 </li> 
      <li id="li_0C8743DB152047819D23C9F180998AD7">对于VOD流 — 支持静态类型的实时用户档案。 </li> 
      <li id="li_FBC6828663FB413798A4BDAF0B9831AA">对于VOD流 — 点播用户档案未针对广告工作流进行认证。 </li> 
      <li id="li_4393B9B1F6144BDEAE484C879750ED23">不支持播放具有多个句点的DASH流。 </li> 
      <li id="li_6A2CEC4E974C4D44A45F5503A1A9D8D0">支持通过辅助功能标签发出信号的嵌入式字幕(608/708)。 </li> 
      <li id="li_EDE93DF4F3A64A53BA80877F701A8F0D">不支持分段/分段VTT文件。 </li> 
      <li id="li_8897F73611194030A490A4FF1178364C">带带内自定义标记的流未经过认证。 </li> 
     </ul></p> </td> 
  </tr> 
 </tbody> 
</table>

