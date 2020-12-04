---
description: 您可以从LoadInformation类读取有关下载资源（如片段和轨道）的服务质量(QoS)信息。
seo-description: 您可以从LoadInformation类读取有关下载资源（如片段和轨道）的服务质量(QoS)信息。
seo-title: 使用加载信息在片段级别跟踪
title: 使用加载信息在片段级别跟踪
uuid: 41fb2b90-3531-4cc5-bf9b-01ccae04d2fd
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# 使用加载信息{#track-at-the-fragment-level-using-load-information}在片段级别跟踪

您可以从LoadInformation类读取有关下载资源（如片段和轨道）的服务质量(QoS)信息。

1. 实现`onLoadInformationAvailable`回调事件监听器。

   ```
   private function onLoadInformationAvailable(event:LoadInformationEvent):void { 
       var loadInformation:LoadInformation = event.loadInformation; 
       // process the load information here     
   }
   ```

1. 注册事件监听器，TVSDK每次下载片段时都会调用它。

   ```
   player.addEventListener(LoadInformationEvent.LOAD_INFORMATION_AVAILABLE,  
                                    onLoadInformationAvailable);
   ```

1. 从传递到回调的`LoadInformation`中读取感兴趣的数据。

   <table id="table_75E61A2EB25E435DB631166A7FF64757"> 
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
      <td colname="col1"> <p>数字 </p> </td> 
      <td colname="col2"> <p>下载的持续时间（以毫秒为单位）。 </p> <p>TVSDK并不区分客户端连接到服务器的时间和下载完整片段所花费的时间。 例如，如果10 MB的片段下载需要8秒，则TVSDK会提供该信息，但不会告诉您直到第一个字节还需要4秒才下载整个片段。 </p> </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration  </span> </td> 
      <td colname="col1"> <p>数字 </p> </td> 
      <td colname="col2"> 下载片段的媒体持续时间（以毫秒为单位）。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 大小  </span> </td> 
      <td colname="col1"> <p>数字 </p> </td> 
      <td colname="col2"> 已下载资源的大小（以字节为单位）。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex  </span> </td> 
      <td colname="col1"> <p>int </p> </td> 
      <td colname="col2"> 相应轨道的索引（如果已知）;否则，为0。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackName  </span> </td> 
      <td colname="col1"> <p>字符串 </p> </td> 
      <td colname="col2"> 相应音轨的名称（如果已知）;否则，为null。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackType  </span> </td> 
      <td colname="col1"> <p>字符串 </p> </td> 
      <td colname="col2"> 相应音轨的类型（如果已知）;否则，为null。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 类型  </span> </td> 
      <td colname="col1"> <p>字符串 </p> </td> 
      <td colname="col2"> TVSDK下载的内容。 以下任一选项： 
      <ul id="ul_FA02F42D109344F4866073908CA4E835"> 
      <li id="li_0E2D3EBCAB58477FB5EA526C54FACFFB">MANIFEST —— 播放列表／清单 </li> 
      <li id="li_D7894C2F0CB64C909C6398288EA5683A">片段——片段 </li> 
      <li id="li_4D4FEDB7704C411B80891B5028B0C20E">TRACK —— 与特定跟踪关联的片段 </li> 
      </ul> 有时，可能无法检测资源的类型。 如果发生这种情况，则返回FILE。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> url  </span> </td> 
      <td colname="col1"> <p>字符串 </p> </td> 
      <td colname="col2"> 指向已下载资源的URL。 </td> 
   </tr> 
   </tbody> 
   </table>
