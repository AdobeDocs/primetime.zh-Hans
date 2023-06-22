---
description: 服务质量(QoS)提供了有关视频引擎执行情况的详细视图。 TVSDK提供有关播放、缓冲和设备的详细统计信息。
title: 使用加载信息在片段级别跟踪
exl-id: 29e82a93-783f-4e32-ab5e-12713a60cfec
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# 使用加载信息在片段级别跟踪{#track-at-the-fragment-level-using-load-information}

服务质量(QoS)提供了有关视频引擎执行情况的详细视图。 TVSDK提供有关播放、缓冲和设备的详细统计信息。

TVSDK还提供了有关以下已下载资源的信息：

1. 播放列表/清单文件
1. 文件片段
1. 文件的跟踪信息

   您可以从以下位置读取有关已下载资源（如片段和跟踪）的服务质量(QoS)信息 `LoadInfo` 类。

1. 实施 `onLoadInfo` 回调事件侦听器。
1. 注册事件侦听器，每次下载片段时TVSDK都会调用该侦听器。
1. 从以下位置读取感兴趣的数据 `LoadInfo` 传递给回调的参数。

   <table id="table_06BD536A23AB4A73B510998426BAE143"> 
    <thead> 
      <tr> 
      <th colname="col01" class="entry"> 属性 </th> 
      <th colname="col1" class="entry"> 类型 </th> 
      <th colname="col2" class="entry"> 描述 </th> 
      </tr> 
    </thead>
    <tbody> 
      <tr> 
      <td colname="col01"> <span class="codeph"> downloadduration </span> </td> 
      <td colname="col1"> <span class="codeph"> 长 </span> </td> 
      <td colname="col2"> <p>下载持续时间（以毫秒为单位）。 </p> <p>TVSDK不区分客户端连接到服务器所用的时间和下载完整片段所用的时间。 例如，如果下载10 MB的片段需要8秒，TVSDK会提供该信息，但不会告诉您第一个字节之前需要4秒，而下载整个片段需要4秒。 </p> </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration </span> </td> 
      <td colname="col1"> <span class="codeph"> 长 </span> </td> 
      <td colname="col2"> 已下载片段的媒体持续时间（以毫秒为单位）。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> 期间索引 </span> </td> 
      <td colname="col1"> <span class="codeph"> int </span> </td> 
      <td colname="col2"> 与下载的资源关联的时间线周期索引。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> 大小 </span> </td> 
      <td colname="col1"> <span class="codeph"> 长 </span> </td> 
      <td colname="col2"> 已下载资源的大小（字节）。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex </span> </td> 
      <td colname="col1"> <span class="codeph"> int </span> </td> 
      <td colname="col2"> 相应轨道的索引（如果已知）；否则为0。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackName </span> </td> 
      <td colname="col1"> <span class="codeph"> 字符串 </span> </td> 
      <td colname="col2"> 相应跟踪的名称（如果已知）；否则为null。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackType </span> </td> 
      <td colname="col1"> <span class="codeph"> 字符串 </span> </td> 
      <td colname="col2"> 相应跟踪的类型（如果已知）；否则为null。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> type </span> </td> 
      <td colname="col1"> <span class="codeph"> 字符串 </span> </td> 
      <td colname="col2"> TVSDK下载了什么。 以下任一项： 
      <ul id="ul_9C3BDEBD878544DA95C7FF81114F9B5C"> 
      <li id="li_A093552B492A44FD8B30785E465F6886">清单 — 播放列表/清单 </li> 
      <li id="li_DEF9AC71AA564F9BB4C5D4E834432EE5">片段 — 片段 </li> 
      <li id="li_57821F47B6F04CD38570BCE6447A01B8">TRACK — 与特定跟踪关联的片段 </li> 
      </ul> 有时可能无法检测资源的类型。 如果发生这种情况，则返回FILE。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> url </span> </td> 
      <td colname="col1"> <span class="codeph"> 字符串 </span> </td> 
      <td colname="col2"> 指向已下载资源的URL。 </td> 
      </tr> 
    </tbody> 
   </table>
