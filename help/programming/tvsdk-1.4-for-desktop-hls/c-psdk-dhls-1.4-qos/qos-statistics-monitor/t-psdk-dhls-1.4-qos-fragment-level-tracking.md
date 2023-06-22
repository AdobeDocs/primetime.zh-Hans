---
description: 您可以从LoadInformation类中读取有关已下载资源（如片段和跟踪）的服务质量(QoS)信息。
title: 使用加载信息在片段级别跟踪
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---


# 使用加载信息在片段级别跟踪{#track-at-the-fragment-level-using-load-information}

您可以从LoadInformation类中读取有关已下载资源（如片段和跟踪）的服务质量(QoS)信息。

1. 实施 `onLoadInformationAvailable` 回调事件侦听器。

   ```
   private function onLoadInformationAvailable(event:LoadInformationEvent):void { 
       var loadInformation:LoadInformation = event.loadInformation; 
       // process the load information here     
   }
   ```

1. 注册事件侦听器，每次下载片段时TVSDK都会调用该侦听器。

   ```
   player.addEventListener(LoadInformationEvent.LOAD_INFORMATION_AVAILABLE,  
                                    onLoadInformationAvailable);
   ```

1. 从以下位置读取感兴趣的数据 `LoadInformation` 会传递到回调的URL。

   <table id="table_75E61A2EB25E435DB631166A7FF64757"> 
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
      <td colname="col1"> <p>数字 </p> </td> 
      <td colname="col2"> <p>下载持续时间（以毫秒为单位）。 </p> <p>TVSDK不区分客户端连接到服务器所用的时间和下载完整片段所用的时间。 例如，如果下载10 MB的片段需要8秒，TVSDK会提供该信息，但不会告诉您第一个字节之前需要4秒，而下载整个片段需要4秒。 </p> </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration </span> </td> 
      <td colname="col1"> <p>数字 </p> </td> 
      <td colname="col2"> 已下载片段的媒体持续时间（以毫秒为单位）。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 大小 </span> </td> 
      <td colname="col1"> <p>数字 </p> </td> 
      <td colname="col2"> 已下载资源的大小（字节）。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex </span> </td> 
      <td colname="col1"> <p>int </p> </td> 
      <td colname="col2"> 相应轨道的索引（如果已知）；否则为0。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackName </span> </td> 
      <td colname="col1"> <p>字符串 </p> </td> 
      <td colname="col2"> 相应跟踪的名称（如果已知）；否则为null。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackType </span> </td> 
      <td colname="col1"> <p>字符串 </p> </td> 
      <td colname="col2"> 相应跟踪的类型（如果已知）；否则为null。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> type </span> </td> 
      <td colname="col1"> <p>字符串 </p> </td> 
      <td colname="col2"> TVSDK下载了什么。 以下任一项： 
      <ul id="ul_FA02F42D109344F4866073908CA4E835"> 
      <li id="li_0E2D3EBCAB58477FB5EA526C54FACFFB">清单 — 播放列表/清单 </li> 
      <li id="li_D7894C2F0CB64C909C6398288EA5683A">片段 — 片段 </li> 
      <li id="li_4D4FEDB7704C411B80891B5028B0C20E">TRACK — 与特定跟踪关联的片段 </li> 
      </ul> 有时可能无法检测资源的类型。 如果发生这种情况，则返回FILE。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> url </span> </td> 
      <td colname="col1"> <p>字符串 </p> </td> 
      <td colname="col2"> 指向已下载资源的URL。 </td> 
   </tr> 
   </tbody> 
   </table>
