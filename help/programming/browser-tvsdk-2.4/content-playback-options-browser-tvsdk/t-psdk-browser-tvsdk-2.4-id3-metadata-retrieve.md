---
description: ID3标记提供有关音频或视频文件的信息，例如文件标题或艺人姓名。 浏览器TVSDK在HLS流中的传输流(TS)区段级别检测ID3标记并调度事件。 应用程序可以从标记中提取数据。
title: ID3标记
exl-id: 33510821-9de4-41fc-b404-bcf0b6ba86ff
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# ID3标记{#id-tags}

ID3标记提供有关音频或视频文件的信息，例如文件标题或艺人姓名。 浏览器TVSDK在HLS流中的传输流(TS)区段级别检测ID3标记并调度事件。 应用程序可以从标记中提取数据。

在基础HLS流中找到新的ID3元数据时，浏览器TVSDK会触发 `AdobePSDK.TimedMetadataEvent` 事件。

此 `TimedMetadata` ID3的对象具有以下属性：

<table id="table_6C61886187FB44B4B9821E4B00200018"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 属性名称 </th> 
   <th colname="col2" class="entry"> 详细信息 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> type </span> </p> </td> 
   <td colname="col2"> <p>一种类型 <span class="codeph"> Timedatadata </span> 对象。 </p> <p>对于ID3元数据，值为 <span class="codeph"> AdobePSDK.TimedMetadataType.ID3 </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> 时间 </span> </p> </td> 
   <td colname="col2"> <p> 检测到此定时元数据的播放器时间。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> id </span> </p> </td> 
   <td colname="col2"> <p>ID <span class="codeph"> Timedatadata </span> 对象。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> name </span> </p> </td> 
   <td colname="col2"> <p>名称 <span class="codeph"> Timedatadata </span> 对象。 对于ID3元数据，值为“ID3”。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> 内容 </span> </p> </td> 
   <td colname="col2"> <p>定时元数据内容。 对于ID3标记，此值表示序列化的字节数组。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> 元数据 </span> </p> </td> 
   <td colname="col2"> <p> <span class="codeph"> Timedatadata </span> 已处理的信息，它是 <span class="codeph"> AdobePSDK.Metadata </span> 存储ID3帧的位置。 </p> <p> <p>注意：对于Safari <span class="codeph"> 视频 </span> 标签中，ID3标签的特定帧数据通过 <span class="codeph"> AdobePSDK.Metadata </span> 对象，而对于其他浏览器，ID3标记的帧数据将通过以字节数组的形式显示 <span class="codeph"> AdobePSDK.Metadata </span> 对象。 </p> </p> </td> 
  </tr> 
 </tbody> 
</table>

&#x200B;

存储在中的各种ID3标记 `TimedMetadata` 应用程序可以通过以下两种方式检索：

* 在AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE事件侦听器中。

   ```
   var isSafari = function () { 
       var nAgt = navigator.userAgent; 
       var appName = navigator.appName; 
       if ((nAgt.indexOf('MSIE') === -1) && //is not MS IE 
           (appName !== 'Netscape' || nAgt.indexOf('Trident/') === -1) && //is not MS IE11 
           (appName !== 'Netscape' || nAgt.indexOf('Edge') === -1) && // is not edge 
           (nAgt.indexOf('Chrome') === -1) && // is not chrome 
           (nAgt.indexOf('Safari') !== -1) //is Safari 
       ){ 
           return true; 
       } 
       return false; 
   }; 
   var hex2a = function (hex, offset, max) { 
       var str = ''; 
       if (!hex) 
           return str; 
       for (var i = offset; i < hex.length && i < offset + max; i++) 
           str += String.fromCharCode(hex[i]); 
       return str; 
   }; 
   var mediaPlayer = new AdobePSDK.MediaPlayer(); 
   mediaPlayer.addEventListener( AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE ,function(event){ 
       var td = event.timedMetadata; 
       if(td.type == AdobePSDK.TimedMetadataType.ID3){ 
           var md = td.metadata; 
           var keySet = md.keySet; 
           var onSafari = isSafari(); 
           if(keySet && keySet.length){ 
               var msg = ''; 
               for(var j = 0; j < keySet.length; j++){ 
                   var idTag = keySet[j]; 
                   msg += idTag; 
                   if(idTag.indexOf("T") == 0){ 
                       /* text frame*/ 
                       if(onSafari){ 
                           /* text frame data is exposed in object format 
                            * where corresponding text data is exposed through 
                            * data key of text frame data object 
                            * */ 
                           var frameDataObject = md.getObject(idTag); 
                           msg += " : " + frameDataObject.data; 
                       } else { 
                           var buff = md.getByteArray(idTag); 
                           msg += " : " + hex2a(buff, 0, buff.length - 1); 
                       } 
                   } 
                   msg += " ; "; 
               } 
           } 
       } 
   }); 
   ```

* 使用 `MediaPlayerItem`的 `timedMetadata` 属性。

   ```
   var isSafari = function () { 
       var nAgt = navigator.userAgent; 
       var appName = navigator.appName; 
       if ((nAgt.indexOf('MSIE') === -1) && //is not MS IE 
           (appName !== 'Netscape' || nAgt.indexOf('Trident/') === -1) && //is not MS IE11 
           (appName !== 'Netscape' || nAgt.indexOf('Edge') === -1) && // is not edge 
           (nAgt.indexOf('Chrome') === -1) && // is not chrome 
           (nAgt.indexOf('Safari') !== -1) //is Safari 
       ){ 
           return true; 
       } 
       return false; 
   }; 
   var hex2a = function (hex, offset, max) { 
       var str = ''; 
       if (!hex) 
           return str; 
       for (var i = offset; i < hex.length && i < offset + max; i++) 
           str += String.fromCharCode(hex[i]); 
       return str; 
   }; 
   var timedMetadataList = player.currentItem.timedMetadata; 
   for(var i = 0; i < timedMetadataList.length; i++){ 
       var td = timedMetadataList[i]; 
       if(td.type == AdobePSDK.TimedMetadataType.ID3){ 
           var md = td.metadata; 
           var keySet = md.keySet; 
           var onSafari = isSafari(); 
           if(keySet && keySet.length){ 
               var msg = ''; 
               for(var j = 0; j < keySet.length; j++){ 
                   var idTag = keySet[j]; 
                   msg += idTag; 
                   if(idTag.indexOf("T") == 0){ 
                       /* text frame*/ 
                       if(onSafari){ 
                           /* text frame data is exposed in object format 
                            * where corresponding text data is exposed through 
                            * data key of text frame data object 
                            * */ 
                           var frameDataObject = md.getObject(idTag); 
                           msg += " : " + frameDataObject.data; 
                       } else { 
                           var buff = md.getByteArray(idTag); 
                           msg += " : " + hex2a(buff, 0, buff.length - 1); 
                       } 
                   } 
                   msg += " ; "; 
               } 
           } 
       } 
   } 
   ```
