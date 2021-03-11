---
description: 服务质量(QoS)将详细视图优惠到视频引擎的性能。 TVSDK提供有关播放、缓冲和设备的详细统计信息。
title: 使用加载信息在片段级别跟踪
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# 使用加载信息{#track-at-the-fragment-level-using-load-information}在片段级别跟踪

服务质量(QoS)将详细视图优惠到视频引擎的性能。 TVSDK提供有关播放、缓冲和设备的详细统计信息。

TVSDK还提供有关以下下载资源的信息：

1. 播放列表/清单文件
1. 文件片段
1. 文件的跟踪信息

   您可以从`LoadInfo`类读取有关下载资源（如片段和轨道）的服务质量(QoS)信息。

1. 实现`onLoadInfo`回调事件侦听器。
1. 注册事件侦听器，TVSDK每次下载片段时都会调用它。
1. 从传递到回调的`LoadInfo`参数中读取所关注的数据。

   <table id="table_06BD536A23AB4A73B510998426BAE143"> 
    <thead> 
      <tr> 
      <th colname="col01" class="entry"> 属性 </th> 
      <th colname="col1" class="entry"> 类型 </th> 
      <th colname="col2" class="entry"> 说明 </th> 
      </tr> 
    </thead>
    <tbody> 
      <tr> 
      <td colname="col01"> <span class="codeph"> downloadDuration  </span> </td> 
      <td colname="col1"> <span class="codeph"> 长  </span> </td> 
      <td colname="col2"> <p>下载的持续时间（以毫秒为单位）。 </p> <p>TVSDK并不区分客户端连接到服务器的时间和下载完整片段所花费的时间。 例如，如果10 MB区段需要8秒钟才能下载，则TVSDK会提供该信息，但不会告诉您直到第一个字节之前需要4秒，下载整个片段还需要4秒。 </p> </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration  </span> </td> 
      <td colname="col1"> <span class="codeph"> 长  </span> </td> 
      <td colname="col2"> 已下载片段的媒体持续时间（以毫秒为单位）。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> periodIndex  </span> </td> 
      <td colname="col1"> <span class="codeph"> int  </span> </td> 
      <td colname="col2"> 与下载的资源关联的时间轴期间索引。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> 大小  </span> </td> 
      <td colname="col1"> <span class="codeph"> 长  </span> </td> 
      <td colname="col2"> 已下载资源的大小（以字节为单位）。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex  </span> </td> 
      <td colname="col1"> <span class="codeph"> int  </span> </td> 
      <td colname="col2"> 相应轨道的索引（如果已知）；否则，为0。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackName  </span> </td> 
      <td colname="col1"> <span class="codeph"> 字符串  </span> </td> 
      <td colname="col2"> 相应轨道的名称（如果已知）；否则，为null。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackType  </span> </td> 
      <td colname="col1"> <span class="codeph"> 字符串  </span> </td> 
      <td colname="col2"> 相应轨道的类型（如果已知）；否则，为null。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> 类型  </span> </td> 
      <td colname="col1"> <span class="codeph"> 字符串  </span> </td> 
      <td colname="col2"> TVSDK下载的内容。 以下任一： 
      <ul id="ul_9C3BDEBD878544DA95C7FF81114F9B5C"> 
      <li id="li_A093552B492A44FD8B30785E465F6886">MANIFEST — 播放列表/清单 </li> 
      <li id="li_DEF9AC71AA564F9BB4C5D4E834432EE5">片段 — 片段 </li> 
      <li id="li_57821F47B6F04CD38570BCE6447A01B8">TRACK — 与特定轨道关联的片段 </li> 
      </ul> 有时，可能无法检测资源的类型。 如果发生这种情况，则返回FILE。 </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> url  </span> </td> 
      <td colname="col1"> <span class="codeph"> 字符串  </span> </td> 
      <td colname="col2"> 指向已下载资源的URL。 </td> 
      </tr> 
    </tbody> 
   </table>
