---
description: ID3标记提供有关音频或视频文件的信息，如文件的标题或艺术家的姓名。 浏览器TVSDK在HLS流中的传输流(TS)段级别检测ID3标记并调度事件。 应用程序可以从标记中提取数据。
seo-description: ID3标记提供有关音频或视频文件的信息，如文件的标题或艺术家的姓名。 浏览器TVSDK在HLS流中的传输流(TS)段级别检测ID3标记并调度事件。 应用程序可以从标记中提取数据。
seo-title: ID3标记
title: ID3标记
uuid: a47cd0cc-b11d-47df-b1fb-56918896ef4c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# ID3标记{#id-tags}

ID3标记提供有关音频或视频文件的信息，如文件的标题或艺术家的姓名。 浏览器TVSDK在HLS流中的传输流(TS)段级别检测ID3标记并调度事件。 应用程序可以从标记中提取数据。

当在基础HLS流中找到新的ID3元数据时，浏览器TVSDK将触发一个 `AdobePSDK.TimedMetadataEvent` 事件。

ID3 `TimedMetadata` 的对象具有以下属性：

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
   <td colname="col2"> <p>TimedMetadata对象 <span class="codeph"> 的类 </span> 型。 </p> <p>对于ID3元数据，该值 <span class="codeph"> 为AdobePSDK.TimedMetadataType.ID3 </span>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> 时间 </span> </p> </td> 
   <td colname="col2"> <p> 检测到此定时元数据的播放器时间。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> id </span> </p> </td> 
   <td colname="col2"> <p>TimedMetadata对象 <span class="codeph"> 的 </span> ID。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> name </span> </p> </td> 
   <td colname="col2"> <p>TimedMetadata对 <span class="codeph"> 象的 </span> 名称。 对于ID3元数据，该值为“ID3”。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> 内容 </span> </p> </td> 
   <td colname="col2"> <p>定时元数据内容。 对于ID3标记，此值表示序列化字节数组。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> 元数据 </span> </p> </td> 
   <td colname="col2"> <p> <span class="codeph"> TimedMetadata </span> 处理的信息，该信息是 <span class="codeph"> AdobePSDK的一个实例。存储 </span> ID3帧的元数据。 </p> <p> <p>注意： 对于Safari <span class="codeph"> 视频标 </span> 签，ID3标签的特定帧数据通过 <span class="codeph"> AdobePSDK以对象形式公开。元数据对象；而对于其他浏览器，ID3标签的帧数据以字节数组形式通过 </span> AdobePSDK.元数据对象公开 <span class="codeph"></span> 。 </p> </p> </td> 
  </tr> 
 </tbody> 
</table>

&#x200B;

应用程序可以通过以下两种方 `TimedMetadata` 式检索存储在中的各种ID3标签：

* 在AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE事件监听器中。

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

* 使用 `MediaPlayerItem`属 `timedMetadata` 性。

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

